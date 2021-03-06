---
layout: page
title: "Q157531: WD97: Table of Figures (TOF) Missing Captions from Text Boxes"
permalink: /kb/157/Q157531/
---

## Q157531: WD97: Table of Figures (TOF) Missing Captions from Text Boxes

{% raw %}

	Article: Q157531
	Product(s): Word 97 for Windows
	Version(s): WINDOWS:97
	Operating System(s): 
	Keyword(s): kberrmsg kbualink97 word97
	Last Modified: 14-NOV-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Word 97 for Windows 
	-------------------------------------------------------------------------------
	
	
	SYMPTOMS
	========
	
	When you create or update a table of figures, the resulting table of figures may
	be missing some entries. If Word finds no entries to use in the table of
	figures, the following error message appears:
	
	  Error! No table of figures entries found.
	
	CAUSE
	=====
	
	When Word builds a table of figures, it does not look at the drawing layer for
	SEQ (Caption) fields to include in the table of figures. Word only looks in the
	text layer.
	
	Captions are inserted into text boxes if the object you wish to caption is a
	floating abject. Textboxes are located in the drawing layer. Therefore, any
	captions that appear in text boxes will be ignored when the table of figures is
	built or updated.
	
	WORKAROUND
	==========
	
	To insert captions so that they are included in a table of figures, use one of
	the following methods.
	
	Method 1: If the Figures and Caption Are Not Already in the Document
	--------------------------------------------------------------------
	
	1. On the Insert menu, point to Picture, and then click From File.
	
	2. In the Insert Picture dialog box, click the picture you want, click to clear
	  the Float Over text check box, and then click Insert.
	
	3. Click the picture to select it.
	
	  You should see the black, square sizing handles around it.
	
	4. On the Insert menu, click Caption.
	
	5. Type the text for the caption, and then click OK.
	
	6. Insert or update your table of figures.
	
	Method 2: If the Picture Is in the Document, but the Caption Is Not
	-------------------------------------------------------------------
	
	1. Click the picture to select it.
	
	  You should see the black, square sizing handles around it.
	
	2. On the Format menu, click Picture.
	
	3. Click the Position tab.
	
	4. Click to clear the Float Over text check box, and then click OK.
	
	5. On the Insert menu, click Caption.
	
	6. Type the text for the caption, and then click OK.
	
	7. Insert or update your table of figures.
	
	Method 3: If the Caption Is Already in the Document
	---------------------------------------------------
	
	1. Click the Caption.
	
	  The text box containing the caption should be selected, and you should see the
	  black sizing handles.
	
	2. On the Format menu, click Text Box.
	
	3. Click the Text Box tab.
	
	4. Click Convert To Frame. Note that the following message appears:
	
	  When you convert this drawing object to a frame, some of the drawing object's
	  formatting may be lost. Do you want to continue?
	
	5. Click OK.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in the Microsoft products that are
	listed at the beginning of this article.
	
	MORE INFORMATION
	================
	
	In earlier versions of Microsoft Word, the insertion of a caption in a text box
	was disabled.
	
	Additional query words:
	
	======================================================================
	Keywords          : kberrmsg kbualink97 word97 
	Technology        : kbWordSearch kbWord97 kbWord97Search kbZNotKeyword2
	Version           : WINDOWS:97
	Hardware          : x86
	Issue type        : kbbug
	
	=============================================================================
	

{% endraw %}
