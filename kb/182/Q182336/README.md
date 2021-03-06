---
layout: page
title: "Q182336: WD97: Lists in Word Cause Numbering Problems When Saved As RTF"
permalink: /kb/182/Q182336/
---

## Q182336: WD97: Lists in Word Cause Numbering Problems When Saved As RTF

{% raw %}

	Article: Q182336
	Product(s): Word 97 for Windows
	Version(s): 
	Operating System(s): 
	Keyword(s): kbdta kbconversion word97 kbnumbering
	Last Modified: 13-MAY-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Word 97 for Windows 
	-------------------------------------------------------------------------------
	
	
	SYMPTOMS
	========
	
	When you save a document in Rich Text Format (RTF) in Microsoft Word 97 for
	Windows to generate Help (.hlp) files with the Microsoft Help Compiler, unwanted
	line numbering may precede paragraphs in the help source file. The document does
	not show these line numbers in Word 97.
	
	CAUSE
	=====
	
	This problem occurs in Word when you choose to continue a previous list, but
	there are non-list paragraphs between the two lists. The list can be either a
	bulleted or a numbered list.
	
	Word places RTF codes after the first list which indicates that line numbering
	should continue silently, as in the example below:
	
	     {\*\pn \pnlvlcont\ilvl0\ls0\pnrnot0\pndec }
	
	The codes in the example above specify the following:
	
	
	     \pnlvlcont = continue line numbering but silently (don't display on
	     screen)
	
	     \ls0 = the list id that should be continued
	
	     \pndec = the list is decimal (1,2,3)
	
	However, these codes are unnecessary. Word relies on the list id (/ls#) to
	determine whether a list should continue a previous list. When you take those
	codes out of the RTF file, Word still renders the file correctly. Hence, the
	additional RTF codes cause the Help compiler to place line numbers on every
	paragraph between the two lists.
	
	WORKAROUND
	==========
	
	The Help compiler does not allow you to continue a previous automatically
	numbered list. To generate this effect, turn off automatic numbering. To turn
	off Automatic numbering, follow these steps:
	
	1. On the Format menu, click AutoFormat, and click Options in the AutoFormat
	  dialog box.
	
	2. Click the AutoFormat As You Type tab, and click to clear the Automatic
	  Numbered Lists check box.
	
	3. Click OK twice.
	
	You then have to type in the numbers for the list manually. Note that this is
	only necessary if you have two separate lists, and the second list needs to
	continue numbering where the first list stopped.
	
	NOTE: Because bulleted lists do not provide the option to continue a previous
	list, this situation is more rare. When it occurs it is more difficult to solve,
	because you can not turn off the "continue previous list" option for bullets.
	
	MORE INFORMATION
	================
	
	Microsoft provides programming examples for illustration only, without warranty
	either expressed or implied, including, but not limited to, the implied
	warranties of merchantability and/or fitness for a particular purpose. This
	article assumes that you are familiar with the programming language being
	demonstrated and the tools used to create and debug procedures. Microsoft
	support professionals can help explain the functionality of a particular
	procedure, but they will not modify these examples to provide added
	functionality or construct procedures to meet your specific needs. If you have
	limited programming experience, you may want to contact a Microsoft Certified
	Partner or the Microsoft fee-based consulting line at (800) 936-5200. For more
	information about Microsoft Certified Partners, please visit the following
	Microsoft Web site:
	
	  http://www.microsoft.com/partner/referral/
	
	For more information about the support options that are available and about how
	to contact Microsoft, visit the following Microsoft Web site:
	
	  http://support.microsoft.com/default.aspx?scid=fh;EN-US;CNTACTMS
	
	The following Word 97 code fixes any RTF document where bulleted lists are
	causing the problem. The code cycles through each paragraph. If the current
	paragraph is in a list, it copies the formatting of the list. It then removes
	the list attribute and reapplies it. By default, these actions remove any
	continuation of previous lists. Note that this will cause separate numbered
	lists that were previously continuous to begin renumbering after each break.
	However, since the Help files can not render this type of list, that problem
	will need to be dealt with separately anyway by manually typing in the list
	numbers.
	
	     Sub BulletFix()
	     '
	     ' BulletFix Macro
	     '
	     Dim par As Object
	
	     ' Cycle through all paragraphs in document
	        For Each par In ActiveDocument.Paragraphs
	           ' Select paragraph
	           par.Range.Select
	           ' Save its ListTemplate (its formatting)
	           Dim lt As ListTemplate
	           Set lt = Selection.Range.ListFormat.ListTemplate
	           If TypeName(lt) <> "Nothing" Then
	              Dim FirstLine As Double
	              Dim LeftIndent As Double
	              FirstLine = Selection.ParagraphFormat.FirstLineIndent
	              LeftIndent = Selection.ParagraphFormat.LeftIndent
	
	              ' Remove Bullets/Numbers
	              Selection.Range.ListFormat.RemoveNumbers _
	                 NumberType:=wdNumberParagraph
	              ' Restore the list format
	              Selection.Range.ListFormat.ApplyListTemplate _
	              ListTemplate:=lt, ApplyTo:=wdListApplyToWholeList
	
	              ' Restore Indentation Settings
	              Selection.ParagraphFormat.FirstLineIndent = FirstLine
	              Selection.ParagraphFormat.LeftIndent = LeftIndent
	           End If
	        Next
	     ' Go back to the beginning of the document
	     Selection.HomeKey Unit:=wdStory
	     End Sub
	
	Deleting the problematic RTF codes should be the last option. In this case, keep
	a backup copy of the RTF file (in case the wrong codes are deleted). The file
	could become corrupt and unreadable by Word.
	
	For more information about the Listformat Property, while in the Visual Basic for
	Applications Editor, click the Office Assistant, type "Listformat," click
	Search, and then click to view "Listformat Property."
	
	NOTE: If the Assistant is hidden, click the Office Assistant button on the
	Standard toolbar. If the Assistant is not able to answer your query, please see
	the following article in the Microsoft Knowledge Base:
	
	  Q120802 OFFICE: How to Add/Remove a Single Office Program of Component
	
	For additional information, please see the following article in the Microsoft
	Knowledge Base:
	
	  Q173707 OFF97: How to Run Sample Code from Knowledge Base Articles
	
	
	This problem also occurs with bulleted lists when numbered lists are converted to
	bulleted lists.
	
	Although there is no continuation option for bulleted lists, a bulleted list can
	inherit this behavior from a numbered list. If you look at the RTF code, the
	same problem RTF codes immediately follow the bulleted list, although they
	specify "\pndec" (referring to a numbered list.)
	
	REFERENCES
	==========
	
	For additional information about the Rich Text Format (RTF) Specification,
	please see the following article in the Microsoft Knowledge Base:
	
	  Q86999 WD: Rich Text Format (RTF) Specification 1.6
	
	Additional query words: access devtools developer Help Workshop RTF Numbers Paragraph Acc97
	
	======================================================================
	Keywords          : kbdta kbconversion word97 kbnumbering 
	Technology        : kbWordSearch kbWord97 kbWord97Search kbZNotKeyword2
	Version           : :
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
