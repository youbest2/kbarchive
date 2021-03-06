---
layout: page
title: "Q139692: FIX: Assertion Failed, Line 475 of Sockcore.cpp"
permalink: /kb/139/Q139692/
---

## Q139692: FIX: Assertion Failed, Line 475 of Sockcore.cpp

{% raw %}

	Article: Q139692
	Product(s): Microsoft C Compiler
	Version(s): winnt:2.0,2.1,2.2
	Operating System(s): 
	Keyword(s): kbMFC kbVC152bug kbVC200bug kbVC210bug kbVC220bug kbVC400fix kbWinsock kbGrpDSMFCATL kb
	Last Modified: 06-MAY-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- The Microsoft Foundation Classes (MFC), used with:
	   - Microsoft Visual C++ for Windows, 16-bit edition, version 1.52 
	   - Microsoft Visual C++, 32-bit Editions, versions 2.0, 2.1, 2.2 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	An MFC application that uses the socket classes and makes sequential calls to
	close and create sockets encounters an assertion failure:
	
	In MFC 3.1 and 3.2, the assertion appears as:
	
	  Assertion Failed: <app name>: File sockcore.cpp, Line 475
	
	In MFC 2.52, the assertion appears as:
	
	  Assertion Failed: <app name>: File sockcore.cpp, Line 456
	
	CAUSE
	=====
	
	MFC maintains a map of dead sockets. (A dead socket is a socket that was open
	but that has been closed.) The purpose of this map is described in further
	detail in the "More Information" section of this article.
	
	If an application closes and opens sockets in the same thread without yielding to
	process messages, then it is possible that an attempt will be made to close a
	socket that has already been closed. MFC does not properly handle this because
	it can only have one entry in the map of dead sockets. The resulting assertion
	failure is checking whether there is already an entry in the map of dead
	sockets:
	
	     ASSERT(CAsyncSocket::LookupHandle(hSocket, TRUE) == NULL);
	     // The TRUE means it is looking for a dead socket handle,
	     // thus the assertion failure occurs.
	
	RESOLUTION
	==========
	
	There are four possible resolutions:
	
	- The problem occurs only if you are closing and opening sockets sequentially
	  without yielding to process messages. If you are doing this to send many
	  small packets of data, there might be other approaches that would work
	  better. See the "More Information" section of this article for further
	  details.
	
	-or-
	
	- One pretty simple resolution is to suspend the closing of any sockets until
	  all sockets have been opened. This prevents any new SOCKET from being opened
	  (and subsequently closed) that happens to have the same SOCKET handle as a
	  previously closed socket.
	
	-or-
	
	- You can write a routine to process all pending socket messages immediately
	  after calling Close and before continuing with code execution. This could be
	  done, for example, in the Close member function of your own
	  CAsyncSocket-derived or CSocket-derived class:
	
	     #include <afxpriv.h>
	
	     void CMySocket::Close()
	     {
	       // For the socket about to be closed.
	       SOCKET hDeadSocket = m_hSocket;
	
	       CAsyncSocket::Close();
	       // or for CSocket-derived class:
	       // CSocket::Close();
	
	       MSG msg;
	       CSocket::ProcessAuxQueue();
	       while(::PeekMessage(&msg,NULL,
	               WM_SOCKET_NOTIFY,WM_SOCKET_DEAD,PM_REMOVE))
	       {
	         ::DispatchMessage(&msg);
	         if( (msg.message==WM_SOCKET_DEAD) &&
	             ((SOCKET)msg.wParam==hDeadSocket))
	           break;
	       }
	     }
	
	  The virtual destructor should also be overridden to make sure the correct
	  Close is called:
	
	     CMySocket::~CMySocket()
	     {
	       if (m_hSocket != INVALID_SOCKET)
	         Close();
	     }
	
	  NOTE: This will cause CAsyncSocket-overriden and CSocket-overridden callbacks
	  (for example, OnReceive, OnAccept) to be called for any currently open
	  sockets that have notification messages pending in the queue.
	
	-or-
	
	- Restructure the code so that the Close/Open operations are not in a non-
	  yielding sequence. This could be done by providing a message handler for a
	  user-defined message and by performing a specific operation in that message
	  handler. Rather than just proceeding with the thread of execution, a function
	  call that Closes or Destroys a CAsyncSocket/CSocket object should be followed
	  by a PostMessage with the user-defined message. This way all other messages
	  (including the WM_SOCKET_DEAD message) will be processed before the
	  subsequent socket operations are performed.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a bug in the Microsoft products listed at the
	beginning of this article. This problem was corrected in the version of MFC that
	ships with Microsoft Visual C++, 32-bit Edition, version 4.0.
	
	MORE INFORMATION
	================
	
	Sending Small Packets of Data
	-----------------------------
	
	If you are just interested in sending small packets of data back and forth, then
	opening and closing several STREAM type sockets might not be the best solution.
	STREAM sockets were created for sending large amounts of data reliably. Two
	alternate solutions (using one persistent connection or using DATAGRAM sockets)
	might be more suitable and would probably provide better performance than you
	would get by opening and closing many STREAM type socket connections.
	
	Using One Persistent Connection
	-------------------------------
	
	If you are sending this data between the same processes, you can do something
	like what the Chatter and ChatSrvr samples do. They both have a Message
	Structure defined. They open a socket connection and leave it open. Then they
	just send multiple Message Structures back and forth to each other through the
	socket until one or the other side decides to disconnect permanently. Then the
	LastMessage bit is set in the Message Structure and sent to the other process.
	The other process then closes down gracefully.
	
	Using DATAGRAM Sockets
	----------------------
	
	You can open a single unconnected DATAGRAM socket, and use the SendTo and
	ReceiveFrom functions to send little bits of data between processes.
	
	This might be a better approach because it does not require you to use the
	overhead of opening or closing a socket connection for every message you send.
	You can just use an unconnected DATAGRAM socket, and use SendTo when you need to
	send the data. Additionally, DATAGRAM sockets are generally faster than STREAM
	sockets. The primary catch here is that DATAGRAM sockets do not guarantee
	delivery of your data -- although on many systems, they are almost as reliable
	as STREAM sockets.
	
	The WM_SOCKET_DEAD Mechanism
	----------------------------
	
	MFC has a mechanism for preventing a problem that occurs when a socket has been
	closed while there were still notification messages in the application's message
	queue that were bound for that socket.
	
	The problem is that a new socket could be opened that has the same handle as the
	socket that was closed. The messages that still existed in the message queue are
	eventually received, and they appear to be destined for the newly opened socket.
	This can cause a variety of problems. For example, OnReceive might be called for
	a socket that actually has nothing to receive.
	
	MFC's appraoch to handling this problem uses a special message called
	WM_SOCKET_DEAD. Whenever a socket is closed, the following occurs:
	
	1. The SOCKET handle is removed from the map of attached sockets.
	
	2. The SOCKET handle is placed in the map of dead sockets.
	
	3. The WM_SOCKET_DEAD message is posted to the application's message queue with
	  a wParam indicating the closed SOCKET handle.
	
	NOTE: These first three steps are implemented in CAsyncSocket::KillSocket, in
	Sockcore.cpp.
	
	1. The message routing mechanism for MFC's hidden socket notification window
	  ignores all messages for a SOCKET handle while the SOCKET handle is in the
	  map of dead sockets.
	
	2. The SOCKET handle is not removed from the map of dead sockets until the
	  WM_SOCKET_DEAD message is received.
	
	By POSTING the WM_SOCKET_DEAD message, MFC causes all pending socket messages for
	that particular SOCKET handle to be ignored until the WM_SOCKET_DEAD message is
	received. The effect of this is to ignore any notifications that were pending
	for the now-dead socket. Any messages received after that are notifications for
	the open socket and those messages will be properly handled.
	
	Additional query words: 2.52 2.10 2.20 3.10 3.20 4.00 CSocket CAsyncSocket
	
	======================================================================
	Keywords          : kbMFC kbVC152bug kbVC200bug kbVC210bug kbVC220bug kbVC400fix kbWinsock kbGrpDSMFCATL kbNoUpdate kbbuglist kbfixlist
	Technology        : kbAudDeveloper kbMFC
	Version           : winnt:2.0,2.1,2.2
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
