---
layout: page
title: "Q259519: PRB: Image Control Invisible When Visible Property Set to True"
permalink: /kb/259/Q259519/
---

## Q259519: PRB: Image Control Invisible When Visible Property Set to True

{% raw %}

	Article: Q259519
	Product(s): Microsoft Visual Basic for Windows
	Version(s): 3.0
	Operating System(s): 
	Keyword(s): kbGrpDSVB kbDSupport kbOSWinCE300
	Last Modified: 20-JAN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft eMbedded Visual Basic, version 3.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When you place an Image control on a form and set its Visible property to True,
	the control seems to stay invisible after you run the application in emulation
	and on the device.
	
	CAUSE
	=====
	
	The problem occurs because the Form and the Image control have the same default
	background color. The Visible property of the Image control is actually working.
	
	RESOLUTION
	==========
	
	To resolve the problem, change the background color of the Form. However, this
	solution only works for the Palm-size PC and the Handheld PC/Pro. On the Pocket
	PC, if you change the background color of the Form, it still does not show the
	Image control although its Visible property is actually True. To solve this, you
	can assign its Picture property to a bitmap and the Image control then becomes
	visible.
	
	STATUS
	======
	
	This behavior is by design.
	
	MORE INFORMATION
	================
	
	Steps to Reproduce Behavior
	---------------------------
	
	1. Start a new eMbedded Visual Basic project. Form1 is created by default.
	
	2. On the Project menu, select Components, and then select Microsoft CE Image
	  Control 3.0.
	
	3. Add an Image control (ImageCtl1) to the form and set its Visible property to
	  False.
	
	4. Add the following code:
	
	  Private Sub Form_Click()
	     MsgBox ImageCtl1.Visible 
	     ImageCtl1.Visible = True
	     MsgBox ImageCtl1.Visible 
	  End Sub
	
	5. Run the project in emulation. Click the Form, and note that the first message
	  box displays False, and the second message box displays True. However, the
	  Image control stays invisible.
	
	Additional query words:
	
	======================================================================
	Keywords          : kbGrpDSVB kbDSupport kbOSWinCE300 
	Technology        : kbVBSearch kbAudDeveloper kbZNotKeyword2 kbVBeMbSearch kbVBeMb300
	Version           : :3.0
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
