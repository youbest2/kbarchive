---
layout: page
title: "Q214600: Encarta Ref Suite 99 Err Msg: Please Insert the Disk Labeled..."
permalink: /kb/214/Q214600/
---

## Q214600: Encarta Ref Suite 99 Err Msg: Please Insert the Disk Labeled...

{% raw %}

	Article: Q214600
	Product(s): Microsoft Home Multimedia Titles
	Version(s): WINDOWS:
	Operating System(s): 
	Keyword(s): kbenv kberrmsg kbsetup kbimu
	Last Modified: 31-JUL-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Encarta Reference Suite 99 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	The following error message may appear when you try to run one or more of the
	installation programs listed below.
	
	  Please insert the disk labeled <diskname>.
	
	  The disk labeled '<diskname>' is now required. The disk is provided by
	  your computer manufacturer. Click OK to continue.
	
	When you click OK, you receive the following error message:
	
	  The file '<filename>' on the <diskname> disk cannot be found.
	  Insert <diskname> in the selected drive, and click OK.
	
	Where <diskname> and <filename> are one of the value pairs listed in
	the following table:
	
	  <diskname>                            <filename>
	  --------------------------------------------------
	
	  DLL Installations                     Axdist.exe
	  DCOM95 for Windows 95                 Dcom95.exe
	  Microsoft Speech Recognition Engine   mscsrgpc.exe
	  Microsoft Text-to-Speech Engine       msttsf16.exe
	  Mtstool                               Mtstool.exe
	  Refshoot                              Reftst99.exe
	  Microsoft Speech API 4.0              Spchapi.exe
	  Setup                                 Speu.exe
	  Shockwave Files                       Sw61inst.exe
	
	CAUSE
	=====
	
	This behavior can occur if the Internet Express (IExpress) installation files on
	your computer are missing or damaged.
	
	RESOLUTION
	==========
	
	To resolve this issue, manually extract the files from the installation program
	to a new folder, and then run the installation script in that folder. To do
	this, follow these steps:
	
	1. Click Start, point to Find, and then click Files Or Folders.
	
	2. In the Named box, type the name of the installation program that causes the
	  problem, and then click Find Now.
	
	  NOTE: You may need to search for the file on the program CD-ROM.
	
	3. In the list of found files, right-click and drag the installation program to
	  the desktop, and then click Create Shortcut.
	
	4. On the desktop, right-click the shortcut to the installation program, and
	  then click Properties.
	
	5. On the Shortcut tab, click the Target box, press the END key, press the
	  SPACEBAR, type "/c" (without the quotation marks), and then click OK.
	
	6. On the desktop, double-click the shortcut to the installation program.
	
	7. If you are prompted to agree to an End User License Agreement, click I Agree.
	
	8. In the "Please type the location where you want to place the extracted files"
	  box, type "c:\junk" (without the quotation marks), and then click OK.
	
	9. Click Start, and then click Run.
	
	10. In the Open box, type "c:\junk" (without the quotation marks), and then
	  click OK.
	
	11. Right-click the <filename>.inf file, and then click Install, where
	  <filename> is the name of the installation program that causes the
	  problem.
	
	12. Follow the instructions on the screen to install the program.
	
	
	Additional query words: kbimu multi multi-media media mm
	
	======================================================================
	Keywords          : kbenv kberrmsg kbsetup kbimu 
	Technology        : kbHomeProdSearch kbHomeMMsearch kbEncartaSearch kbEncartaReference99
	Version           : WINDOWS:
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
