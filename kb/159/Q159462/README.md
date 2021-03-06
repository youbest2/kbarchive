---
layout: page
title: "Q159462: SNA Server 802.2 Connection Stays in Pending State"
permalink: /kb/159/Q159462/
---

## Q159462: SNA Server 802.2 Connection Stays in Pending State

{% raw %}

	Article: Q159462
	Product(s): Microsoft SNA Server
	Version(s): WINDOWS:2.0,2.1,2.11,2.11 SP1,2.11 SP2,3.0,3.0 SP1,3.0 SP2,3.0 SP3,4.0,4.0 SP1
	Operating System(s): 
	Keyword(s): 
	Last Modified: 12-JUN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft SNA Server, versions 2.0, 2.1, 2.11, 2.11 SP1, 2.11 SP2, 3.0, 3.0 SP1, 3.0 SP2, 3.0 SP3, 4.0, 4.0 SP1 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	A computer running SNA Server on an Ethernet network that has an 802.2 DLC
	connection configured to communicate with a remote device (AS/400, 3174, or
	3745, for example) on a Token Ring may exhibit the following symptoms:
	
	- The 802.2 DLC Connection configured in SNA Server Admin stays in a perpetual
	  "Pending" state.
	
	- The Windows NT Application Event Log on the SNA Server does not contain any
	  events that indicate connection activation problems. The Application Log will
	  usually contain an Event 230 or an Event 23 when an 802.2 DLC connection
	  fails to activate.
	
	- A Network General Sniffer(TM) or Microsoft Network Monitor trace on the
	  Ethernet segment of the computer running SNA Server shows an XID exchange
	  that never completes. The computer running SNA Server never receives the
	  SABME mode setting command from the remote system to indicate the end of the
	  XID exchange.
	
	CAUSE
	=====
	
	This problem has been observed when SNA Server is connected to the remote system
	across a Cisco router which is configured for LLC Local Acknowledgment. The
	Cisco router fails to forward the SABME command sent by the remote device (for
	example, IBM 3745) to SNA Server, causing the connection to fail to activate.
	The result is that the SNA Server restarts the XID process by sending a
	pre-negotiation XID to the remote device. This process continues indefinitely.
	
	RESOLUTION
	==========
	
	To work around this problem:
	
	- Disable Local Acknowledgment on the Cisco router(s) between the Ethernet and
	  Token Ring.
	
	MORE INFORMATION
	================
	
	In an LLC (802.2 DLC) session, when Device A sends a frame to Device B, Device A
	expects Device B to respond before the T1 timer expires. In a WAN environment
	that contains slow links, it is possible to see the T1 timer expire before a
	response was received causing retransmissions. Cisco's Local Acknowledgment
	feature attempts to solve this problem by splitting the LLC session between the
	two devices. If Local Acknowledgment is configured, the LLC session between two
	two devices is not end-to-end but instead terminates at the local router(s). The
	LLC session with Device A ends at the Router as does the LLC session with Device
	B. The router then responds to the frames sent from Devices A and B instead of
	having the actual device send the response. When this feature is enabled, all
	LLC supervisory frames (RR, RNR, REJ) from one of the devices go no farther than
	the router since the router will respond to them on behalf of the other device.
	
	The third-party products discussed here are manufactured by vendors independent
	of Microsoft; we make no warranty, implied or otherwise, regarding these
	products' performance or reliability.
	
	REFERENCES
	==========
	
	For additional information on SNA Server and 802.2 Connection Timers, please see
	the following article in the Microsoft Knowledge Base:
	
	  Q129786 SNA Server and 802.2 Connection Timers (t1, t2, ti)
	
	Additional query words: prodsna spoofing llc2
	
	======================================================================
	Keywords          :  
	Technology        : kbAudDeveloper kbSNAServSearch kbSNAServ300 kbSNAServ200 kbSNAServ211 kbSNAServ400 kbSNAServ210 kbSNAServ211SP1 kbSNAServ211SP2 kbSNAServ300SP3 kbSNAServ300SP1 kbSNAServ400SP1 kbSNAServ300SP2
	Version           : WINDOWS:2.0,2.1,2.11,2.11 SP1,2.11 SP2,3.0,3.0 SP1,3.0 SP2,3.0 SP3,4.0,4.0 SP1
	
	=============================================================================
	

{% endraw %}
