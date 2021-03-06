---
layout: page
title: "Q300586: BUG: Error &quot;Row Cannot Be Located for Updating&quot;"
permalink: /kb/300/Q300586/
---

## Q300586: BUG: Error &quot;Row Cannot Be Located for Updating&quot;

{% raw %}

	Article: Q300586
	Product(s): Microsoft Visual Basic for Windows
	Version(s): 6.0
	Operating System(s): 
	Keyword(s): _IK_kbATM kbDataBinding kbJET kbGrpDSVBDB kbGrpDSMDAC kbDSupport
	Last Modified: 25-JUN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual Basic Enterprise Edition for Windows, version 6.0 
	- Microsoft Visual Basic Professional Edition for Windows, version 6.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	If an ActiveX Data Objects data control (ADODC) is bound to a Microsoft Access
	table that specifies a default value for the numeric field, when you take the
	following actions:
	
	1. Add a new record to the ADO recordset, which the ADODC exposes, without
	  entering a value for that numeric field.
	
	2. Update the recordset.
	
	3. Type a value into the numeric field (either directly into the Recordset field
	  or into the corresponding DataGrid cell) in that same newly-added record.
	
	4. Update the recordset again.
	
	the following run-time error is raised with error number -2147217864 (80040e38)
	or 6153:
	
	  Row cannot be located for updating. Some values may have changed since it was
	  last read.
	
	If a DataGrid control is bound to the ADODC, the same error message usually
	appears a second time without an error number in a dialog box that is entitled
	"Microsoft DataGrid Control."
	
	RESOLUTION
	==========
	
	To resolve this problem, remove the default value that is specified for the
	numeric field in the Access database table.
	
	Alternately, you can run an UPDATE statement on a separate ADO Connection object
	to update the numeric field in the newly-added record directly in the database
	and then refresh the ADODC.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a bug in the Microsoft products listed at the
	beginning of this article.
	
	MORE INFORMATION
	================
	
	Note that this bug is not a duplicate of the issue that is described in the
	following Knowledge Base article:
	
	  Q294842 PRB: Error When You Update or Delete New Rows in Access 97 Table
	
	The same error message occurs with Access 97 databases because ADO does not
	retrieve the AutoNumber values correctly for newly-added records. The bug that
	is described in the present article occurs with later versions of Access
	(including Access 2002), and the AutoNumber primary key values for newly-added
	records are present in the recordset.
	
	Steps to Reproduce Behavior
	---------------------------
	
	1. Create an empty Access database named db1.mdb in a folder that you intend to
	  use for this test.
	
	2. Create a new Standard EXE project in Visual Basic. Form1 is created by
	  default.
	
	3. If necessary, add the ADO data control and DataGrid to the toolbox.
	
	4. Add an ADODC, a DataGrid, and six Command buttons to Form1.
	
	5. Paste the following code into the code module of Form1:
	
	  Option Explicit
	
	  Private Sub Command1_Click()
	      Dim cn As ADODB.Connection
	      Dim strCreate
	      Set cn = New ADODB.Connection
	      cn.Open "Provider=Microsoft.Jet.OLEDB.4.0;" & _
	          "Data Source=" & App.Path & "\db1.mdb"
	      On Error Resume Next
	      cn.Execute "DROP TABLE InsertTest", , adExecuteNoRecords
	      On Error GoTo 0
	      strCreate = "CREATE TABLE InsertTest (TestID int identity not null primary key," & _
	                  "TestValue int default 0, TestOther varchar(16))"
	      Debug.Print strCreate
	      cn.Execute strCreate, , adExecuteNoRecords
	      cn.Execute "INSERT INTO InsertTest (TestValue, TestOther) VALUES (1, 'John')"
	      cn.Execute "INSERT INTO InsertTest (TestValue, TestOther) VALUES (2, 'Mary')"
	      cn.Close
	      Set cn = Nothing
	  End Sub
	
	  Private Sub Command2_Click()
	      Dim cn As ADODB.Connection
	      Dim strCreate
	      Set cn = New ADODB.Connection
	      cn.Open "Provider=Microsoft.Jet.OLEDB.4.0;" & _
	          "Data Source=" & App.Path & "\db1.mdb"
	      On Error Resume Next
	      cn.Execute "DROP TABLE InsertTest", , adExecuteNoRecords
	      On Error GoTo 0
	      strCreate = "CREATE TABLE InsertTest (TestID int identity not null primary key," & _
	                  "TestValue int, TestOther varchar(16))"
	      Debug.Print strCreate
	      cn.Execute strCreate, , adExecuteNoRecords
	      cn.Execute "INSERT INTO InsertTest (TestValue, TestOther) VALUES (1, 'John')"
	      cn.Execute "INSERT INTO InsertTest (TestValue, TestOther) VALUES (2, 'Mary')"
	      cn.Close
	      Set cn = Nothing
	  End Sub
	
	  Private Sub Command3_Click()
	      With Adodc1
	          .ConnectionString = "Provider=Microsoft.Jet.OLEDB.4.0;" & _
	              "Data Source=" & App.Path & "\db1.mdb"
	          .RecordSource = "SELECT * FROM InsertTest"
	          .Refresh
	      End With
	      Set DataGrid1.DataSource = Adodc1
	  End Sub
	
	  Private Sub Command4_Click()
	      With Adodc1.Recordset
	          .AddNew
	          .Fields("TestOther").Value = "Joe"
	          .Update
	          .Fields("TestValue").Value = 1
	          .Update
	      End With
	  End Sub
	
	  Private Sub Command5_Click()
	      With DataGrid1
	          .Row = Adodc1.Recordset.RecordCount
	          .Columns(2).Value = "Jane"
	          .Row = .Row - 1
	          .Row = .Row + 1
	          .Columns(1).Value = 123
	          .Row = .Row - 1
	      End With
	      Set DataGrid1.DataSource = Adodc1
	  End Sub
	
	  Private Sub Command6_Click()
	      Set DataGrid1.DataSource = Nothing
	      DataGrid1.ClearFields
	      With Adodc1.Recordset
	          .AddNew
	          .Fields("TestOther").Value = "Joe"
	          .Update
	          .Fields("TestValue").Value = 1
	          .Update
	      End With
	      MsgBox "Update completed."
	  End Sub
	
	  Private Sub Form_Load()
	      Command1.Caption = "Create Table with Default"
	      Command2.Caption = "Create Table without Default"
	      Command3.Caption = "Load Recordset"
	      Command4.Caption = "Test Recordset Update"
	      Command5.Caption = "Test Grid Cell Update"
	      Command6.Caption = "Test Update without Grid"
	      DataGrid1.AllowAddNew = True
	  End Sub
	
	6. Run the project. Click Create Table with Default, click Load Recordset, and
	  then click Test Recordset Update. This updates the numeric field in a
	  newly-added record in the ADODC recordset. It raises run-time error
	  -2147217864 (80040e38), which is followed by a DataGrid error. Both of these
	  errors contain the following message:
	
	  Row cannot be located for updating. Some values may have changed since it was
	  last read.
	
	7. Run the project again. Click Create Table with Default, click Load Recordset,
	  and then click Test Grid Cell Update. This updates the DataGrid cell that
	  corresponds to the numeric field in a newly-added record in the ADODC
	  recordset. It raises run-time error 6153, which is followed by a DataGrid
	  error. Both of these errors contain the following message:
	
	  Row cannot be located for updating. Some values may have changed since it was
	  last read.
	
	8. Run the project again. Click Create Table with Default, click Load Recordset,
	  and then click Test Update without Grid. This updates the numeric field in a
	  newly-added record in the ADODC recordset without using the DataGrid. It
	  raises only the run-time error -2147217864 (80040e38), which displays the
	  following message:
	
	  Row cannot be located for updating. Some values may have changed since it was
	  last read.
	
	9. Run the project again. Click Create Table without Default, click Load
	  Recordset, and then click each of the last three buttons. In each case, the
	  newly-added record is successfully updated because the default value is no
	  longer specified on the problem numeric field in the Access table.
	
	Additional query words: adodc datagrid 6153 80040e38 -2147217864 runtime
	
	======================================================================
	Keywords          : _IK_kbATM kbDataBinding kbJET kbGrpDSVBDB kbGrpDSMDAC kbDSupport 
	Technology        : kbVBSearch kbAudDeveloper kbZNotKeyword6 kbZNotKeyword2 kbVB600Search kbVB600
	Version           : :6.0
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
