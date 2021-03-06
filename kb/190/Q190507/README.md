---
layout: page
title: "Q190507: BUG: No Incompatibility Error When Interface Changes"
permalink: /kb/190/Q190507/
---

## Q190507: BUG: No Incompatibility Error When Interface Changes

{% raw %}

	Article: Q190507
	Product(s): Microsoft Visual Basic for Windows
	Version(s): 
	Operating System(s): 
	Keyword(s): kbGrpDSVB
	Last Modified: 11-JAN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual Basic Learning Edition for Windows, version 6.0 
	- Microsoft Visual Basic Professional Edition for Windows, version 6.0 
	- Microsoft Visual Basic Enterprise Edition for Windows, version 6.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	If an ActiveX DLL project has a subroutine that takes a class in another ActiveX
	DLL as its parameter, modifying the class will not generate an incompatibility
	error when the project runs in the design environment, even though the class is
	set to be binary compatible.
	
	CAUSE
	=====
	
	While compiling a project that references an ActiveX DLL that has been modified,
	Visual Basic will replace the reference to the old DLL with the one to the new
	DLL. After that, it compiles the project and replaces the reference back to the
	old DLL. However, while running the project in design environment, this
	reference replacement does not occur since no compilation is done. Therefore the
	expected incompatibility error only occurs in compilation but not in the design
	environment.
	
	
	RESOLUTION
	==========
	
	Compiling the DLL corrects this behavior.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a bug in the Microsoft products listed at the
	beginning of this article. We are researching this bug and will post new
	information here in the Microsoft Knowledge Base as it becomes available.
	
	MORE INFORMATION
	================
	
	Steps to Reproduce Behavior
	---------------------------
	
	1. Start a new ActiveX DLL project in Visual Basic. Class1 is created by
	  default.
	
	2. Select Project1 Properties from the Project menu and change the Project Name
	  to "TestApp1."
	
	3. Paste the following code into Class1:
	
	        Public Sub TestMethod1()
	        End Sub
	
	4. Select Make TestApp1.dll from the File menu, and compile the DLL.
	
	5. Select TestApp1 Properties from the Project menu, and select the Binary
	  Compatibility option on the Component tab.
	
	6. Select Add Project from the File menu, and add another ActiveX DLL project to
	  the project group. Repeat step 2 and change its name to "TestApp2."
	
	7. Select References from the Project menu, and check the reference to TestApp1.
	
	8. Paste the following code into Class1 of TestApp2:
	
	        Public Sub A(obj As TestApp1.Class1)
	        End Sub
	
	9. Select Make TestApp2.dll from the File menu, and compile the DLL.
	
	10. Repeat step 5 to set Binary Compatibility for TestApp2.dll.
	
	11. In the Project Group Window, right-click on TestApp2, and choose Set As
	  Start Up.
	
	12. Paste the following code into Class1 of TestApp1:
	
	        Public Sub TestMethod2()
	        End Sub
	
	13. Select Make TestApp1.dll from the File menu. When prompted for a name,
	  change it to TestApp3. Click OK.
	
	14. Press the F5 key to run the project.
	
	15. When the Project Properties dialog for TestApp2 appears, leave the default
	  option selected, and click OK. TestApp2 starts up correctly, although it is
	  referencing TestApp1 ,which has been replaced by TestApp3. No
	  incompatibility error is reported.
	
	Additional query words: kbdss kbDSupport kbVBp kbVBp600bug kbActiveX kbAutomation
	
	======================================================================
	Keywords          : kbGrpDSVB 
	Technology        : kbVBSearch kbAudDeveloper kbZNotKeyword6 kbZNotKeyword2 kbVB600Search kbVBA600 kbVB600
	Issue type        : kbbug
	
	=============================================================================
	

{% endraw %}
