---
layout: page
title: "Q260103: FIX: IDE Memory Leak on Form Run/Stop in Visual Basic 6"
permalink: /kb/260/Q260103/
---

## Q260103: FIX: IDE Memory Leak on Form Run/Stop in Visual Basic 6

{% raw %}

	Article: Q260103
	Product(s): Microsoft Visual Basic for Windows
	Version(s): WINDOWS:6.0,6.0 SP4,6.0 sp1, sp2, sp3
	Operating System(s): 
	Keyword(s): kbVBp600 kbVBp600bug kbVS kbVS600 kbVS600bug kbFAQ MSGRAPH kbVBp600FAQ kbVS600sp4fix kb
	Last Modified: 20-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual Basic Professional Edition for Windows, version 6.0 
	- Microsoft Visual Basic Enterprise Edition for Windows, version 6.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When you are programming in Visual Basic 6.0 and you use the following code, the
	code leaks 8 KB per button click as observed from the Windows NT Task Manager.
	
	  Private Sub Command1_Click()
	           For i = 1 To 5
	              Load Winsock1(1)
	              Unload Winsock1(1)
	              DoEvents 'does not cause problem but helps
	                       'to allow idle time so you can stop application.
	           Next i    
	  End Sub
	
	CAUSE
	=====
	
	There is a memory leak in the code and related system files.
	
	RESOLUTION
	==========
	
	Install the latest service pack for Visual Studio 6.0.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a bug in the Microsoft products listed at the
	beginning of this article. This bug was corrected in the latest service pack for
	Visual Studio 6.0.
	
	For additional information about Visual Studio service packs, click the article
	numbers below to view the articles in the Microsoft Knowledge Base:
	
	  Q194022 INFO: Visual Studio 6.0 Service Packs, What, Where, Why
	
	  Q194295 HOWTO: Tell That a Visual Studio Service Pack Is Installed
	
	You can download the latest Visual Studio service pack from the following
	Microsoft Web site:
	
	  Visual Studio Product Updates
	  (http://msdn.microsoft.com/vstudio/downloads/updates.asp)
	
	MORE INFORMATION
	================
	
	NOTE: The integrated development environment (IDE) contains a memory leak on
	Form Run/Stop. This was a previous Winsock control (Service Pack 2) memory leak
	on load/unload.
	
	Additional query words: VSSP4, vssetup
	
	======================================================================
	Keywords          : kbVBp600 kbVBp600bug kbVS kbVS600 kbVS600bug kbFAQ MSGRAPH kbVBp600FAQ kbVS600sp4fix kbVS600sp5fix 
	Technology        : kbVBSearch kbAudDeveloper kbZNotKeyword6 kbZNotKeyword2 kbVB600Search kbVB600
	Version           : WINDOWS:6.0,6.0 SP4,6.0 sp1, sp2, sp3
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
