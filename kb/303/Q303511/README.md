---
layout: page
title: "Q303511: STREETS: Err Msg: Setup Cannot Find the MDAC Directory"
permalink: /kb/303/Q303511/
---

## Q303511: STREETS: Err Msg: Setup Cannot Find the MDAC Directory

{% raw %}

	Article: Q303511
	Product(s): Microsoft Automap
	Version(s): 1.0,3.1,3.5,3.51,3.51 SP5,4.0,4.0 SP1,4.0 SP2,4.0 SP3,4.0 SP4,4.0 SP5,4.0 SP6,4.0 SP6a
	Operating System(s): 
	Keyword(s): kberrmsg kbimu
	Last Modified: 06-AUG-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Streets and Trips 2001 
	- Microsoft MapPoint 2000 
	- Microsoft MapPoint 2001 
	- Microsoft MapPoint 2002 
	- Microsoft Streets & Trips 2002, version 1.0 
	- the operating system: Microsoft Windows NT, versions 3.1, 3.5, 3.51, 3.51 SP5, 4.0, 4.0 SP1, 4.0 SP2, 4.0 SP3, 4.0 SP4, 4.0 SP5, 4.0 SP6, 4.0 SP6a 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When you attempt to install one of the Microsoft programs listed in the "Applies
	to" section of this article, you may receive the following error message:
	
	  Setup cannot find the MDAC directory
	
	CAUSE
	=====
	
	This behavior can occur if you are attempting to install one of these programs
	on a Microsoft Windows NT 4.0-based computer. This behavior occurs if the
	Microsoft Data Access Components (MDAC) are not installed correctly.
	
	RESOLUTION
	==========
	
	To resolve this issue, install MDAC from the Microsoft MapPoint or Microsoft
	Streets & Trips CD-ROM, and then re-run the installation of the program.
	
	To do this, follow these steps:
	
	1. Insert disc 1 of the program's CD-ROM package, and then press the SHIFT key
	  to prevent program installation from starting automatically.
	
	2. Double-click My Computer on the desktop, and then double-click the CD-ROM or
	  DVD-ROM drive icon to start Windows Explorer.
	
	3. Locate, and then double-click, the MDAC_TYP.EXE file to install MDAC.
	
	  The file can be found in one of the following folders, depending on the
	  program:
	
	   - For 2002 versions:
	
	     <CD-ROM drive letter>:\SUPPORT\MDAC
	
	   - For 2001 versions:
	
	     <CD-ROM drive letter>:\MSMAP\REDIST\MDAC
	
	   - For 2000 versions:
	
	     <CD-ROM drive letter>:\COMMON\ENU
	
	4. Follow the instructions to install MDAC, and then restart your computer when
	  installation is completed.
	
	5. Insert disc 1 of the program's CD-ROM package, and then follow the
	  instructions to install the program.
	
	Additional query words:
	
	======================================================================
	Keywords          : kberrmsg kbimu 
	Technology        : kbOSWinSearch kbHomeProdSearch _IKkbbogus kbOSWinNT310 kbOSWinNT350 kbOSWinNT400 kbOSWinNT351 kbExpediaSearch kbMapptSearch kbMapPoint2000 kbMapPoint2001 kbOSWinNTSearch kbExpediaStreets2001 kbOSWinNT400SP6a kbOSWinNT400SP6 kbOSWinNT400SP4 kbOSWinNT400SP3 kbOSWinNT400SP2 kbOSWinNT400SP1 kbOSWinNT351SP5 kbOSWinNT400SP5 kbExpediaStreets2002 kbMapPoint2002
	Version           : :1.0,3.1,3.5,3.51,3.51 SP5,4.0,4.0 SP1,4.0 SP2,4.0 SP3,4.0 SP4,4.0 SP5,4.0 SP6,4.0 SP6a
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
