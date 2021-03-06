---
layout: page
title: "Q189083: WD97: Automatically Saving Current Work (Open Document)"
permalink: /kb/189/Q189083/
---

## Q189083: WD97: Automatically Saving Current Work (Open Document)

{% raw %}

	Article: Q189083
	Product(s): Word 97 for Windows
	Version(s): WINDOWS:97
	Operating System(s): 
	Keyword(s): kbdta
	Last Modified: 14-NOV-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Word 97 for Windows 
	-------------------------------------------------------------------------------
	
	
	SUMMARY
	=======
	
	Microsoft Word does not have built-in functionality that allows you to
	automatically perform a full save of the current document at specific intervals.
	Instead, Word uses a separate AutoRecover file to prevent data loss.
	
	This article explains why the AutoRecover file method is more effective than
	automatic full saves.
	
	NOTE: While it is possible to write a macro that will save your document at
	regular intervals, this is neither recommended nor supported.
	
	MORE INFORMATION
	================
	
	How the AutoRecover Feature Works
	---------------------------------
	
	When you enable the "Save AutoRecover info every" option (click Options on the
	Tools menu, and click the Save tab), Word creates a temporary AutoRecover file
	which includes the latest changes in your document. This file is updated at the
	end of each preset period.
	
	This AutoRecover file is created so that it will be available when Word is
	restarted after a crash. Each time Word is started, it searches your computer
	for these temporary AutoRecover files and automatically opens them. When Word
	successfully recovers a file, the file is displayed, and the document title bar
	displays the file name of the document as "<file name> (Recovered)." You
	can save the file at this time to permanently preserve your work or save it with
	a new name using the Save As command on the File menu.
	
	Why a Separate AutoRecover File Is Better Than an Automatic Full Save
	---------------------------------------------------------------------
	
	When you perform a full save of your file, there is no way to go back to your
	original version. If the document were to be saved automatically, then there
	would be many instances where data would be lost because a full save is
	irreversible. In contrast, AutoRecover does not overwrite your original file:
	this allows you to back out of most errors simply by not saving changes when you
	close the file. An AutoRecover file is created or updated each time there are
	changes that have not been saved at the end of the preset time period. You
	should perform a full save specifically based on progress you've made in your
	document rather than arbitrarily at regular time intervals.
	
	How to Manually Save a File
	---------------------------
	
	At any time during an editing session, it is possible to save your file using a
	keystroke (CTRL+S), by clicking the save button on the Standard toolbar, or by
	clicking Save on the File menu. All of these options will save the file and then
	delete the temporary AutoRecover file.
	
	If you forget to save your work prior to closing the Word program, you are
	reminded that the work has not been saved and you are given the opportunity to
	save or not save. Either option clears the temporary AutoRecover file. Doing it
	this way, you are protected in case of crashes, power failures, and so on.
	
	Another way to protect your work and maintain all of your changes is to use the
	Versions option on the File menu.
	
	In Word, for more information about the AutoRecover feature, click the Office
	Assistant, type "Prevent loss of work and recover lost documents" click Search,
	and then click " Prevent loss of work and recover lost documents."
	
	NOTE: If the Assistant is hidden, click the Office Assistant button on the
	Standard toolbar. If Word Help is not installed on your computer, please see the
	following article in the Microsoft Knowledge Base:
	
	  Q120802 Office: How to Add/Remove a Single Office Program or Component
	
	Additional query words: 8.00 autosave office8 office97 schedule timed word8 word97
	
	======================================================================
	Keywords          : kbdta 
	Technology        : kbWordSearch kbWord97 kbWord97Search kbZNotKeyword2
	Version           : WINDOWS:97
	Issue type        : kbinfo
	
	=============================================================================
	

{% endraw %}
