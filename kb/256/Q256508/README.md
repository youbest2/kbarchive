---
layout: page
title: "Q256508: Installing Routing and Remote Access Services in Unattended Mode"
permalink: /kb/256/Q256508/
---

## Q256508: Installing Routing and Remote Access Services in Unattended Mode

{% raw %}

	Article: Q256508
	Product(s): Microsoft Windows NT
	Version(s): winnt:4.0
	Operating System(s): 
	Keyword(s): kbsetup kbtool
	Last Modified: 08-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Server version 4.0 
	- Microsoft Windows NT Server, Enterprise Edition version 4.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	With the advent of Windows NT 4.0 Service Pack 5, you can install Routing and
	Remote Access Services (RRAS) in unattended Setup mode, requiring little user
	intervention. Service Pack 6 includes updated RRAS files in Support\RRAS
	folder.
	
	You can use one of two different methods to perform an unattended RRAS
	installation.
	
	The following text is a copy of the information in the RRAS Readme.txt file
	included with Service Pack 6a.
	
	MORE INFORMATION
	================
	
	The first method is performed where the Remote Access Service (RAS) was
	previously installed during an unattended installation of Windows NT 4.0
	Server.
	
	The second method is performed after the installation of the operating system and
	SP5. See the steps below for more detailed information.
	
	--------------------------------------------------------------
	2.1 Method One: Installing During Windows NT Unattended Setup
	--------------------------------------------------------------
	1. Copy all the Windows NT system files needed, usually the I386 folder (ALPHA is
	valid if installing on Alpha) and all its subfolders from the CD to a network
	share devoted to network server setup. The folder name of this network share is
	usually also I386 (the remainder of this article assumes I386 in the steps).
	
	2. Delete the following 63 files from the I386 folder. It is recommended that you
	create a batch file to help simplify the deletion process. For more information
	about creating this batch file, see Section, 4.2.
	
	asyncmac.sy_
	cis.sc_
	inetmib1.dl_
	kmddsp.ts_
	modem.in_
	ndistapi.sy_
	ndiswan.sy_
	nwlnkipx.sy_
	oemnsvra.in_
	pad.in_
	pppmenu.sc_
	rasacd.sy_
	rasadhlp.dl_
	rasadmin.cn_
	rasadmin.ex_
	rasadmin.hl_
	rasapi32.dl_
	rasauto.dl_
	rasautou.ex_
	rascauth.dl_
	rascbcp.dl_
	rasccp.dl_
	rascfg.dl_
	raschap.dl_
	rascpl.cp_
	rasctrs.dl_
	rasdial.ex_
	rasdlg.dl_
	rasfil32.dl_
	rasgloss.cn_
	rasgloss.hl_
	rasgprxy.dl_
	rasgtwy.dl_
	rasipcp.dl_
	rasiphlp.dl_
	rasipxcp.dl_
	rasman.dl_
	rasmon.ex_
	rasmxs.dl_
	rasnbfcp.dl_
	raspap.dl_
	rasphone.cn_
	rasphone.ex_
	rasphone.hl_
	raspppen.dl_
	raspptpe.sy_
	raspptpm.sy_
	raspptpu.sy_
	rasread.tx_
	rassapi.dl_
	rassauth.dl_
	rasscrpt.dl_
	rasser.dl_
	rassetup.cn_
	rassetup.hl_
	rasshell.dl_
	rasspap.dl_
	rastapi.dl_
	script.do_
	slip.sc_
	slipmenu.sc_
	switch.in_
	ws2_32.dl_
	
	3. Create a new folder named $OEM$ in the I386 folder.
	
	4. In the $OEM$ folder, create a file named CMDLINES.TXT with the following
	lines:
	[Commands] ".\UPDATE\UPDATE.EXE -U -Z -N"
	
	This file alerts Setup to install the Service Pack at the end of GUI mode setup.
	
	5. Copy SP6 to the $OEM$ folder. If you have the Service Pack CD, copy the
	contents of the I386 folder to the $OEM$ folder. If you have the compressed
	format of the Service Pack, you need to use the "SP6I386.EXE /X" command. See
	http://support.microsoft.com/highlights/ntw40.asp
	(http://support.microsoft.com/highlights/ntw40.asp)
	
	6. Expand the RRAS source files into the I386 folder using the "MPRI386.EXE /C"
	command.
	See http://www.microsoft.com/ntserver/nts/downloads/winfeatures/rras/rrasdown.asp
	(http://www.microsoft.com/ntserver/nts/downloads/winfeatures/rras/rrasdown.asp)
	
	7. Copy four updated RRAS files, required for unattended setup, to the I386
	folder, confirming any file replacement messages:
	- Dosnet.inf
	- Txtsetup.sif
	- Mprsetup.exe (SP5 filename: mprsetup.ste)
	- Rascfg.dll (SP5 filename: rascfg.ste)
	
	The first two, Dosnet.inf and Txtsetup.sif, are located in the Support\RRAS
	folder on the SP5 CD. The second two, Mprsetup.exe and Rascfg.dll, are located
	in SP6. Since they are RRAS-specific files, they have been renamed with the .ste
	file extension.
	
	Copy them from SP5 into the I386 folder and rename them using the proper file
	extension names.
	
	8. Modify "UNATTEND.TXT", located in the I386 folder, with settings for your RRAS
	computer(s). Information about RRAS specific parameters is listed in this
	document. A sample unattend file is included for your reference in Section 4.1.
	
	See the Knowledge Base Articles documented in Section 5.2 for any non-RRAS
	specific settings.
	
	9. Start unattended Setup mode using: WINNT[32].EXE /U:answer file /S:install
	source
	
	Examples:
	C:\I386\WINNT32 /U:C:\I386\UNATTEND.TXT
	C:\I386\WINNT /U:C:\I386\UNATTEND.TXT /S:C:\I386
	
	--------------------------------------------------------------
	2.2 Method Two: Installing Post-Windows NT Setup
	--------------------------------------------------------------
	
	1. Install Windows NT Server 4.0 (or use your existing installation).
	
	2. Install all necessary communications devices (Modems/VPNs). Verify that the
	following services/protocols are not installed on the system (if any or all are,
	remove them):
	
	- DHCP Relay Agent
	- RIP for Internet Protocol
	- RIP for NwLink IPX/SPX compatible transport
	- SAP Agent
	- Remote Access Service
	- Routing and Remote Access Service
	
	3. Install SP6 (RRAS requires SP3 or later to install).
	
	4. Expand the RRAS source files into a temporary folder using the "MPRI386.EXE
	/C" command. The remainder of this method assumes you used C:\TEMP.
	
	See http://www.microsoft.com/ntserver/nts/downloads/winfeatures/rras/rrasdown.asp
	(http://www.microsoft.com/ntserver/nts/downloads/winfeatures/rras/rrasdown.asp)
	
	5. Copy two updated RRAS files, required for unattended setup, to the C:\TEMP
	folder, confirming any file replacement messages:
	
	mprsetup.exe (SP6 file name: Mprsetup.ste)
	rascfg.dll (SP6 file name: Rascfg.ste)
	
	Mprsetup.exe and Rascfg.dll are located in SP6. Since they are RRAS specific
	files, they have been renamed with the .ste file extension. Copy and rename them
	from SP6 into the C:\TEMP folder using the proper file extension names. If you
	have the compressed format of the Service Pack, you need to use the "SP6I386.EXE
	/X" command to expand it.
	
	6. Modify "$WINNT$.INF" in the "%WINDIR%\SYSTEM32" folder of your existing
	Windows NT Server installation with specific settings for your RRAS computer(s).
	Information about RRAS specific parameters is listed in Section 3.0. A sample
	file has also been included for your reference. If the "$WINNT$.INF" file does
	not exist on your computer, create it using the parameter information.
	
	7. Start the RRAS setup using the Run command or the command line: mprsetup.exe
	/u install source
	
	Example: C:\TEMP\mprsetup.exe /u C:\Temp
	
	8. Reapply SP6.
	
	--------------------------------------------------------------
	2.3 Known Issues with Method One
	
	1. If you want to install the NWLink IPX/SPX Compatible Transport during the
	unattended Setup mode, perform the following steps:
	
	- Delete NDIS.SY_ from the I386 folder
	- Copy NDIS.SYS from Service Pack 6 into the I386 folder
	- Start unattended Setup mode
	
	2. More than one NIC can not be configured for static or DHCP TCP/IP addressing
	during unattended setup. It can be set manually after the restarting the
	computer or see Section 5.2 for information on a workaround.
	
	3. The IPX Internal Network Number can not be configured during unattended Setup
	mode. It can be set manually after restarting the computer or see Section 5.2
	for information on a workaround.
	
	4. The IPX Frame Type can not be configured during unattended Setup mode. It can
	be set manually after first boot or see Section 5.2 for information on a
	workaround.
	
	5. The "Remote Access Admin" shortcut on the Start Menu\Programs\Administrative
	Tools (Common) folder is not removed by Setup. You receive a warning if you try
	to use this application. To avoid this, remove the following line from the
	[AdminTools] block of syssetup.inf before installing:
	
	%rasadmin% = rasadmin.exe,rasadmin.exe,,0
	
	--------------------------------------------------------------
	2.4 Known Issues with Method Two
	--------------------------------------------------------------
	1. The RRAS parameter section located in $winnt$.inf must be named
	"RASParamSection" or unattended Setup fails.
	
	2. Normally, for the PPTP Protocol to be installed, the Remote Access Service
	(RAS) must also be installed or NT will install it for you. RAS/RRAS cannot be
	currently installed if you want to use RRAS unattend Setup Method Two. The
	easiest way to install the PPTP Protocol without installing RAS is to perform
	the following steps:
	
	- Click Start, point to Settings, and click Control Panel.
	- Double-click Network, click the Protocols tab, and click Add.
	- Select the Point To Point Tunneling Protocol, and click OK.
	- Select the desired number of VPN Ports, and click OK.
	- Click OK on the Setup Message regarding RAS.
	- Click Cancel on the Add RAS Device dialog.
	- Click Cancel on the Remote Access Setup dialog.
	- Click Yes on the warning message, and click Close.
	
	===================================================
	3.0 NEW UNATTENDED OPTIONS
	===================================================
	The following information is intended to be a supplement for existing Windows NT
	4.0 unattended information found in the Knowledge Base. The updated
	configuration options described below need to be used in conjunction with
	previously documented unattended Setup options to successfully install the
	Routing and Remote Access Service during an unattended installation of Windows
	NT Server 4.0. See the Section 5.2 for additional Knowledge Base article
	information.
	
	New unattended options:
	
	[Ras PPTP Parameters]
	
	NumVPN
	
	Value: Number of VPN ports
	Specifies the number of Virtual Private Network (VPN) devices PPTP setup should
	create. You can specify the number of VPN devices from 1 to 255. The default
	value is 1.
	
	[RasParameters]
	
	PortSections
	Values: port section name
	The PortSections key is used to define a port section name. Multiple port section
	names can be specified but they must be separated by commas ",". See [Port
	Section Name] definition below.
	
	DialoutProtocols
	Value: TCP/IP | IPX | NETBEUI | All
	ALL implies all installed protocols.
	
	RasType
	Value: RAS | DemandDial | LanToLan | All
	The RasType key defines the type of RRAS installation you want to perform.
	RAS - Install as a RAS Server (default value).
	DemandDial - Install as a DemandDial Router/RAS Server (DemandDial option will
	automatically install the RAS Server option).
	
	LanToLan - Install as a LanToLan Router only (DemandDial and RAS are disabled).
	All - Install all of the options above.
	
	DialinProtocols
	Value: TCP/IP | IPX | NETBEUI | All
	ALL implies all installed protocols.
	
	NetBEUIClientAccess
	Value: Network | ThisComputer
	Default is Network.
	
	TcpIpClientAccessv Value: Network | ThisComputer
	Default is Network.
	
	UseDHCP
	Value: YES | NO
	Default is YES.
	
	StaticAddress
	Value: Network_ID
	The StaticAddress key is required if UseDHCP = NO.
	
	StaticMask
	Value: Subnet_Mask
	The StaticMask key is required if UseDHCP = NO.
	
	ClientCanRequestIPAddress
	Value: YES | NO
	Default is NO.
	
	IpxClientAccess
	Value: Network | ThisComputer
	Default is Network.
	
	AutomaticNetworkNumbers
	Value: YES | NO
	Default is YES.
	
	NetworkNumberFrom
	Value: IPX_net_number
	Valid numbers range from 1 to 0xFFFFFFFE. This key is required if
	AutomaticNetworkNumbers = NO.
	
	AssignSameNetworkNumber
	Value: YES | NO
	Default is YES.
	
	ClientsCanRequestIpxNodeNumber
	Value: YES | NO
	Default is NO.
	
	[Port Section Name]
	
	PortName
	Value: COM1 | COM2 | COM3-COM25 | VPN1 | VPN2 | VPN3-VPN8
	The PortName key indicates the names of the ports to be configured in a
	particular port section.
	
	DeviceType
	Value: Modem | Vpn
	The DeviceType key indicates the type of device RRAS should install. ISDN devices
	are not currently supported.
	
	PortUsage
	Value: DialOut | DialIn | DialInOut | Routing | All
	The PortUsage key defines the dialing properties for the ports being configured.
	
	DialOut - enables the port(s) to be used for dialing out as a RAS client.
	DialIn - enables the port(s) to be used for dialing in as a RAS server.
	DialInOut - enables the port(s) to be used for dialing out/dialing in as a RAS
	client/server.
	Routing - enables the port(s) to be used for dialing out/dialing in as a
	Demand-dial Router.
	All - enables all of the port options above.
	
	=================================================
	4.0 SAMPLE FILES
	=================================================
	
	----------------------------------------
	4.1 Unattend Sample File (UNATTEND.TXT)
	----------------------------------------
	A sample unattended installation file has been created below for your use. This
	file is included for reference purposes only; it's not intended for use as your
	actual answer file.
	
	;[Unattended]
	;OEMPreinstall = Yes
	;NoWaitAfterTextMode = 1
	;NoWaitAfterGuiMode = 1
	;FileSystem = LeaveAlone
	;ExtendOemPartition = 0
	;ConfirmHardware = No
	;NtUpgrade = No
	;Win31Upgade = No
	;TargetPath = \RRASUTND
	
	;[GuiUnattended]
	;OemSkipWelcome = 1
	;OEMBlankAdminPassword = 1
	;TimeZone = "(GMT-08:00) Pacific Time (US and Canada); Tijuana"
	;AdvServerType = SERVERNT
	
	;[UserData]
	;FullName = UserName
	;OrgName = CompanyName
	;ComputerName = ComputerName
	
	;[LicenseFilePrintData]
	;AutoMode = PERSEAT
	;[Display]
	;BitsPerPel = 32
	;XResolution = 800
	;YResolution = 600
	;VRefresh = 85
	;AutoConfirm = 1
	
	;[Modem]
	;InstallModem = ModemParameter
	
	;[ModemParameter]
	;COM1 = "Courier V.Everything External Plug and Play"
	
	;[Network]
	;JoinWorkGroup = WORKGROUP
	;DetectAdapters = DetectNICs
	;InstallProtocols = ProtocolList
	;InstallServices = SevicesList
	
	;[DetectNICs]
	;DetectCount = 1
	
	;[ProtocolList]
	;TC = InstallTCPIP
	;NWLNKIPX = InstallIPX
	;NBF = InstallNetBEUI
	;RASPPTP = InstallPPTP
	
	;[InstallTCPIP]
	;DHCP = Yes
	
	;[InstallIPX]
	;[InstallNetBEUI]
	
	;[InstallPPTP]
	;NumVpn = 7
	
	;[SevicesList]
	;RAS = RASParamSection
	
	;[RASParamSection]
	;PortSections = PortSection1,PortSection2
	;DialoutProtocols = All
	;RasType = All
	;DialinProtocols = All
	;UseDHCP = No
	;StaticAddress = 192.168.1.240
	;StaticMask = 255.255.255.240
	;IpxClientAccess = Network
	;AutomaticNetworkNumbers = YES
	;AssignSameNetworkNumber = YES
	;ClientsCanRequestIpxNodeNumber = NO
	;NetBEUIClientAccess = Network
	
	;[PortSection1]
	;PortName = COM1
	;DeviceType = MODEM
	;PortUsage = All
	
	;[PortSection2]
	;PortName = VPN1-VPN7
	;DeviceType = VPN
	;PortUsage = All
	
	--------------------------------------------------------------
	4.2 Deletion Batch File
	--------------------------------------------------------------
	You can create a batch file for Method One by using the following lines:
	
	del asyncmac.sy_ /F
	del cis.sc_ /F
	del inetmib1.dl_ /F
	del kmddsp.ts_ /F
	del modem.in_ /F
	del ndistapi.sy_ /F
	del ndiswan.sy_ /F
	del nwlnkipx.sy_ /F
	del oemnsvra.in_ /F
	del pad.in_ /F
	del pppmenu.sc_ /F
	del rasacd.sy_ /F
	del rasadhlp.dl_ /F
	del rasadmin.cn_ /F
	del rasadmin.ex_ /F
	del rasadmin.hl_ /F
	del rasapi32.dl_ /F
	del rasauto.dl_ /F
	del rasautou.ex_ /F
	del rascauth.dl_ /F
	del rascbcp.dl_ /F
	del rasccp.dl_ /F
	del rascfg.dl_ /F
	del raschap.dl_ /F
	del rascpl.cp_ /F
	del rasctrs.dl_ /F
	del rasdial.ex_ /F
	del rasdlg.dl_ /F
	del rasfil32.dl_ /F
	del rasgloss.cn_ /F
	del rasgloss.hl_ /F
	del rasgprxy.dl_ /F
	del rasgtwy.dl_ /F
	del rasipcp.dl_ /F
	del rasiphlp.dl_ /F
	del rasipxcp.dl_ /F
	del rasman.dl_ /F
	del rasmon.ex_ /F
	del rasmxs.dl_ /F
	del rasnbfcp.dl_ /F
	del raspap.dl_ /F
	del rasphone.cn_ /F
	del rasphone.ex_ /F
	del rasphone.hl_ /F
	del raspppen.dl_ /F
	del raspptpe.sy_ /F
	del raspptpm.sy_ /F
	del raspptpu.sy_ /F
	del rasread.tx_ /F
	del rassapi.dl_ /F
	del rassauth.dl_ /F
	del rasscrpt.dl_ /F
	del rasser.dl_ /F
	del rassetup.cn_ /F
	del rassetup.hl_ /F
	del rasshell.dl_ /F
	del rasspap.dl_ /F
	del rastapi.dl_ /F
	del script.do_ /F
	del slip.sc_ /F
	del slipmenu.sc_ /F
	del switch.in_ /F
	del ws2_32.dl_ /F
	
	=======================================
	5.0 KNOWLEDGE BASE ARTICLES
	=======================================
	
	--------------------------------------------------------------
	5.1 Additional Articles
	--------------------------------------------------------------
	For additional information, see the following articles in the Knowledge Base:
	
	ARTICLE-ID: Q155197
	TITLE : Unattended Setup Parameters for Unattend.txt File
	
	ARTICLE-ID: Q177267
	TITLE : Unattended Setup Disables EnableDHCPFlag on Second Adapter
	
	ARTICLE-ID: Q159837
	TITLE : Setting the Frame Type for IPX During Unattended Setup
	
	ARTICLE-ID: Q195178
	TITLE : Setting the IPX Internal Network Number During Unattended Setup
	
	ARTICLE-ID: Q175267
	TITLE : How to Install an OEM Modem .INF File In Unattended Setup
	
	ARTICLE-ID: Q168814
	TITLE : Installing WinNT 4.0 Service Packs During Unattended Install
	
	REFERENCES
	==========
	
	For additional information, click the article number below to view the article
	in the Microsoft Knowledge Base:
	
	  Q219322 Unattended Setup for RRAS (Steelhead) Requires Service Pack 5
	
	Additional query words:
	
	======================================================================
	Keywords          : kbsetup kbtool 
	Technology        : kbWinNTsearch kbWinNT400search kbWinNTSsearch kbWinNTSEntSearch kbWinNTSEnt400 kbWinNTS400search kbWinNTS400
	Version           : winnt:4.0
	Issue type        : kbinfo
	
	=============================================================================
	

{% endraw %}
