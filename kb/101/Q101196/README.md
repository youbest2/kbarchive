---
layout: page
title: "Q101196: LastDrive Affects Windows on Novell and LAN Manager"
permalink: /kb/101/Q101196/
---

## Q101196: LastDrive Affects Windows on Novell and LAN Manager

{% raw %}

	Article: Q101196
	Product(s): Microsoft Windows 95.x Retail Product
	Version(s): WINDOWS:3.1,3.11
	Operating System(s): 
	Keyword(s): 
	Last Modified: 03-OCT-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows versions 3.1, 3.11 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	Not having a LastDrive statement in the CONFIG.SYS file or setting the LastDrive
	statement to a "low" (that is, alphabetically early) drive letter (such as E)
	limits the number of network drive connections available when you are using
	Microsoft LAN Manager version 2.0, 2.1, or 2.2 and Novell NetWare (when you are
	using a monolithic workstation redirector [NETX.COM or NETX.EXE]).
	
	MORE INFORMATION
	================
	
	LAN Manager Versions 2.0 and 2.1
	--------------------------------
	
	If the LastDrive statement in the CONFIG.SYS file is not present, LastDrive is
	set to a default of E. If drive E is being used by a physical partition or for
	some other purpose, the default LastDrive setting needs to be increased.
	
	If LastDrive is set to a low drive letter and all drive letters become used,
	Windows may hang at startup or may display the error message "Cannot read from
	drive x:."
	
	LAN Manager Version 2.2
	-----------------------
	
	If the LastDrive statement in the CONFIG.SYS file is not present, LAN Manager
	sets LastDrive to E by default unless the last physical partition on the local
	drive is greater than E; in that scenario, LastDrive is set to the letter value
	of the last physical partition on the local drive. Once the number of drives in
	use equals the letter value of LastDrive, LastDrive does not allow connections
	to additional drive letters. This limitation of available drives also occurs if
	the LastDrive statement is set to a low drive letter and all the network drives
	are in use.
	
	When all network drives are in use, File Manager does not allow additional
	network drive connections. Usually, the Drive Letter box automatically
	increments to the next available drive letter. However, if all network drives
	are in use, the Drive Letter box remains blank because no more network drive
	letters are available.
	
	To correct this problem, edit the LastDrive statement in the CONFIG.SYS file so
	that it reads "LastDrive=Z" (without the quotation marks) and then restart your
	computer.
	
	Now, when you connect to a new network drive the Drive Letter box should
	increment to the next available drive letter.
	
	Novell NetWare Using a Monolithic Workstation Redirector
	--------------------------------------------------------
	
	Novell NETX.COM and NETX.EXE use the LastDrive statement to determine at which
	drive letter network drives are available. For example, if LastDrive=Z, then it
	is impossible to log on to Novell.
	
	To correct this problem, edit the LastDrive statement in the CONFIG.SYS file so
	that it uses the last physical drive on the local workstation and then restart
	your computer.
	
	This should allow you to log on to the Novell server successfully.
	
	Additional query words: 3.10 3.1 last drive server net error message err msg lanman login logon netware hang hangs lock locks stop reboot
	
	======================================================================
	Keywords          :  
	Technology        : kbWin3xSearch kbZNotKeyword3 kbWin310 kbWin311
	Version           : WINDOWS:3.1,3.11
	
	=============================================================================
	

{% endraw %}
