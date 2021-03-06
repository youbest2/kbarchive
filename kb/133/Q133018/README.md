---
layout: page
title: "Q133018: INFO: Visual SourceSafe Setup Registration Settings"
permalink: /kb/133/Q133018/
---

## Q133018: INFO: Visual SourceSafe Setup Registration Settings

{% raw %}

	Article: Q133018
	Product(s): Microsoft SourceSafe
	Version(s): 4.0,5.0
	Operating System(s): 
	Keyword(s): kbsetup kbSSafe
	Last Modified: 03-JUN-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual SourceSafe for Windows, versions 4.0, 5.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	NOTE: All references to WIN.INI and 16-bit installs relate only to Visual
	SourceSafe 4.x. Version 5.0 is 32-bit only.
	
	For Visual SourceSafe 4.0 to work correctly with Visual Basic and Visual C++, it
	needs to make modifications to the Registry, WIN.INI (16-bit only), and VB.INI.
	These modifications occur during a Client install, Custom install (SETUP.EXE),
	or a Network Client install (NETSETUP.EXE). The Network Client install is only
	available after a Server install has been performed.
	
	MORE INFORMATION
	================
	
	This is what the Client setup script does to register the SourceSafe Visual
	Basic Add-In and SCC DLL.
	
	
	Registration Database Keys
	--------------------------
	
	These entries are created during 32-bit and 16-bit installations. In the
	description below, {%INSTALLDIRECTORY%} is replaced with the path to the DLL.
	For example, if you are installing into C:\SS4, then {%INSTALLDIRECTORY%} is
	replaced with C:\SS4\WIN32 on 32-bit systems and C:\SS4\WIN on 16-bit systems.
	
	     HKEY_CLASSES_ROOT\SccAddIn.SourceCodeControlAddIn = Source Code Control
	        Add-In
	     HKEY_CLASSES_ROOT\SccAddIn.SourceCodeControlAddIn\Clsid = {2F998FDA-
	        3487-11CE-BCB6-00AA00688899}
	
	     HKEY_CLASSES_ROOT\SccAddIn.SourceCodeControlAddIn.1 = Source Code
	        Control Add-In
	     HKEY_CLASSES_ROOT\SccAddIn.SourceCodeControlAddIn.1\Clsid = {2F998FDA-
	        3487-11CE-BCB6-00AA00688899}
	
	     HKEY_CLASSES_ROOT\CLSID\{2F998FDA-3487-11CE-BCB6-00AA00688899} = Source
	        Code Control Add-In
	     HKEY_CLASSES_ROOT\CLSID\{2F998FDA-3487-11CE-BCB6-00AA00688899}\ProgID =
	        SccAddIn.SourceCodeControlAddIn.1
	     HKEY_CLASSES_ROOT\CLSID\{2F998FDA-3487-11CE-BCB6-00AA00688899}\ 
	        VersionIndependentProgID = SccAddIn.SourceCodeControlAddIn
	     HKEY_CLASSES_ROOT\CLSID\{2F998FDA-3487-11CE-BCB6-00AA00688899}\ 
	        InProcServer32 = {%INSTALLDIRECTORY%}Ssvb.dll
	     HKEY_CLASSES_ROOT\CLSID\{2F998FDA-3487-11CE-BCB6-00AA00688899}\ 
	        InProcServer = {%INSTALLDIRECTORY%}Ssvb16.dll
	
	The following registry entries are created on 32-bit installations only:
	
	     HKEY_LOCAL_MACHINE\Software\SourceCodeControlProvider = Value:
	        ProviderRegKey = Software\Microsoft\SourceSafe
	     HKEY_LOCAL_MACHINE\Software\Microsoft\SourceSafe = Value: SCCServerPath
	        = {%INSTALLDIRECTORY%}ssscc.dll
	     HKEY_LOCAL_MACHINE\Software\Microsoft\SourceSafe = Value: SCCServerName
	        = Microsoft Visual SourceSafe
	
	WIN.INI File Modifications
	--------------------------
	
	These changes are made during on 16-bit installation only. {%INSTALLDIRECTORY%}
	is replaced with the path to the DLL:
	
	     [Source Code Control]
	     SourceCodeControlProvider = SourceSafeSCCServer
	     [SourceSafeSCCServer]
	     SCCServerPath = {%INSTALLDIRECTORY%}ssscc16.dll
	     SCCServerName = Microsoft Visual SourceSafe
	
	VB.INI Entries
	--------------
	
	These entries are made during 16-bit and 32-bit installs. SourceSafe Setup
	determines the location of VB.INI by:
	
	1. Looking in the registry to figure out where the registered version of Visual
	  Basic is.
	
	2. Asking the user.
	
	     [Add-Ins32]
	     SccAddIn.SourceCodeControlAddIn=1
	
	     [Add-Ins16]
	     SccAddIn.SourceCodeControlAddIn=1
	
	
	Additional query words: install
	
	======================================================================
	Keywords          : kbsetup kbSSafe 
	Technology        : kbSSafeSearch kbAudDeveloper kbSSafe400 kbSSafe500
	Version           : :4.0,5.0
	Issue type        : kbinfo
	
	=============================================================================
	

{% endraw %}
