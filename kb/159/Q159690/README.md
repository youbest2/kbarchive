---
layout: page
title: "Q159690: PRB: Problem Adding Objects Created in VBA to SourceSafe"
permalink: /kb/159/Q159690/
---

## Q159690: PRB: Problem Adding Objects Created in VBA to SourceSafe

{% raw %}

	Article: Q159690
	Product(s): Microsoft SourceSafe
	Version(s): 97
	Operating System(s): 
	Keyword(s): kbinterop
	Last Modified: 01-JUL-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Access 97 
	-------------------------------------------------------------------------------
	
	Moderate: Requires basic macro, coding, and interoperability skills.
	
	SYMPTOMS
	========
	
	If you are developing a database application that is under Source Code Control
	(SCC) using Microsoft Visual SourceSafe integration, and you create a database
	object programmatically using Visual Basic for Applications code, you are not
	prompted to add the new object to SCC control. When you try to add the new
	object manually, you receive a message that there are no objects to add to
	Visual SourceSafe.
	
	CAUSE
	=====
	
	When you create the new object programmatically, Microsoft Access 97 fails to
	notify the SCC integration that a new object exists. This causes a situation
	where you cannot add the new object to SCC control until you close and reopen
	the database.
	
	RESOLUTION
	==========
	
	Close and reopen the database after you create new objects programmatically
	under Source Code Control (SCC). This allows the new objects to be added to SCC
	correctly.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Microsoft Access 97. We are
	researching this problem and will post new information here in the Microsoft
	Knowledge Base as it becomes available.
	
	MORE INFORMATION
	================
	
	Steps to Reproduce Behavior
	---------------------------
	
	To demonstrate the issue and how it affects a form that you create
	programmatically, follow these steps.
	
	NOTE: The steps in this example require you to install Microsoft Visual
	SourceSafe.
	
	1. Create a new database.
	
	2. Create a module and type the following procedure to create a new form with a
	  class module:
	
	        Function ClickEventProcForm()
	           Dim frm As Form, ctl As Control, mdl As Module
	           Dim lngReturn As Long
	           On Error GoTo Error_ClickEventProcForm
	           Set frm = CreateForm
	           Set ctl = CreateControl(frm.Name, acCommandButton, , , , 1000, _
	              1000)
	           ctl.Caption = "Click here"
	           Set mdl = frm.Module
	           lngReturn = mdl.CreateEventProc("Click", ctl.Name)
	           mdl.InsertLines lngReturn + 1, vbTab & "MsgBox ""Way cool!"""
	           DoCmd.Close acForm, frm.Name, acSaveYes
	           ClickEventProcForm = True
	        Exit_ClickEventProcForm:
	           Exit Function
	        Error_ClickEventProcForm:
	           MsgBox Err & " :" & Err.Description
	           ClickEventProcForm = False
	           Resume Exit_ClickEventProcForm
	        End Function
	
	3. Add the database to SourceSafe Source Code Control.
	
	4. To test this function, type the following line in the Debug window, and then
	  press ENTER.
	
	        ?ClickEventProcForm()
	
	5. On the Tools menu, point to SourceSafe and then click Add Objects to
	  SourceSafe. Note that you receive a message that there are no objects to add
	  to the VSS database.
	
	6. Close the database, and then reopen it.
	
	7. On the Tools menu, point to SourceSafe and then click Add Objects to
	  SourceSafe. Note that you can add Form1 to Source Code Control.
	
	Additional query words: SCC ACCSCC
	
	======================================================================
	Keywords          : kbinterop 
	Technology        : kbAccessSearch kbAccess97 kbAccess97Search
	Version           : 97
	Hardware          : x86
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
