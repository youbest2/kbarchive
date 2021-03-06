---
layout: page
title: "Q84575: Windows 3.1: Troubleshooting Creating a Permanent Swap File"
permalink: /kb/084/Q84575/
---

## Q84575: Windows 3.1: Troubleshooting Creating a Permanent Swap File

{% raw %}

	Article: Q84575
	Product(s): Microsoft Windows 95.x Retail Product
	Version(s): WINDOWS:3.1,3.11
	Operating System(s): 
	Keyword(s): 
	Last Modified: 01-OCT-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows versions 3.1, 3.11 
	- Microsoft Windows for Workgroups versions 3.1, 3.11 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	Some third-party video drivers (S3 drivers obtained from Orchid Technologies)
	can prevent Microsoft Windows from setting up a permanent swap file.
	
	Orchid has corrected these problems and provides an upgraded BIOS and driver. The
	new BIOS is version 3.0 and the new driver is version 7.0
	
	To obtain the phone numbers for Orchid, query on the following words here in the
	Microsoft Knowledge Base:
	
	  Orchid and phonebook and pss
	
	If you cannot set up a permanent swap file and are using a third-party video
	driver, try changing back to the standard Windows VGA of Super VGA (800x600, 16
	color) video driver.
	
	MORE INFORMATION
	================
	
	The following is a list of other problems and solutions you may encounter when
	attempting to set up a permanent swap file:
	
	  Problem                  Solution
	  -------                  --------
	
	  Windows suggests very    Run a disk optimization utility to
	  small swap file size.    defragment the disk drive.
	
	  Incompatible third-      Contact your device driver vendor for
	  party device drivers.    an update. You must have 512-byte sectors
	                           to create a permanent swap file.
	
	  Incompatible security    Disable software or device drivers and
	  software or device       change swap file settings.
	  drivers.
	
	  Permanent swap file      Check the SYSTEM.INI file for the following:
	  size is not added to        Paging=Off
	  physical RAM             -or-
	  statement.                  Paging=False
	                           If found, remark it out with a semicolon
	                           (;), restart Windows.
	
	KBCategory: kb3rdparty kbdisplay kbtshoot
	KBSubcategory: windrvr win31 wfw wfwg
	
	Additional query words: 3.10 3.11 tshoot virtual memory 3rdparty
	
	======================================================================
	Keywords          :  
	Technology        : kbAudDeveloper kbWin3xSearch kbWFWSearch kbZNotKeyword3 kbWin310 kbWin311 kbWFW310 kbWFW311
	Version           : WINDOWS:3.1,3.11
	
	=============================================================================
	

{% endraw %}
