---
layout: page
title: "Q97737: Running Windows for Workgroups on a DEC Pathworks Network"
permalink: /kb/097/Q97737/
---

## Q97737: Running Windows for Workgroups on a DEC Pathworks Network

{% raw %}

	Article: Q97737
	Product(s): Microsoft Windows 3.x Retail Product
	Version(s): WINDOWS:
	Operating System(s): 
	Keyword(s): 
	Last Modified: 25-SEP-1999
	
	3.10 3.11
	WINDOWS
	kbnetwork kbsetup kb3rdparty kbfasttip kbpolicy
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows for Workgroups 
	-------------------------------------------------------------------------------
	
	
	This article contains information about using Windows for Workgroups
	with third-party products or configurations that have not been tested
	and are not supported by Microsoft.
	
	If the steps described in this article do not function properly, use
	a supported configuration or contact the manufacturer of your
	third-party product for more information.
	
	SUMMARY
	=======
	
	Although Digital Equipment Corporation (DEC) Pathworks has not been tested with
	Windows for Workgroups and its use is not supported with Windows for Workgroups,
	you can integrate the two networks following the appropriate procedure in this
	article.
	
	Please note that separate procedures are provided for Windows for Workgroups 3.11
	and Windows for Workgroups 3.1.
	
	MORE INFORMATION
	================
	
	WINDOWS FOR WORKGROUPS 3.11 PROCEDURE
	=====================================
	
	To properly set up Windows for Workgroups version 3.11 with DEC
	Pathworks, do the following:
	
	1. Get DEC Pathworks version 4.0 or later running at the MS-DOS level.
	
	2. Obtain the file DECNB.386 from DEC.
	
	3. Install Windows for Workgroups 3.11
	
	4. Select DEC Pathworks under the "Install Windows support for the
	  following network only" option.
	
	  NOTE: There are two options for DEC Pathworks: Version 4.0 and
	  Version 4.1 and later. Be sure to select the correct option.
	
	WINDOWS FOR WORKGROUPS 3.1 PROCEDURE
	====================================
	
	The procedure below describes the steps necessary to enable the
	Windows for Workgroups 3.1 full redirector to connect to DEC Pathworks
	running on an Ethernet network. For additional configuration options
	(such as Token Ring, asynchronous DECnet, or the Windows for
	Workgroups basic redirector), call DEC Technical Support at (800)
	332-8000.
	
	This procedure assumes the following conditions are true:
	
	- DEC Pathworks is installed in the C:\DECNET directory.
	- Windows for Workgroups is installed in the C:\WINDOWS directory.
	- Your boot drive is drive C.
	
	If your system configuration differs, substitute the correct paths
	where necessary.
	
	To Integrate DEC Pathworks and Windows for Workgroups 3.1
	---------------------------------------------------------
	
	1. Make backup copies of the following files:
	
	     AUTOEXEC.BAT
	     CONFIG.SYS
	     STARTNET.BAT
	     PROTOCOL.INI
	     SYSTEM.INI
	
	  If you encounter any problems during this procedure, you can restore
	  these files and return to your original working configuration.
	
	2. In Windows for Workgroups Control Panel, choose the Network icon.
	  Choose the Networks button and remove all the networks listed in
	  the Other Networks In Use box. Choose the OK button twice to close
	  the Compatible Networks and Network Settings dialog boxes. When
	  prompted to restart Windows, choose the Continue button. Quit
	  Windows for Workgroups, but do not restart your computer.
	
	3. Open your AUTOEXEC.BAT file in a text editor, such as MS-DOS
	  Editor, and make the following changes:
	
	  a. Insert the REM command at the beginning of the NET START command
	     line. For example, change
	
	        c:\windows\net start
	
	     -to-
	
	        rem c:\windows\net start
	
	  b. If the Pathworks directory is not already included in your PATH
	     statement, add it. For example, change
	
	        path c:\windows;c:\dos;
	
	     -to-
	
	        path c:\windows;c:\dos;c:\decnet;
	
	4. Open your CONFIG.SYS file in a text editor and make the following
	  changes:
	
	  a. Insert the REM command at the beginning of the PROTMAN.SYS
	     DEVICE command line. For example, change
	
	        device=c:\decnet\protman.sys /i:c:\decnet
	
	     -to-
	
	        rem device=c:\decnet\protman.sys /i:c:\decnet
	
	     NOTE: The CONFIG.SYS file contains two files with similar names:
	     PROTMAN.SYS and PROTMAN.DOS. PROTMAN.SYS is the protocol manager
	     for Pathworks, which you just disabled. PROTMAN.DOS is the
	     protocol manager for Windows for Workgroups and should not be
	     altered.
	
	  b. Add a DEVICE command line to load the Pathworks file,
	     DLLNDIS.EXE, before the line that loads WORKGRP.SYS. For
	     example, change
	
	        device=c:\windows\elnkii.dos
	        device=c:\windows\workgrp.sys
	
	     -to-
	
	        device=c:\windows\elnkii.dos
	        device=c:\decnet\dllndis.exe
	        device=c:\windows\workgrp.sys
	
	     NOTE: The file ELNKII.DOS may differ depending on the type of
	     network interface card (NIC) you use.
	
	5. The following two steps require that you use a text editor that has
	  a cut and paste feature, such as MS-DOS Editor.
	
	  a. Open the C:\DECNET\PROTOCOL.INI file, and cut the [DATALINK]
	     section (including its title, [DATALINK]).
	
	  b. Open the C:\WINDOWS\PROTOCOL.INI file, position the insertion
	     point at the end of the file and paste in the [DATALINK]
	     section. Do not close PROTOCOL.INI or quit the text editor.
	
	6. Make the following additional changes to your
	  C:\WINDOWS\PROTOCOL.INI file:
	
	  a. Modify the BINDINGS statement in the [DATALINK] section so that
	     it is the same as the BINDINGS statement for your other
	     transports. For example, change
	
	        bindings=elnkii.dos
	
	     -to-
	
	        bindings=ms$elnkii
	
	     NOTE: In most cases, NetBEUI is your Windows for Workgroups
	     transport. If this is the case, simply copy the BINDINGS
	     statement from the [NetBEUI] section to the [DATALINK] section,
	     and insert the REM command at the beginning of the original
	     BINDINGS statement in the [DATALINK] section. For a more
	     complete example of this modification, see the "Sample
	     PROTOCOL.INI" section below.
	
	  b. In the [DATALINK] section, make sure that the NI_IRQ statement
	     is set to the same value as the INTERRUPT statement in your
	     network card section. For example, if your network card section
	     appears as follows
	
	        [ms$elnkii]
	        drivername=elnkii$
	        interrupt=3
	        ...
	
	     change the NI_IRQ statement to read
	
	        [DATALINK]
	        ni_irq=3
	
	  c. In the [NETWORK.SETUP] section, copy the LANA line for NetBEUI,
	     and paste it on the next line. The line you paste should look
	     similar to the following:
	
	        lana0=ms$ewtrbtp,1,ms$netbeui
	
	     NOTE: The first parameter, MS$EWTRBTP in this example, varies
	     depending on the NIC you use.
	
	  d. In the line you pasted, increase the LANA number by one and
	     replace the last parameter, MS$NETBEUI with DATALINK. The
	     resulting line should look similar to the following:
	
	        lana1=ms$ewtrbtp,1,datalink
	
	7. Open the STARTNET.BAT file in a text editor and make the following
	  changes:
	
	  a. Find the line that contains the NETBIND command and insert the
	     REM command at the beginning of the line. For example, change
	
	        %boot%\decnet\netbind
	
	     -to-
	
	        rem %boot%\decnet\netbind
	
	  b. Add the NET START command after the line loading NETBIND. For
	     example, change
	
	        rem %boot%\decnet\netbind
	
	     -to-
	
	        rem %boot%\decnet\netbind
	        c:\windows\net start
	
	  c. Disable the command that starts the Pathworks redirector,
	     REDIR.EXE, using the REM command. For example, change
	
	        %boot%\decnet\redir5.exe
	
	     -to-
	
	        rem %boot%\decnet\redir5.exe
	
	  d. Disable the command that loads the DLLNDIS driver using the REM
	     command. For example, change
	
	        %boot%\decnet\dllndis
	
	     -to-
	
	        rem %boot%\decnet\dllndis
	
	  e. Locate the command lines that load DNNETH.EXE and add the /LANA
	     switch to specify which LANA the DECnet protocol is using. (This
	     is the same number you changed in step 6d; it is the LANA number
	     for the DATALINK protocol.) For example, change
	
	        %boot%\decnet\dnneth.exe /rem:2
	        if errorlevel 1 %boot%\decnet\dnneth.exe /rem:2
	
	     -to-
	
	        %boot%\decnet\dnneth.exe /rem:2 /lana:1
	        if errorlevel 1 %boot%\decnet\dnneth.exe /rem:2 /lana:1
	
	  f. Locate the following section for the Pathworks redirector:
	
	        echo -----------------------------------------------
	        echo using basic redirector
	        echo -----------------------------------------------
	
	     Insert the line, GOTO TIMEDONE, as follows:
	
	        goto timedone
	        echo -----------------------------------------------
	        echo using basic redirector
	        echo -----------------------------------------------
	
	  g. If you use LAT and/or CTERM, add the appropriate line(s) after
	     the :TIMEDONE label. For example, if you want to add LAT, add
	     the following lines:
	
	        :timedone
	        c:\decnet\lat.exe
	
	     Or, if you want to add CTERM, add the following lines:
	
	        :timedone
	        c:\decnet\cterm.exe
	
	     NOTE: If you plan to use LAT, LAD, and/or CTERM, you must copy
	     the LAT.EXE, LAD.EXE, and/or CTERM.EXE files from the Pathworks
	     PCSAV41 file service before you reboot.
	
	8. Open your SYSTEM.INI file in a text editor and make the following
	  changes:
	
	  a. In the [386Enh] section, find the NETWORK statement and add the
	     virtual network driver DECNET.386 as follows:
	
	        [386enh]
	        network=vnetbios.386,...,decnet.386
	
	     NOTE: The DECNET.386 file is not included with Windows for
	     Workgroups. If you have Windows version 3.1, it is located on
	     Disk 2. If you are upgrading over a previous Windows
	     installation that was set up for Pathworks, this file should
	     already be in your WINDOWS\SYSTEM subdirectory. If this is a new
	     Windows for Workgroups installation and you do not have Windows
	     3.1, DECNET.386 is available from the DECPCI forum on CompuServe
	     or from DEC Technical Support.
	
	  b. Add the following statement to the [386Enh] section:
	
	        timercriticalsection=10000
	
	After you restart your machine, you can connect to DEC Pathworks
	servers as well as other machines in your Windows for Workgroups
	workgroup. If you cannot connect to your DEC Pathworks network,
	contact DEC Technical Support.
	
	NOTE: Pathworks servers do not appear in the list of shared
	directories because they are not included in the Windows for
	Workgroups network browsing system. To connect to a Pathworks server,
	you must type the name of the server and share name.
	
	Sample PROTOCOL.INI
	-------------------
	
	The sample PROTOCOL.INI file below has been modified by following the
	previous steps. Comments on modifications appear in parentheses to the
	right of statements. This file was taken from a system using NetBEUI
	installed on a 3Com EtherLink II NIC.
	
	[network.setup]
	  version=0x0000
	  netcard=ms$elnkii,1,MS$ELNKII
	  transport=ms$netbeui,MS$NETBEUI
	  lana0=ms$elnkii,1,ms$netbeui
	  lana1=ms$elnkii,1,DATALINK
	
	[protman]
	  DriverName=PROTMAN$
	
	[MS$ELNKII]              (NIC section)
	  DriverName=ELNKII$
	  INTERRUPT=3
	  IOADDRESS=0x300
	  MAXTRANSMITS=12
	  TRANSCEIVER=onboard   (thin Ethernet cable)
	
	[MS$NETBEUI]             (NetBEUI transport section)
	  DriverName=netbeui$
	  SESSIONS=6
	  NCBS=12
	  BINDINGS=MS$ELNKII
	  LANABASE=0
	
	[DATALINK]               (DEC Pathworks transport)
	  DRIVERNAME=DLL$MAC
	  LG_BUFFERS=16
	  SM_BUFFERS=6
	  OUTSTANDING=32
	  HEURISTICS=0
	  BINDINGS=MS$ELNKII    (changed to match NetBEUI BINDINGS line)
	  NI_IRQ=3              (changed to match NIC INTERRUPT line)
	
	REFERENCES
	==========
	
	DEC Technical Support can be reached by calling (800) 332-8000. DEC
	provides a detailed document titled "PATHWORKS for DOS and Windows for
	Workgroups Installation Guide," which describes how to configure
	Windows for Workgroups and a Pathworks network for compatibility. The
	document provides information on the following configurations and
	topics:
	
	  Physical Media:
	
	     Ethernet
	     Token Ring
	     Asynchronous DECnet
	     DECnet
	
	  Protocols:
	
	     DECnet
	     Pathworks NetWare Coexistence
	     Digital's LAST/LAD
	     Pathworks NetBEUI
	     Windows for Workgroups NetBEUI
	     Windows for Workgroups Novell
	
	  Miscellaneous:
	
	     Running Windows for Workgroups Novell IPX on Digital's Ethernet
	     Connecting to Pathworks for VMS or Pathworks for Ultrix
	     Setting up Local Area Disk (LAD) Support
	     Using InfoServers
	
	You can download "PATHWORKS for DOS and Windows for Workgroups
	Installation Guide" from the DECPCI forum on CompuServe, or you can
	call DEC Technical Support.
	
	Additional query words: 3.10 3.11
	
	======================================================================
	Keywords          :  
	Technology        : kbAudDeveloper kbWFWSearch
	Version           : WINDOWS:
	
	=============================================================================
	

{% endraw %}
