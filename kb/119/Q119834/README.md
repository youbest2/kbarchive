---
layout: page
title: "Q119834: LAN Manager as the Network with Windows for Workgroups 3.11"
permalink: /kb/119/Q119834/
---

## Q119834: LAN Manager as the Network with Windows for Workgroups 3.11

{% raw %}

	Article: Q119834
	Product(s): Windows for Workgroups and Windows NT Networking Issues
	Version(s): 3.11
	Operating System(s): 
	Keyword(s): 
	Last Modified: 17-DEC-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows for Workgroups version 3.11 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	When you install Windows for Workgroups over Microsoft LAN Manager, Setup
	assumes you are upgrading your network operating system. It assumes that you
	will not be using LAN Manager as your network, but will instead be using the
	Microsoft Windows Network, or one of the other supported networks listed during
	installation.
	
	This article describes how to configure your workstation to use Windows for
	Workgroups with LAN Manager as the only network operating system.
	
	
	MORE INFORMATION
	================
	
	After you install Windows for Workgroups on top of LAN Manager and select "No
	Windows support for networks," the following error message may appear when you
	start Windows:
	
	  Cannot find a device file that may be needed to run Windows.
	
	  Make sure that the PATH line in your AUTOEXEC.BAT file points to the directory
	  that contains the file and that it exists on your hard disk. If the file does
	  not exist, try running Setup to install it or remove any referenced to it
	  from your SYSTEM.INI file. ee16.386 (This line varies, depending on your
	  network card.)
	
	The AUTOEXEC.BAT, CONFIG.SYS, and SYSTEM.INI files need to be modified to make
	Windows for Workgroups function properly with LAN Manager.
	
	Setup saved your old CONFIG.SYS file as CONFIG.OLD and your old AUTOEXEC.BAT file
	as AUTOEXEC.OLD. Copy the lines specific to LAN Manager from the .OLD files and
	combine them with the lines needed for Windows.
	
	NOTE: If you had an existing AUTOEXEC.OLD or CONFIG.OLD, it will rename the files
	CONFIG.001 and AUTOEXEC.001
	
	Example AUTOEXEC.BAT for Windows for Workgroups with LAN Manager:
	
	  @ECHO OFF
	  PROMPT $p$g
	  C:\WINDOWS\SMARTDRV.EXE
	  PATH C:\WINDOWS;C:\DOS
	  SET TEMP=C:\DOS
	  C:\DOS\DOSKEY
	  @REM ==== LANMAN 2.2 === DO NOT MODIFY BETWEEN THESE LINES ===
	  LANMAN 2.2 ====
	  SET PATH=C:\LANMAN.DOS\NETPROG;%PATH%
	  NET START WORKSTATION
	  LOAD NETBEUI
	  @REM ==== LANMAN 2.2 === DO NOT MODIFY BETWEEN THESE LINES ===
	  LANMAN 2.2 ====
	  WIN
	
	Example CONFIG.SYS for Windows for Workgroups with LAN Manager:
	
	(Notice that the line DEVICE=C:\WINDOWS\IFSHLP.SYS has been removed that Windows
	for Workgroups Setup usually inserts.)
	
	  DEVICE=C:\DOS\SETVER.EXE
	  DEVICE=C:\WINDOWS\HIMEM.SYS
	  DOS=HIGH
	  FILES=30
	  SHELL=C:\DOS\COMMAND.COM C:\DOS\ /p
	  LASTDRIVE=Z
	  STACKS=9,256
	  DEVICE=C:\LANMAN.DOS\DRIVERS\PROTMAN\PROTMAN.DOS /i:C:\LANMAN.DOS
	  DEVICE=C:\LANMAN.DOS\DRIVERS\ETHERNET\EXP16\EXP16.DOS
	
	Delete the SYSTEM.INI in the Windows directory.
	
	Modify the following lines:
	
	  [boot]
	  network.drv=LANMAN21.DRV   (Add LANMAN21.DRV)
	  [386Enh]
	  netcard=                   (You may need to remove a reference
	                              to the network card, such as ee16.386.)
	  transport=                 (You may need to remove a reference
	                              to the protocol used, such as netbeui.386.)
	
	The PROTOCOL.INI in the LANMAN.DOS directory should remain unchanged from a
	regular LAN Manager workstation. The PROTOCOL.INI in the Windows directory
	should contain only the following lines:
	
	  [network.setup]
	  version=0x3110
	
	NOTE: If you plan on using WinPopup, make sure that you run WINPOPUP.EXE from the
	LANMAN.DOS\NETPROG directory, not the one that may be in the Windows directory.
	
	Additional query words: wfw wfwg 3.11 2.2 2.1
	
	======================================================================
	Keywords          :  
	Technology        : kbAudDeveloper kbWFWSearch kbWFW311
	Version           : 3.11
	
	=============================================================================
	

{% endraw %}
