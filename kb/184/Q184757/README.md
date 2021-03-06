---
layout: page
title: "Q184757: Programs on Pan-Chinese Windows NT May Use Fixed Font for Menus"
permalink: /kb/184/Q184757/
---

## Q184757: Programs on Pan-Chinese Windows NT May Use Fixed Font for Menus

{% raw %}

	Article: Q184757
	Product(s): Microsoft Windows NT
	Version(s): 4.0
	Operating System(s): 
	Keyword(s): kbenv kbui
	Last Modified: 09-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Server version 4.0 
	- Microsoft Windows NT Workstation version 4.0 
	- Microsoft Windows NT Server, Enterprise Edition version 4.0 
	-------------------------------------------------------------------------------
	
	
	SYMPTOMS
	========
	
	Programs installed on the Pan Chinese localized (foreign language) version of
	Windows NT may not use the proper font (typically the Tahoma font) for their
	menus. Instead, the program's menus may use a non-proportional font that looks
	like Courier rather than a proportional font similar to Arial. This may cause
	the menus to be truncated or not visible in some programs, making them difficult
	or impossible to use.
	
	CAUSE
	=====
	
	This problem can occur if the charset is set to 86 (GB2312). Because of this,
	CreateFontIndirect() returns the SimSun font as the closest match for the
	requested Tahoma font.
	
	RESOLUTION
	==========
	
	To resolve this problem, contact Microsoft Technical Support to obtain the
	following fix, or wait for the next Windows NT service pack.
	
	This fix should have the following time stamp or later:
	
	+------------------------------------------------------+
	| Imm32.dll  | 94,992    | 03/04/98 | 05:07p | (Intel) | 
	+------------------------------------------------------+
	| User32.dll | 346,384   | 03/04/98 | 05:07p | (Intel) | 
	+------------------------------------------------------+
	| Win32k.sys | 1,307,376 | 04/20/98 | 08:35p | (Intel) | 
	+------------------------------------------------------+
	| Winsrv.dll | 251,152   | 03/04/98 | 05:04p | (Intel) | 
	+------------------------------------------------------+
	
	+------------------------------------------------------+
	| Imm32.dll  | 171,792   | 03/04/98 | 05:08p | (Alpha) | 
	+------------------------------------------------------+
	| User32.dll | 623,888   | 03/04/98 | 05:08p | (Alpha) | 
	+------------------------------------------------------+
	| Win32k.sys | 2,173,776 | 04/20/98 | 08:34p | (Alpha) | 
	+------------------------------------------------------+
	| Winsrv.dll | 450,832   | 03/04/98 | 05:05p | (Alpha) | 
	+------------------------------------------------------+
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Windows NT version 4.0.
	
	
	A supported fix is now available, but has not been fully regression tested and
	should be applied only to computers experiencing this specific problem. Unless
	you are severely impacted by this specific problem, Microsoft recommends that
	you wait for the next service pack that contains this fix. Contact Microsoft
	Technical Support for more information.
	
	
	Additional query words:
	
	======================================================================
	Keywords          : kbenv kbui 
	Technology        : kbWinNTsearch kbWinNTWsearch kbWinNTW400 kbWinNTW400search kbWinNT400search kbWinNTSsearch kbWinNTSEntSearch kbWinNTSEnt400 kbWinNTS400search kbWinNTS400
	Version           : :4.0
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
