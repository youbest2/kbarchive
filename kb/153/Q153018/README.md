---
layout: page
title: "Q153018: BUG: CreateDynaset Holds Lock on Index if No Records Return"
permalink: /kb/153/Q153018/
---

## Q153018: BUG: CreateDynaset Holds Lock on Index if No Records Return

{% raw %}

	Article: Q153018
	Product(s): Microsoft Visual Basic for Windows
	Version(s): WINDOWS:4.0
	Operating System(s): 
	Keyword(s): kbDatabase kbVBp400 kbGrpDSVBDB kbDSupportkbbuglist
	Last Modified: 11-JAN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual Basic Standard Edition, 32-bit, for Windows, version 4.0 
	- Microsoft Visual Basic Professional Edition, 16-bit, for Windows, version 4.0 
	- Microsoft Visual Basic Professional Edition, 32-bit, for Windows, version 4.0 
	- Microsoft Visual Basic Enterprise Edition, 16-bit, for Windows, version 4.0 
	- Microsoft Visual Basic Enterprise Edition, 32-bit, for Windows, version 4.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	After opening a Dynaset that contains no records with a SQL statement that
	refers to an indexed field, attempting to access that table from another
	application can cause the following error:
	
	  Couldn't save; currently locked by <User_Name> on machine
	  <Machine_Name>
	
	To work around this problem, add a call to the Idle method of the DBEngine object
	immediately after the call to OpenRecordset. Add the following line of code:
	
	     DBEngine.Idle dbFreeLocks
	
	CAUSE
	=====
	
	The error occurs because the Jet engine is not, by default, releasing the lock
	on the index page after opening the Recordset. This behavior only occurs when
	the Recordset returned contains no records. It occurs with Jet 2.5 and Jet 3.0,
	but doesn't occur with Jet 1.1.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in the Microsoft products that are
	listed at the beginning of this article.
	
	MORE INFORMATION
	================
	
	Steps To Reproduce Problem
	--------------------------
	
	1. Start Visual Basic 4.0. Form1 is created by default.
	
	2. Open the References dialog (Tools Reference), and add a reference to either
	  DAO 2.5 (16-bit) or DAO 3.0 (32-bit).
	
	3. Add a single Command button to Form1.
	
	4. Add the following code to the form:
	
	     Private Sub Command1_Click()
	        Set db = OpenDatabase("BIBLIO.MDB")
	        Set rs = db.OpenRecordset("Select * From Authors Where AU_ID > _
	                 200", dbOpenDynaset)
	     End Sub
	
	5. From the Insert menu, choose Module, and insert a single code module.
	
	6. Add the following code to the module:
	
	     Global rs As Recordset
	     Global db As Database
	
	7. Press the F5 key or select Start from the Run menu to run the application.
	  Click on the Command button to open the database, and create a Recordset.
	
	8. Start another instance of Visual Basic. From the Add-Ins menu, choose Data
	  Manager, and start the Data Manager application.
	
	9. In Data Manager, open the same BIBLIO database that was opened in step 4.
	  Open the Authors table and attempt to add a new record. When the update is
	  attempted, Data Manager will give the error mentioned above.
	
	Additional query words:
	
	======================================================================
	Keywords          : kbDatabase kbVBp400 kbGrpDSVBDB kbDSupport kbbuglist
	Technology        : kbVBSearch kbAudDeveloper kbVB400Search kbVB400 kbVB16bitSearch
	Version           : WINDOWS:4.0
	Issue type        : kbbug
	Solution Type     : kbpending
	
	=============================================================================
	

{% endraw %}
