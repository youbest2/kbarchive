---
layout: page
title: "Q166991: OS/2 Error 1588444941 When Starting OS/2 App as a Service"
permalink: /kb/166/Q166991/
---

## Q166991: OS/2 Error 1588444941 When Starting OS/2 App as a Service

{% raw %}

	Article: Q166991
	Product(s): Microsoft Windows NT
	Version(s): 3.5,3.51,4.0
	Operating System(s): 
	Keyword(s): kbtshoot
	Last Modified: 25-FEB-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Workstation versions 3.5, 3.51, 4.0 
	- Microsoft Windows NT Server versions 3.5, 3.51, 4.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	Your attempts to launch the OS/2-based applications may fail when started as a
	service with OS/2 error 1588444941. The error may still occur even though the
	application will launch fine in console mode.
	
	CAUSE
	=====
	
	The above error indicates a failure loading. This can be because of corruption
	in either the application or the OS/2 subsystem files.
	
	RESOLUTION
	==========
	
	Try to remove and reinstall the application software before you attempt to
	replace the OS/2 subsystem files as corrupt application files are more often the
	cause of the error.
	
	To reinstall the OS/2 subsystem use EXPAND.EXE or EXPNDW32.EXE (found in the
	Windows NT Resource Kit) for the following files:
	
	  OS2SS.EXE    - %SystemRoot%\System32\ 
	  OS2.EXE      - %SystemRoot%\System32\ 
	  OS2SRV.EXE   - %SystemRoot%\System32\ 
	  NETAPI.DLL   - %SystemRoot%\System32\Os2\Dll\ 
	  doscalls.dll - %SystemRoot%\System32\Os2\Dll\ 
	
	Oso001.009 does not need to be expanded, but replace the file in the
	%SystemRoot%\System32\Os2\ with a fresh copy.
	
	For steps to remove the OS/2 subsystem registry entries please see the following
	Microsoft Knowledge Base article:
	
	  ARTICLE-ID: Q94566
	  TITLE : GP Fault in OS/2 Subsystem
	
	
	Additional query words:
	
	======================================================================
	Keywords          : kbtshoot 
	Technology        : kbWinNTsearch kbWinNTWsearch kbWinNTW400 kbWinNTW400search kbWinNT351search kbWinNT350search kbWinNT400search kbWinNTW350 kbWinNTW350search kbWinNTW351search kbWinNTW351 kbWinNTSsearch kbWinNTS400search kbWinNTS400 kbWinNTS351 kbWinNTS350 kbWinNTS351search kbWinNTS350search
	Version           : :3.5,3.51,4.0
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
