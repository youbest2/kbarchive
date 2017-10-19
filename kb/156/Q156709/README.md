---
layout: page
title: "Q156709: XCLN: Errors When Trying to Start EFD"
permalink: kb/156/Q156709/
---

## Q156709: XCLN: Errors When Trying to Start EFD

	Article: Q156709
	Product(s): Microsoft Exchange
	Version(s): winnt:4.0
	Operating System(s): 
	Keyword(s): kbusage
	Last Modified: 13-JAN-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Server, version 4.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When you attempt to start the Microsoft Exchange Electronic Forms Designer
	(EFD), the following error message may appear:
	
	  Unable to create information structure for clipboard file.
	
	You may also encounter an error after you finish the Forms Designer Wizard by
	either clicking Finish before the form template appears or by adding one or more
	controls to the template form and clicking Save or Save As on the File menu. The
	following error message appears:
	
	  The file, c:\temp\e~fp3733a.tmp', cannot be saved.
	
	CAUSE
	=====
	
	These errors are caused by outdated ODBC components or by invalid file pointers
	in one or more of the Odbc*.ini files.
	
	WORKAROUND
	==========
	
	To work around this problem:
	
	- Verify that the proper ODBC components are installed and that the .ini files
	  contain the proper paths to the DLLs.
	
	Additional file clean-up and re-installation of EFD may be required.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Microsoft Exchange version 4.0.
	We are researching this problem and will post new information here in the
	Microsoft Knowledge Base as it becomes available.
	
	MORE INFORMATION
	================
	
	ODBC is a common interface used and installed by many applications. EFD uses it
	in the creation and management of forms. ODBC was first introduced with
	Microsoft Access 1.0 and many other applications install one or more of the core
	components like Odbc.dll. Currently, detection of installed ODBC components and
	whether or not to update them is inconsistent. This can lead to the error
	messages and application malfunction.
	
	The following ODBC components are installed by EFD 4.0 Setup:
	
	Filename      Size       Version       Target Directory
	
	Odbc.dll       56240     2.10.2401     Windows\System
	Odbcadm.exe     6464     2.10.23.9     Windows\System
	Odbccurs.dll   88896     2.10.23.23    Windows\System
	Odbcinst.dll   92576     2.10.24.1     Windows\System
	Odbcinst.hlp   17412     n/a           Windows\System
	Odbcjt16.dll  246928     2.0.23.17     Windows\System
	Odbctl16.dll   64080     1.0.23.9      Windows\System
	
	All EFD ODBC components have a date stamp consistent with the product release
	date, for example, 3/6/96 or a later Service Pack release date. However, because
	setup programs usually compare their version with the existing version's
	internal stamp (column 3, above), it is possible that a file with the same or
	greater internal version number (but different file date) already exists in the
	target directory. In this case, most setup programs will not overwrite the
	existing file.
	
	To see the internal version stamps of existing files:
	
	1. Start Msd.exe.
	
	2. On the File menu, click Find File.
	
	3. Type "odbc*.*" (without the quotation marks) in the Search For dialog box.
	
	4. Specify the appropriate drive, and select the Include Sub-dirs checkbox.
	
	This will list all ODBC files on the specified drive and display the associated
	internal version stamps. The MSD utility ships with MS-DOS versions 5.x and
	later and with Windows versions 3.1 and later. It will run under Windows 95 and
	Windows NT. Even though Windows NT will report a direct hard disk access
	attempt, you can click Ignore and utility will work.
	
	Odbc.ini files modified by EFD setup:
	
	EFD Setup creates or adds the following sections and entries in the INI files
	listed below:
	
	ODBC.INI
	
	  [ODBC Data Sources]
	  MS EFD Databases=Microsoft Access Driver (*.mdb)
	
	  [MS EFD Databases]
	  Driver=C:\WINDOWS\SYSTEM\odbcjt16.dll
	  DriverId=25
	  Exclusive=1
	  FIL=MS Access;
	  JetIniPath=odbcddp.ini
	  UID=admin
	
	ODBCDDP.INI
	
	  [ISAM]
	  PageTimeout=600
	  MaxBufferSize=512
	
	Note the entry "Driver=C:\WINDOWS\SYSTEM\odbcjt16.dll". A copy of this DLL must
	reside in this location in order for EFD to function properly. Additionally,
	"JetIniPath=odbcddp.ini" should exist in the \Windows subdirectory and contain
	the entries listed above.
	
	Additional Troubleshooting:
	
	Once you verify all of the above files and INI entries, if you start EFD and it
	still displays the "Unable to create information structure error message, follow
	these steps:
	
	1. Rename the Exchange\Efdforms\Efdcb.mdb and Efdcb.ldb files.
	
	2. Delete all old TMP files from the computer. This might require you to close
	  all running applications and restart the computer.
	
	3. Verify that the TEMP environmental variable references a valid path.
	
	4. Restart EFD.
	
	This should generate fresh versions of the EFDCB files. If this fails to resolve
	the problem, try reinstalling EFD over the current installation.
	
	Additional query words:
	
	======================================================================
	Keywords          : kbusage 
	Technology        : kbExchangeSearch kbExchange400 kbZNotKeyword2
	Version           : winnt:4.0
	
	=============================================================================
	