---
layout: page
title: "Q126972: Control Panel &quot;Don't Load&quot; Feature Does Not Work"
permalink: /kb/126/Q126972/
---

## Q126972: Control Panel &quot;Don't Load&quot; Feature Does Not Work

{% raw %}

	Article: Q126972
	Product(s): Microsoft Windows NT
	Version(s): 3.1 3.5 3.51
	Operating System(s): 
	Keyword(s): kbusage
	Last Modified: 08-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Server version 3.1 
	- Microsoft Windows NT Workstation version 3.1 
	- Microsoft Windows NT Advanced Server, version 3.1 
	- Microsoft Windows NT Workstation versions 3.5, 3.51 
	- Microsoft Windows NT Server versions 3.5, 3.51 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	You can prevent individual Control Panel components from loading under Windows
	NT versions 3.1 and 3.5 by modifying the Registry. However, this does not work
	in Windows NT version 3.5. For example, if you modify the Registry to specify
	that the Control Panel Keyboard component should not load, the component still
	loads.
	
	CAUSE
	=====
	
	In Windows NT version 3.5, a cache mechanism is implemented to speed up the
	loading of Control Panel components. When you run Control Panel for the first
	time, a cache is created that includes information regarding each component in
	the Control Panel. Therefore, Registry entries specifying certain components not
	to load are not read in Windows NT version 3.5.
	
	WORKAROUND
	==========
	
	To work around this problem, add the /CACHE switch to the Control Panel Command
	Line in the Program Manager Program Item Properties dialog box after you modify
	the Registry. For example:
	
	  CONTROL.EXE /cache
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Windows NT version 3.5. We are
	researching this problem and will post new information here in the Microsoft
	Knowledge Base as it becomes available.
	
	MORE INFORMATION
	================
	
	You can use the following procedure to prevent Control Panel components from
	loading.
	
	  WARNING: Using Registry Editor incorrectly can cause serious, system-wide
	  problems that may require you to reinstall Windows NT to correct them.
	  Microsoft cannot guarantee that any problems resulting from the use of
	  Registry Editor can be solved. Use this tool at your own risk.
	
	1. Run Registry Editor (REGEDT32.EXE).
	
	2. From the HKEY_CURRENT_USER subtree, go to the following key:
	
	  \Control Panel
	
	3. From the Edit menu, choose Add Key.
	
	4. Type "Don't Load" (without the quotation marks) in the Key Name text box and
	  choose OK.
	
	5. Select Don't Load.
	
	6. From the Edit menu, choose Add Value.
	
	7. Type the following in the appropriate text boxes:
	
	     Value Name:  <Control Panel component>
	     Data Type:   REG_SZ
	     String:      0 or 1 (Either string value will prevent the
	                          Control component from loading)
	
	  The default Control Panel component names are:
	
	     Color          International          Desktop
	     Fonts          System                 Keyboard
	     Ports          Date/Time              Printers
	     Mouse          Network                Devices
	     Drivers        Sound                  Cursors
	     Server         Services               UPS
	     Display (Windows NT version 3.5 only)
	     MIDI Mapper (Windows NT version 3.1 only)
	
	8. Quit Registry Editor and restart Control Panel.
	
	NOTE: If you need to modify the Registry again to prevent additional Control
	Panel components from loading, do not repeat steps three and four.
	
	Additional query words: prodnt main cpl nkbd
	
	======================================================================
	Keywords          : kbusage 
	Technology        : kbWinNTsearch kbWinNTWsearch kbWinNT351search kbWinNT350search kbWinNTW350 kbWinNTW350search kbWinNTW351search kbWinNTW351 kbWinNTW310 kbWinNTSsearch kbWinNTS351 kbWinNTS350 kbWinNTS310 kbWinNTAdvSerSearch kbWinNTAdvServ310 kbWinNTS351search kbWinNTS350search kbWinNTS310search kbWinNT310Search kbWinNTW310Search
	Version           : 3.1 3.5 3.51
	
	=============================================================================
	

{% endraw %}
