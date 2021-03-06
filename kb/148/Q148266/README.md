---
layout: page
title: "Q148266: Data Forms Designer Doesn't Recognize MS Access 7.0 Database"
permalink: /kb/148/Q148266/
---

## Q148266: Data Forms Designer Doesn't Recognize MS Access 7.0 Database

{% raw %}

	Article: Q148266
	Product(s): Microsoft Visual Basic for Windows
	Version(s): WINDOWS:4.0
	Operating System(s): 
	Keyword(s): kbGrpDSVBDB
	Last Modified: 11-JAN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual Basic Standard Edition, 32-bit, for Windows, version 4.0 
	- Microsoft Visual Basic Professional Edition, 32-bit, for Windows, version 4.0 
	- Microsoft Visual Basic Enterprise Edition, 32-bit, for Windows, version 4.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	DataForms Designer under Windows 95 does not recognize a Microsoft Access 7.0
	database and generates the error: "Can't open DataBase "c:\xxx.mdb" It may not
	be a Database or the file may be corrupt".
	
	Steps to Reproduce the Problem
	------------------------------
	
	1. Start Visual Basic or from the File menu, choose New Project (ALT, F, N).
	
	2. From the Add-ins menu select Data Form Designer. If Data Form Designer is not
	  available choose Add-in-manager and add it to the menu.
	
	3. After selecting Data Form Designer click on the Opendatabase button on Data
	  form designer dialog and select the Northwind.mdb from the samples directory
	  of the Access application. The error message will display at this point.
	
	CAUSE
	=====
	
	In the dfd.frm which is in the data wizard sample, there is a subroutine Sub
	cmdOpenDB_Click which includes a case statement that incorrectly has a
	dlgDBOpen.Flags setting of &H4 or the constant value for cdlOFNHideReadOnly.
	The dlgDBOpen.Flags needs to be assigned the cdlOFNExplorer constant value which
	can be located in the object browser.
	
	RESOLUTION
	==========
	
	1. Start VB4-32 and load the dfd.vbp project from the samples\datawiz directory
	  of VB4-32.
	
	2. View the code of dfd.frm file and locate the cmdOpenDB_Click procedure.
	
	3. Change the value assigned to the dlgDBOpen.Flags setting which is shown below
	  with the incorrect setting.
	
	     With dlgDBOpen
	           .FilterIndex = 1
	           .FileName = msDBName  '""
	           .CancelError = True
	           .Flags = &H4
	           .Action = 1
	     End With
	
	To change the constant value for dlgDBOpen.Flags:
	
	1. Highlight the &H4 value.
	
	2. Press the F2 key to bring up the Object Browser.
	
	3. From the Libraries/Projects drop down list box Select "MSComDlg - Microsoft
	  Common Dialog Control."
	
	4. Under Classes/Modules, select FileOpenConstants.
	
	5. Under Methods/Properties, select cdlOFNExplorer, then click the Paste button.
	
	6. From the VB file menu, choose Make Ole Dll File, and save to the
	  samples\datawiz directory of VB4-32.
	
	7. In a new project, detach then reattach the DataForm Designer to the Add- ins
	  menu. It will now recognize a Microsoft Access 7.0 database.
	
	Additional query words: kbVBp400 kbVBp kbDSupport kbdse
	
	======================================================================
	Keywords          : kbGrpDSVBDB 
	Technology        : kbVBSearch kbAudDeveloper kbVB400Search kbVB400
	Version           : WINDOWS:4.0
	
	=============================================================================
	

{% endraw %}
