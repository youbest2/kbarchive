---
layout: page
title: "Q136934: Event ID 7000 and 7001 Appear When You Use HTTP and GSNW"
permalink: /kb/136/Q136934/
---

## Q136934: Event ID 7000 and 7001 Appear When You Use HTTP and GSNW

{% raw %}

	Article: Q136934
	Product(s): Microsoft Windows NT
	Version(s): 3.51 4.0
	Operating System(s): 
	Keyword(s): kbnetwork
	Last Modified: 08-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Server versions 3.51, 4.0 
	- MSPRESS Microsoft Windows NT Resource Kit, version 3.51 
	- Microsoft Windows NT Workstation version 4.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When you use the Hyper Text Transfer Protocol (HTTP) service in Windows NT 3.51
	Resource Kit with Gateway Services for NetWare (GSNW), the following system
	events appear in the Event Viewer when you start Windows NT:
	
	  Event ID: 7000
	  Source: Service Control Manager
	  Type: Error
	  Description: The MUP service failed to start due to the following error: An
	  instance of the service is already running.
	
	  Event ID: 7001
	  Source: Service Control Manager
	  Type: Error
	  Description: HTTP server service depends on the MUP service which failed to
	  start because of the following error: An instance of the service is already
	  running.
	
	RESOLUTION
	==========
	
	To correct this problem:
	
	WARNING: Using Registry Editor incorrectly can cause serious, system-wide
	problems that may require you to reinstall Windows NT to correct them. Microsoft
	cannot guarantee that any problems resulting from the use of Registry Editor can
	be solved. Use this tool at your own risk.
	
	1. Run Registry Editor (REGEDT32.EXE).
	
	2. From the HKEY_LOCAL_MACHINE subtree, go to the following subkey:
	
	  \SYSTEM\CurrentControlSet\Services\HTTPS
	
	3. For the following value name, remove MUP:
	
	  Value Name: DependOnService
	  Data Type: REG_MULTI_SZ
	  String: MUP Tcpip AFD
	
	4. Quit Registry Editor.
	
	5. Shutdown and restart Windows NT.
	
	Additional query words: prodnt
	
	======================================================================
	Keywords          : kbnetwork 
	Technology        : kbWinNTsearch kbWinNTWsearch kbWinNTW400 kbWinNTW400search kbWinNT351search kbWinNT400search kbWinNTSsearch kbWinNTS400search kbWinNTS400 kbWinNTS351 kbMSPressSearch kbWinNTS351search kbZNotKeyword6 kbZNotKeyword2 kbZNotKeyword5
	Version           : 3.51 4.0
	
	=============================================================================
	

{% endraw %}
