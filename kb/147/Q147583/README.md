---
layout: page
title: "Q147583: BUG: Adding Multiple Files w/16-Bit SetupWiz Fails on Win95/98"
permalink: /kb/147/Q147583/
---

## Q147583: BUG: Adding Multiple Files w/16-Bit SetupWiz Fails on Win95/98

{% raw %}

	Article: Q147583
	Product(s): Microsoft Visual Basic for Windows
	Version(s): WINDOWS:4.0,95,98
	Operating System(s): 
	Keyword(s): kbsetup kb16bitonly kbwizard kbDSSTools kbVBp400bug kbGrpDSVB kbDSupport
	Last Modified: 13-JAN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual Basic Professional Edition for Windows, version 4.0 
	- Microsoft Visual Basic Enterprise Edition for Windows, version 4.0 
	- Microsoft Windows 95 
	- Microsoft Windows 98 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	Attempting to add more than one file in step 7 of the Visual Basic 4.0 Setup
	Wizard fails. After selecting multiple files and clicking OK, the Setup Wizard
	displays a dialog containing "This file may be required for your program to run
	correctly" and prompts if a search for this file should be continued. If the
	search is terminated, a dialog displays "The file(s) you selected were already
	in the list. No new files have been added."
	
	CAUSE
	=====
	
	The Setup Wizard attempts to look for a single file with a filename that is the
	concatenation of all the files selected. This problem only occurs with the
	16-bit version of the Microsoft Visual Basic 4.0 Setup Wizard for Windows when
	run on Microsoft Windows 95 or Windows 98. It does not occur on Microsoft
	Windows NT version 3.51 or on any 16-bit Microsoft Windows operating system.
	This problem does not occur using the 32-bit version of the Microsoft Visual
	Basic 4.0 Setup Wizard for Windows.
	
	RESOLUTION
	==========
	
	Use any one of the following methods to work around this problem:
	
	- Add each file one at a time.
	
	- Create setup media or a template (.Vbz) file for the setup using an operating
	  system other than Microsoft Windows 95. If a template is created on another
	  machine, then the .Vbz file can be copied to the Microsoft Windows 95 or
	  Windows 98 machine and selected in Step 1 of the Setup Wizard using the Load
	  Template button.
	
	- Add files manually to a template file generated on the Windows 95 or Windows
	  98 machine. In step 7, click Save Template and save a template (.Vbz) file to
	  disk. Open this template file in a text editor and manually add a line for
	  each file that you want to add. Listed below are some sample added FileXX
	  lines, just replace the first parameter with the path to the file you wish to
	  include:
	
	     File17=C:\ENROLL\ENROLL.ICO,0,$(AppPath),,|32760|,-1,0,0,0,,,0
	     File18=C:\ENROLL\MSTRS.EXE,0,$(AppPath),,|32760|,-1,0,0,0,,,0
	     File19=C:\ENROLL\README.HLP,0,$(AppPath),,|32760|,-1,0,0,0,,,0
	     File20=C:\ENROLL\TRAIN.HLP,0,$(AppPath),,|32760|,-1,0,0,0,,,0
	
	  Then restart the Setup Wizard and click Open Template to load the modified
	  template file.
	
	STATUS
	======
	
	Microsoft has confirmed this to be an issue in the Microsoft products listed at
	the beginning of this article. We will post new information about this issue
	here in the Microsoft Knowledge Base as it becomes available.
	
	MORE INFORMATION
	================
	
	Steps To Reproduce Problem
	--------------------------
	
	1. Start the 16-bit version of the Visual Basic 4.0 Setup Wizard for Windows.
	
	2. In step 1, select the .Vbp file for the Calc sample (located in the
	  Vb\Samples\Calc directory).
	
	3. Click Next repeatedly until you reach step 7.
	
	4. Click "Add Files..." and select more than one file in the common dialog box
	  that appears. The previously mentioned dialog boxes appear after you click OK
	  to dismiss the dialog box.
	
	Additional query words:
	
	======================================================================
	Keywords          : kbsetup kb16bitonly kbwizard kbDSSTools kbVBp400bug kbGrpDSVB kbDSupport 
	Technology        : kbVBSearch kbAudDeveloper kbWin95search kbWin98search kbZNotKeyword6 kbZNotKeyword2 kbVB400Search kbVB400 kbZNotKeyword3 kbWin98
	Version           : WINDOWS:4.0,95,98
	Issue type        : kbbug
	Solution Type     : kbpending
	
	=============================================================================
	

{% endraw %}
