---
layout: page
title: "Q264632: DLC Session Hangs When Using DLSW"
permalink: kb/264/Q264632/
---

## Q264632: DLC Session Hangs When Using DLSW

	Article: Q264632
	Product(s): Microsoft Windows NT
	Version(s): 4.0
	Operating System(s): 
	Keyword(s): kbWinNT400PreSP7Fix
	Last Modified: 08-MAY-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Server version 4.0 
	- Microsoft Windows NT Workstation version 4.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	You may experience session disconnects under heavy network load when you are
	using Cisco routers with Data-Link Switching (DLSW) activated.
	
	CAUSE
	=====
	
	When an error condition occurs on the network, the stations attempt to
	reconnect. When you are using DLSW, the Windows NT Data Link Control (DLC) stack
	may enter an invalid state from which it cannot recover. If you are using a
	Network Monitor trace, the problem is visible when the client's DLC stack sends
	"I" frames although it should be in a disconnected state.
	
	RESOLUTION
	==========
	
	A supported fix is now available from Microsoft, but it is only intended to
	correct the problem described in this article and should be applied only to
	systems experiencing this specific problem. This fix may receive additional
	testing at a later time, to further ensure product quality. Therefore, if you
	are not severely affected by this problem, Microsoft recommends that you wait
	for the next Windows NT 4.0 service pack that contains this fix.
	
	To resolve this problem immediately, contact Microsoft Product Support Services
	to obtain the fix. For a complete list of Microsoft Product Support Services
	phone numbers and information about support costs, please go to the following
	address on the World Wide Web:
	
	  http://support.microsoft.com/default.aspx?scid=fh;EN-US;CNTACTMS
	
	NOTE: In special cases, charges that are normally incurred for support calls may
	be canceled, if a Microsoft Support Professional determines that a specific
	update will resolve your problem. Normal support costs will apply to additional
	support questions and issues that do not qualify for the specific update in
	question.
	
	The English version of this fix should have the following file attributes or
	later:
	
	  Date      Time      Size     File name  Platform
	  ------------------------------------------------
	  07/12/2000  05:06p  102,512  Dlc.sys    Alpha
	  07/12/2000  05:08p   55,376  Dlc.sys    Intel
	
	
	
	WORKAROUND
	==========
	
	If local "acks" (DLC spoofing) are disabled on the routers, this problem does
	not occur.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in the Microsoft products that are
	listed at the beginning of this article.
	
	Additional query words:
	
	======================================================================
	Keywords          : kbWinNT400PreSP7Fix 
	Technology        : kbWinNTsearch kbWinNTWsearch kbWinNTW400 kbWinNTW400search kbWinNT400search kbWinNTSsearch kbWinNTS400search kbWinNTS400
	Version           : :4.0
	Hardware          : ALPHA x86
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	