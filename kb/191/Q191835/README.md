---
layout: page
title: "Q191835: PRB: Enumerated Data Types in DBGRID32.OCX"
permalink: /kb/191/Q191835/
---

## Q191835: PRB: Enumerated Data Types in DBGRID32.OCX

{% raw %}

	Article: Q191835
	Product(s): Microsoft Visual Basic for Windows
	Version(s): 
	Operating System(s): 
	Keyword(s): kbGrpDSVB
	Last Modified: 11-JAN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual Basic Learning Edition for Windows, versions 5.0, 6.0 
	- Microsoft Visual Basic Professional Edition for Windows, versions 5.0, 6.0 
	- Microsoft Visual Basic Enterprise Edition for Windows, versions 5.0, 6.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When using the Microsoft Data Bound Grid Control (DBGRID32.OCX) in Visual Basic,
	one of two symptoms can occur:
	
	1. The autolist may not drop down enumerated types for some declared
	  properties.
	
	  -or-
	
	2. In the Object Browser, some enumerated types cannot be viewed because they
	  are hidden.
	
	CAUSE
	=====
	
	The enum data types for the Data Bound Grid Control are defined in the Type
	Library. The constants defined in the those enum data types are hidden;
	therefore, you cannot view the contents of the enum datatypes.
	
	RESOLUTION
	==========
	
	If you are declaring a variable as:
	
	     Dim x As enumSplitSizeModeConstants
	
	then this should be modified to read:
	
	     Dim x As SplitSizeModeConstants
	
	STATUS
	======
	
	This behavior is by design.
	
	MORE INFORMATION
	================
	
	Although the Microsoft Data Bound Grid Control (DBGRID32.OCX) ships with Visual
	Basic 6.0, a new control called the Microsoft DataGrid Control 6.0
	(MSDATGRD.OCX) is also included with Visual Basic 6.0. This new control does not
	exhibit the above-mentioned behavior.
	
	Steps to Reproduce the Autolist Drop Down Behavior
	--------------------------------------------------
	
	1. Start Visual Basic and open a Standard EXE project. Form1 is created by
	  default.
	
	2. Under the Project menu, select Components. A dialog will be shown that lists
	  all the available controls. In the Controls tab, check the "Microsoft Data
	  Bound Grid Control" (DBGRID32.OCX), then click OK. The control will be added
	  to the Visual Basic components toolbar.
	
	3. Add a DBGrid control to Form1.
	
	4. In any event procedure, type the following code:
	
	        Dim x As enumSplitSizeModeConstants
	
	5. When you type "x =" you will notice that the autolist box does not appear as
	  expected.
	
	6. Now, change the DIM statement above to:
	
	        Dim x As SplitSizeModeConstants
	   
	
	7. Notice that when you type "x =" you get a list of enumerated types.
	
	Steps to Reproduce the Hidden Type in Object Browser Behavior
	-------------------------------------------------------------
	
	1. Start Visual Basic and open a Standard EXE project. Form1 is created by
	  default.
	
	2. Add the "Microsoft Data Bound Grid Control" (DBGRID32.OCX) to the Visual
	  Basic components toolbar.
	
	3. From the View Menu, select Object Browser or Press the F2 key.
	
	4. Select MSDBGrid from the Project/Library drop-down list box.
	
	5. Under the Classes list box, select Split.
	
	6. Under the Members of "Split" list box, select SizeMode.
	
	7. You will see in the bottom frame that SizeMode is declared as
	  enumSplitSizeModeConstants.
	
	8. Click on enumSplitSizeModeConstants. Visual Basic will display the message,
	  "Cannot jump to 'enumSplitSizeModeConstants' because it is hidden."
	
	Additional query words: kbDSupport kbDSD kbVBp kbVBp500 kbVBp600 kbCtrl
	
	======================================================================
	Keywords          : kbGrpDSVB 
	Technology        : kbVBSearch kbAudDeveloper kbZNotKeyword6 kbZNotKeyword2 kbVB500Search kbVB600Search kbVBA500 kbVBA600 kbVB500 kbVB600
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
