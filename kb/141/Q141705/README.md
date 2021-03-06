---
layout: page
title: "Q141705: How to Set Up Directory Annotation for Internet Server FTP"
permalink: /kb/141/Q141705/
---

## Q141705: How to Set Up Directory Annotation for Internet Server FTP

{% raw %}

	Article: Q141705
	Product(s): Internet Information Server
	Version(s): winnt:1.0,2.0,3.0,4.0
	Operating System(s): 
	Keyword(s): 
	Last Modified: 11-JUN-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Internet Information Server versions 1.0, 2.0, 3.0, 4.0 
	-------------------------------------------------------------------------------
	
	IMPORTANT: This article contains information about modifying the registry. Before you modify the registry, make sure to back it up and make sure that you understand how to restore the registry if a problem occurs. For information about how to back up, restore, and edit the registry, click the following article number to view the article in the Microsoft Knowledge Base:
	
	  Q256986 Description of the Microsoft Windows Registry
	
	SUMMARY
	=======
	
	This article describes how to add directory descriptions to inform FTP users of
	the contents of directories on the server.
	
	To annotate files, do the following:
	
	1. Create a file called ~ftpsvc~.ckm in the directory where you want to annotate
	  with the information to be displayed to the user.
	
	2. In Windows NT File Manager, select the file and make it a hidden file so that
	  directory listings do not display this file.
	
	NOTE: This only works with the command line FTP on one line. If you are using
	Microsoft Internet Explorer for FTP, and using directory annotation, Internet
	Explorer will give you the following error message:
	
	  Internet explorer could not open site address
	
	Netscape browser does not give an error; however, it still does not work. This is
	a client or browser problem.
	
	MORE INFORMATION
	================
	
	Directory annotation can be toggled by FTP users on a user-by-user basis with a
	built-in, site-specific command called ckm. This varies depending on the FTP
	client used. For a Microsoft FTP client, the command "literal SITE CKM" toggles
	annotations for the FTP client on or off.
	
	To change the FTP Server service configuration in the registry, do the
	following:
	
	WARNING: If you use Registry Editor incorrectly, you may cause serious problems
	that may require you to reinstall your operating system. Microsoft cannot
	guarantee that you can solve problems that result from using Registry Editor
	incorrectly. Use Registry Editor at your own risk.
	
	1. Run Registry Editor (Regedt32.exe).
	
	2. From the HKEY_LOCAL_MACHINE subtree, go to the following key:
	  SYSTEM\CurrentControlSet\Services\msftpsvc\Parameters
	
	3. Add the entry: AnnotateDirectories Data type = REG_DWORD Range = 0 or 1
	  (default = 0) 0, false - directory annotation is off 1, true - directory
	  annotation is on The value, AnnotateDirectories, does not appear by default
	  in the registry, so you must add an entry if you want to change its default
	  value.
	
	4. Set this value is 1 to enable directory annotation.
	
	5. Choose OK and quit Registry Editor.
	
	6. Shut down and restart Windows NT.
	
	Additional query words:
	
	======================================================================
	Keywords          :  
	Technology        : kbiisSearch kbiis400 kbiis300 kbiis200 kbiis100
	Version           : winnt:1.0,2.0,3.0,4.0
	
	=============================================================================
	

{% endraw %}
