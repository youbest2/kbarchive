---
layout: page
title: "Q301260: HOW TO: Install SQL Server CE by Using eMbedded Visual Basic"
permalink: /kb/301/Q301260/
---

## Q301260: HOW TO: Install SQL Server CE by Using eMbedded Visual Basic

{% raw %}

	Article: Q301260
	Product(s): Microsoft Visual Basic for Windows
	Version(s): 3.0
	Operating System(s): 
	Keyword(s): kbenv kbGrpDSVB kbAudDeveloper kbHOWTOmaster
	Last Modified: 06-JUN-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft eMbedded Visual Basic, version 3.0 
	-------------------------------------------------------------------------------
	
	IN THIS TASK
	------------
	
	- SUMMARY
	
	   - Requirements
	- How to Use eMbedded Visual Basic to Install SQL Server CE
	- Additional Steps
	
	- REFERENCES
	
	SUMMARY
	=======
	
	This article demonstrates how to leverage the Microsoft eMbedded Visual Basic
	development environment to automatically install Microsoft SQL Server CE on a
	Microsoft Windows CE-based device.
	
	Requirements
	------------
	
	The following list outlines the recommended hardware, software, network
	infrastructure, and service packs that you will need:
	
	- Microsoft Windows 2000 or Windows NT Workstation 4.0 with Service Pack 5
	  (SP5) or later
	- Microsoft eMbedded Visual Basic
	- Microsoft Windows CE-based device
	
	How to Use eMbedded Visual Basic to Install SQL Server CE
	---------------------------------------------------------
	
	The eMbedded Visual Basic development environment automates many of the debugging
	processes that you need to use to develop a new application. Part of this
	process includes downloading prototype versions of the application into a
	Windows CE-based device where it can be run and debugged.
	
	The development environment uses ActiveSync on the development computer to
	download the files into the Windows CE-based device. The development environment
	can automatically monitor which executable files are included in the application
	and which DLLs the application uses. During the download process, the
	development environment downloads the latest version of all of these components
	together. If you are using eMbedded Visual Basic, you can take advantage of
	these capabilities during the development process.
	
	1. Start eMbedded Visual Basic, and then either create a new Windows CE project
	  or open an existing project.
	
	2. On the Project menu, click References, and select the "Microsoft CE SQL
	  Server Control 1.0" and "Microsoft CE ADO Control 3.1" check boxes. If your
	  application uses the ActiveX Data Objects (ADO) extensions for data
	  definition language (DDL) (or ADOX), select the Microsoft CE ADO Ext. 3.1 for
	  DDL check box. Click OK.
	
	3. On the Project menu, click Properties.
	
	4. On the General tab, in the "Update Component Frequency" list box, click Ask.
	
	5. Select the "Runtime Files and Project Components" check boxes.
	
	6. On the Run menu, click Execute to invoke the eMbedded Visual Basic program.
	  eMbedded Visual Basic downloads and registers all SQL Server CE, ADO, OLE DB,
	  and ADOX components that you selected in step 2 of this procedure to your
	  Windows CE-based device.
	
	  NOTE: In the event that you encounter installation problems, you can force
	  eMbedded Visual Basic to download components again. To do this, on the
	  Project menu, and click Properties. In the "Update Component Frequency" list
	  box, click Always, and then click Project Components.
	
	Your application components are downloaded to the Windows CE-based device each
	time you modify and rebuild your application to test it.
	
	NOTE: You do not need the DLLRegister.exe file if you are using eMbedded Visual
	Basic to deploy your application because the tools handle all registration
	automatically.
	
	Additional Steps
	----------------
	
	After you have completed your application, you can use the download capability of
	the eMbedded Visual Basic tools to deploy the application to every Windows
	CE-based device.
	
	This simple method of deployment saves you the trouble of creating any other
	setup mechanism, but it means that you must purchase a copy of the eMbedded
	Visual Basic tools and SQL Server CE for every computer that you want to use for
	installing your application onto Windows CE-based devices. Microsoft recommends
	this method only for smaller installations where it is not a problem to connect
	every Windows CE-based device to a development computer to initiate the setup.
	
	REFERENCES
	==========
	
	For more information, see the Microsoft Windows CE 3.0 Software Developer
	Documentation at the following MSDN Web site:
	
	  http://msdn.microsoft.com/library/default.asp?URL=/library/wcedoc/wceintro/cestart.htm
	
	You can download ADOCE 3.1 from the following Microsoft Web site:
	
	  http://msdn.microsoft.com/code/sample.asp?url=/msdn-files/027/001/491/msdncompositedoc.xml
	
	For more information about SQL Server CE, see the following Microsoft Web site:
	
	  http://www.microsoft.com/sql/CE/default.asp
	
	Additional query words:
	
	======================================================================
	Keywords          : kbenv kbGrpDSVB kbAudDeveloper kbHOWTOmaster 
	Technology        : kbVBSearch kbAudDeveloper kbZNotKeyword2 kbVBeMbSearch kbVBeMb300
	Version           : :3.0
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
