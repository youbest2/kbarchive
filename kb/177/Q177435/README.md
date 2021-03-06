---
layout: page
title: "Q177435: PRB: Resolving DEVBCPX: Required file cannot be loaded Error"
permalink: /kb/177/Q177435/
---

## Q177435: PRB: Resolving DEVBCPX: Required file cannot be loaded Error

{% raw %}

	Article: Q177435
	Product(s): Microsoft C Compiler
	Version(s): 5.0,6.0
	Operating System(s): 
	Keyword(s): kberrmsg kbVC500 kbVC600 kbGrpDSTools
	Last Modified: 18-JUN-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual C++, 32-bit Enterprise Edition, versions 5.0, 6.0 
	- Microsoft Visual C++, 32-bit Professional Edition, versions 5.0, 6.0 
	- Microsoft Visual C++, 32-bit Learning Edition, version 6.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When starting Microsoft Developer Studio, the following error is displayed:
	
	  DEVBCPX - This required file cannot be loaded. Please re-install Microsoft
	  Developer Studio"
	
	This error may be generated if you have a dual-boot machine and Numega's Bounds
	Checker is installed. Even if Developer Studio is reinstalled, the error still
	occurs.
	
	NOTE: The same error occurs when Bounds Checker is uninstalled.
	
	CAUSE
	=====
	
	This error occurs if Developer Studio cannot load the Devbcpx.pkg file. This
	file is installed by Numega's software package BoundsChecker, which is
	integrated with Developer Studio. This error is generated if you have a
	dual-boot machine for Microsoft Windows NT version 4.0 and Microsoft Windows 95,
	and BoundsChecker is installed in only one operating system and Visual C++
	Developer Studio is installed on both the operating systems in a common folder
	on the hard drive. The file Devbcpx.pkg is installed in the
	DevStudio\SharedIDE\Bin\Ide folder. When starting Developer Studio, Msdev.exe
	tries to locate the Devbcpx.pkg file through the registry entry and if
	BoundsChecker is not installed for the operating system in which the machine is
	booted, the error occurs.
	
	RESOLUTION
	==========
	
	You can use one of the following options to resolve this problem depending on
	your requirements.
	
	Option 1
	--------
	
	Use this option if you are using a dual-boot machine and you want to use both
	Visual C++ Developer Studio and BoundsChecker, and you are getting this error
	when you try to use Developer Studio in only one of the operating systems.
	
	The resolution for the above configuration is to install BoundsChecker also for
	the operating system where the error has occurred.
	
	Option 2
	--------
	
	Use this option if you are the only user of the machine and you have no intention
	of using BoundsChecker.
	
	The resolution is to uninstall Visual C++, and verify the following information.
	
	For Visual C++, version 5.0:
	
	  Verify that the the directories DevStudio\SharedIDE\Bin and DevStudio\Vc\Bin
	  are empty. Also, ensure that the following registry keys are deleted if you
	  find them:
	
	     HKEY_CURRENT_USER\Software\Microsoft\DevStudio
	     HKEY_CURRENT_USER\Software\Microsoft\Infoviewer\5.0
	     HKEY_LOCAL_MACHINE\Software\Microsoft\DevStudio
	     HKEY_LOCAL_MACHINE\Software\Microsoft\Infoviewer\5.0
	
	For Visual C++, version 6.0:
	
	  Verify that the directories [Visual Studio Path]\Common\MSDEV98\Bin and
	  [Visual Studio Path]\VC98\Bin are empty. Also, ensure that the following
	  registry keys are deleted if you find them:
	
	     HKEY_CURRENT_USER\Software\Microsoft\DevStudio\6.0
	     HKEY_LOCAL_MACHINE\Software\Microsoft\DevStudio\6.0
	
	Then reinstall Visual C++. If you installed the MSDN Library before, it is
	advisable that you reinstall the MSDN Library also after reinstalling Visual
	C++.
	
	STATUS
	======
	
	This behavior is by design.
	
	Additional query words:
	
	======================================================================
	Keywords          : kberrmsg kbVC500 kbVC600 kbGrpDSTools 
	Technology        : kbVCsearch kbAudDeveloper kbVC500 kbVC600 kbVC32bitSearch kbVC500Search
	Version           : :5.0,6.0
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
