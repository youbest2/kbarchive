---
layout: page
title: "Q171980: HOWTO: Play MIDI Files Using API Functions"
permalink: /kb/171/Q171980/
---

## Q171980: HOWTO: Play MIDI Files Using API Functions

{% raw %}

	Article: Q171980
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
	- Microsoft Visual Basic Control Creation Edition for Windows, version 5.0 
	- Microsoft Visual Basic Learning Edition for Windows, version 5.0 
	- Microsoft Visual Basic Professional Edition for Windows, version 5.0 
	- Microsoft Visual Basic Enterprise Edition for Windows, version 5.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	This article demonstrates how to play a MIDI (.MID) file from Visual Basic using
	the WIN 32 API call named mciSendString.
	
	NOTE: You can use the MCI control to play a MIDI file; you don't need to use the
	APIs.
	
	MORE INFORMATION
	================
	
	Step-by-Step Example
	--------------------
	
	1. Start Visual Basic, or if Visual Basic is already running, click New Standard
	  EXE Project on the File menu (ALT, F, N). Form1 is created by default.
	
	2. Add a CommandButton (Command1) to Form1.
	
	3. Add the following code to the Command1_Click event of Form1:
	
	        Private Sub Command1_Click()
	        Dim ret As Integer
	
	           ' The following will open the sequencer with the CANYON.MID
	           ' file. Canyon is the device_id.
	
	           ret = mciSendString( _
	             "open " & Song & " type sequencer alias canyon", _
	             0&, 0, 0)
	
	           ' The wait tells the MCI command to complete before returning
	           ' control to the application.
	
	           ret = mciSendString("play canyon wait", 0&, 0, 0)
	
	           ' Close CANYON.MID file and sequencer device
	
	           ret = mciSendString("close canyon", 0&, 0, 0)
	
	        End Sub
	
	4. Add the following code to the General Declarations section of Form1.
	
	        Private Declare Function mciSendString Lib "winmm.dll" Alias _
	           "mciSendStringA" (ByVal lpstrCommand As String, ByVal  _
	           lpstrReturnString As Any, ByVal uReturnLength As Long, ByVal _
	           hwndCallback As Long) As Long
	
	        ' Modify the value of the constant "Song" with your path
	              ' to "canyon.mid".
	              Private Const Song As String = "C:\Windows\Media\Canyon.MID"
	
	5. On the Run menu, click Start (ALT, R, S) or press the F5 key to run the
	  program.
	
	REFERENCES
	==========
	
	Microsoft Developer Network Library, Platform SDK, Reference, Multimedia
	Commands.
	
	For additional information about playing MIDI files using API calls from Visual
	Basic 4.0, please see the following article in the Microsoft Knowledge Base:
	
	  Q141756 : HOWTO: Play MIDI Files Using API Calls from Visual Basic
	
	Additional query words: kbVBp kbdsd kbDSupport kbVBp500 kbVBp600 KBAPI
	
	======================================================================
	Keywords          : kbGrpDSVB 
	Technology        : kbVBSearch kbAudDeveloper kbZNotKeyword6 kbZNotKeyword2 kbVB500Search kbVB600Search kbVBA500Search kbVBA500 kbVBA600 kbVB500 kbVB600 kbZNotKeyword3
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
