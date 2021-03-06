---
layout: page
title: "Q262814: IEEE 1394 OHCI Driver Does Not Retry Busy Devices Properly"
permalink: /kb/262/Q262814/
---

## Q262814: IEEE 1394 OHCI Driver Does Not Retry Busy Devices Properly

{% raw %}

	Article: Q262814
	Product(s): Microsoft Windows NT
	Version(s): WINDOWS:2000
	Operating System(s): 
	Keyword(s): kbDDK kbOSWin2000bug kbDSupport kbGrpDSNTDDK kbADO260fix kbWin2000PreSP2Fix kbWin2000SP
	Last Modified: 17-JUN-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows 2000 Professional 
	- Microsoft Windows 2000 Server 
	- Microsoft Windows 2000 Advanced Server 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	You may be unable to connect to an IEEE (Institute of Electrical and Electronics
	Engineers) 1394 high-performance serial bus-compliant device, such as a digital
	camera.
	
	CAUSE
	=====
	
	This problem can occur if the Ohcil394.sys host controller driver does not retry
	busy devices enough times.
	
	RESOLUTION
	==========
	
	To resolve this problem, obtain the latest service pack for Windows 2000. For
	additional information, please see the following article in the Microsoft
	Knowledge Base:
	
	  Q260910 How to Obtain the Latest Windows 2000 Service Pack
	
	The English version of this fix should have the following file attributes or
	later:
	
	  Date        Time       Version        Size    File name
	  ----------------------------------------------------------
	  06/14/2000  02:58 PM   5.0.2195.2096  36,848  Ohci1394.sys
	
	
	STATUS
	======
	
	Microsoft has confirmed that this is a bug in the Microsoft products that are
	listed at the beginning of this article. This problem was first corrected in
	Windows 2000 Service Pack 2.
	
	MORE INFORMATION
	================
	
	Devices that communicate as specified by the IEEE 1394 specification can respond
	to requests from the computer with a "BusyX" code. In this case, the device is
	busy, because of hardware limitations or software interactions in an early
	generation of the 1394 chipset.
	
	Support for BusyX retries is defined in the IEEE1394-1995 specification and is
	important for successful computer-to-1394 device communications.
	
	For additional information about how to install Windows 2000 and Windows 2000
	hotfixes at the same time, click the article number below to view the article in
	the Microsoft Knowledge Base:
	
	  Q249149 Installing Microsoft Windows 2000 and Windows 2000 Hotfixes
	
	Additional query words: IEEE 1394 ohci
	
	======================================================================
	Keywords          : kbDDK kbOSWin2000bug kbDSupport kbGrpDSNTDDK kbADO260fix kbWin2000PreSP2Fix kbWin2000SP2Fix 
	Technology        : kbwin2000AdvServ kbwin2000AdvServSearch kbwin2000Serv kbwin2000ServSearch kbwin2000Search kbwin2000ProSearch kbwin2000Pro kbWinAdvServSearch
	Version           : WINDOWS:2000
	Hardware          : x86
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
