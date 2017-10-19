---
layout: page
title: "Q159426: XCLN: How to Write Listbox Items to an E-form Package"
permalink: kb/159/Q159426/
---

## Q159426: XCLN: How to Write Listbox Items to an E-form Package

	Article: Q159426
	Product(s): Microsoft Exchange
	Version(s): WINDOWS:4.0,5.0
	Operating System(s): 
	Keyword(s): kbusage
	Last Modified: 12-APR-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Windows 95/98 client, versions 4.0, 5.0 
	- Microsoft Exchange Windows 3.x client, versions 4.0, 5.0 
	- Microsoft Exchange Windows NT client, versions 4.0, 5.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	When you use the Microsoft Exchange 4.0 Electronic Forms Designer to create a
	custom E-form that has a listbox, you can set the initial content of the listbox
	by double-clicking the listbox to open up a Field Properties dialog box,
	choosing the Initial Value tab, and setting the list items for the listbox.
	
	But sometimes you may want to have an initially blank listbox and have the E-form
	sender dynamically add or remove the list items. In this case, you have to
	modify the Visual Basic code generated by the E-form Designer to write the
	content of the listbox to the E-form package. Otherwise, the receiver of the
	E-form will receive a blank listbox. This article illustrates the techniques of
	writing the listbox items to an E-form package.
	
	MORE INFORMATION
	================
	
	1. Use the Microsoft Exchange E-form Designer Wizard to generate an one- window
	  electronic form called List.efp. Add a listbox to the E-form. Compile and
	  install the form. This will generate a 16-bit Visual Basic project called
	  List.vbp.
	
	2. Load List.vbp into a 16-bit version of Visual Basic.
	
	3. Add a Command button, Command1, to Window1.Frm. In the click event, populate
	  the list box:
	
	        Private Sub Command1_Click()
	            Dim i As Integer
	            For i = 0 To 10
	                ListBox1_Ctrl.AddItem "Item " & i
	            Next i
	        End Sub
	
	4. Add a public function to Window1.Frm to write the list items of ListBox1_Ctrl
	  into a single Visual Basic Variant type variable:
	
	  Public Function CreateVariant() As Variant
	            Dim varRet As Variant
	            Dim strTemp() As String
	            ReDim strTemp(ListBox1_Ctrl.ListCount) As String
	            Dim i As Integer
	            For i = 0 To ListBox1_Ctrl.ListCount - 1
	                strTemp(i) = ListBox1_Ctrl.List(i)
	            Next i
	            CreateVariant = strTemp 'store an array into a variant
	        End Function
	
	5. Remove the ListBox1_Ctrl_Click() procedure from the Window1.Frm.
	
	6. In the Window_Store procedure of the Window1.Frm, add the following
	  statement
	
	        ListBox1_Ctrl_Val = CreateVariant
	
	  before the following statement
	
	        Call SetMapiProp(ctlSubject.Text, "MAPI_Subject_Custom",vbString, Msg)
	
	7. In the Window_Load procedure, comment out the following statement:
	
	        If (VarType(varTemp) And vbArray) = vbArray Then varTemp = varTemp(0)
	
	8. Change the SetListBoxValue subroutine in the Global.bas to the following:
	
	        Public Sub SetListBoxValue(ByVal var As Variant, ctl As Control, _
	           inType As Integer)
	            Dim Index As Integer
	            Dim lstMost As Integer
	
	            If IsNull(var) Then Exit Sub
	            If VarType(var) < vbArray Then Exit Sub
	            ctl.Clear
	            lstMost = UBound(var)
	            For Index = 0 To lstMost - 1
	                ctl.AddItem var(Index)
	            Next Index
	
	        End Sub
	
	9. Rebuild the executable file and install it.
	
	To test the newly installed E-form , the sender loads the form using the
	Microsoft Exchange client. The sender first clicks the Command1 button to
	populate the listbox and then click the Send button. When the receiver opens up
	the received form, the list items of the listbox are received.
	
	
	Additional query words: Eforms VB Eform
	
	======================================================================
	Keywords          : kbusage 
	Technology        : kbExchangeSearch kbExchange500 kbExchange400 kbExchangeClientSearch kbZNotKeyword kbZNotKeyword2 kbZNotKeyword3 kbExchange400NT kbExchange500NT kbExchange400Win95 kbExchange500Win95
	Version           : WINDOWS:4.0,5.0
	Issue type        : kbhowto
	
	=============================================================================
	