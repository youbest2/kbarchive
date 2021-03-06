---
layout: page
title: "Q179692: INFO: COM Method Call in WM_PAINT Handler Returns 0x80010005"
permalink: /kb/179/Q179692/
---

## Q179692: INFO: COM Method Call in WM_PAINT Handler Returns 0x80010005

{% raw %}

	Article: Q179692
	Product(s): Microsoft C Compiler
	Version(s): 4.2,4.2b,5.0,6.0
	Operating System(s): 
	Keyword(s): kbcode kbole kbnokeyword kbActiveX kbCOMt kbContainer kbMFC kbVC420 kbVC500 kbVC600 kbG
	Last Modified: 25-APR-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- The Microsoft Foundation Classes (MFC), used with:
	   - Microsoft Visual C++, 32-bit Enterprise Edition, versions 4.2, 4.2b, 5.0, 6.0 
	   - Microsoft Visual C++, 32-bit Professional Edition, versions 4.2, 4.2b, 5.0, 6.0 
	   - Microsoft Visual C++, 32-bit Learning Edition, version 6.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	When calling methods on a COM server from within OnDraw() or a WM_PAINT message
	handler of an MFC client application, you may receive an HRESULT of 0x80010005
	(RPC_E_CANTCALLOUT_INEXTERNALCALL - it is illegal to call out while inside
	message filter) as the return value of a COM call to a server.
	
	MORE INFORMATION
	================
	
	MFC has a default implementation of IMessageFilter(COleMessageFilter).
	IMessageFilter is used by COM servers and clients to selectively handle incoming
	and outgoing COM messages while waiting for a response from synchronous calls.
	MFC's implementation allows processing of WM_PAINT messages (to keep the UI
	updated) on the COM client side, while waiting on a synchronous COM call to a
	server (for example, a call to an automation method). This is done through
	IMessageFilter::MessagePending(). Thus, when calling a COM server method inside
	of a WM_PAINT handler, you could already be in the middle of a call to the
	server, and therefore receive the error 0x80010005.
	
	As with any Windows application, the code in WM_PAINT handlers should be minimal.
	If at all possible, do not have any calls to COM servers in WM_PAINT handlers.
	
	To resolve this problem you could use any one of the following three
	workarounds:
	
	- In the WM_PAINT handler, post yourself a user-defined message; in the handler
	  for the user-defined message, make the call to the COM server. -or-
	
	  Create a secondary UI thread that creates and makes all calls to the COM
	  servers.
	
	  -or-
	
	  Modify MFC's default implementation of MessageFilter::MessagePending(), which
	  currently processes WM_PAINT messages. To do this, derive a class from
	  COleMessageFilter and override the virtual function OnMessagePending():
	
	        CMyMessageFilter : public COleMessageFilter
	        {
	           virtual BOOL OnMessagePending(const MSG* pMsg);
	        }
	
	        BOOL CMyMessageFilter::OnMessagePending(const MSG* pMsg)
	        {
	           //The base class function dispatches WM_PAINT
	           //by returning FALSE no messages are being processed; the
	           //user can add code here to appropriately handle messages.
	           //WARNING: Not processing WM_PAINT messages will cause the user
	           //         interface to appear to hang and not update until the
	           //         current COM method call returns.
	           return FALSE;
	        }
	
	Then, in the InitInstance() of the CWinApp derived class, unregister the
	IMessageFilter MFC registers for you when calling AfxOleInit(). Add this code
	after the call to AfxOleInit(). Then instantiate a class of type
	CMyMessageFilter and register it:
	
	     BOOL CmyApp::InitInstance()
	     {
	        // Initialize OLE libraries and registers default message filter.
	        if (!AfxOleInit())
	        {
	           AfxMessageBox(IDP_OLE_INIT_FAILED);
	           return FALSE;
	        }
	
	        CWinThread* pThread = AfxGetThread();
	        if (pThread != NULL)
	        {
	           // Destroy message filter, thereby unregistering it.
	           delete pThread->m_pMessageFilter;
	           pThread->m_pMessageFilter = NULL;
	
	           // Create the new message filter object.
	           pThread->m_pMessageFilter = new CMyMessageFilter;
	           ASSERT(AfxOleGetMessageFilter() != NULL);
	
	           // Register the new message filter object.
	           AfxOleGetMessageFilter()->Register();
	        }
	        ...
	        ...
	     }
	
	For more information on how message filters work, please see the online
	documentation on IMessageFilter and COleMessageFilter.
	
	REFERENCES
	==========
	
	"Inside OLE", second edition, by Kraig Brockschmidt, Chapter 6, "Local/Remote
	Transparency," published by Microsoft Press.
	
	Visual C++ Books Online and the MFC source code for the functions mentioned in
	this article.
	
	(c) Microsoft Corporation 1997, All Rights Reserved. Contributions by Jaganathan
	Thangavelu, Microsoft Corporation.
	
	Additional query words: 80010005 2147549189 IMessageFilter MessagePending COleMessageFilter OnDraw
	
	======================================================================
	Keywords          : kbcode kbole kbnokeyword kbActiveX kbCOMt kbContainer kbMFC kbVC420 kbVC500 kbVC600 kbGrpDSMFCATL kbArchitecture 
	Technology        : kbAudDeveloper kbMFC
	Version           : :4.2,4.2b,5.0,6.0
	Issue type        : kbinfo
	
	=============================================================================
	

{% endraw %}
