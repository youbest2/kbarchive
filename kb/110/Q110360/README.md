---
layout: page
title: "Q110360: How to Select Custom Page Sizes in FoxPro for Macintosh"
permalink: /kb/110/Q110360/
---

## Q110360: How to Select Custom Page Sizes in FoxPro for Macintosh

{% raw %}

	Article: Q110360
	Product(s): Microsoft FoxPro
	Version(s): MACINTOSH:2.5b,3.0b
	Operating System(s): 
	Keyword(s): 
	Last Modified: 05-FEB-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft FoxPro for Macintosh, version 2.5b 
	- Microsoft Visual FoxPro for Macintosh, version 3.0b 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	The FoxPro for Macintosh Report Writer does not allow the selection of custom
	page sizes, regardless of the type of printer selected. In FoxPro for Windows,
	this functionality is available if the printer driver selected allows the use of
	custom page sizes. To add this functionality to FoxPro for Macintosh, see the
	information below.
	
	MORE INFORMATION
	================
	
	WARNING: ANY USE BY YOU OF THE INFORMATION PROVIDED IN THIS ARTICLE IS AT YOUR
	OWN RISK. Microsoft provides this information "as is" without warranty of any
	kind, either expressed or implied, including but not limited to the implied
	warranties of merchantability and/or fitness for a particular purpose.
	
	You can edit the FoxPro for Macintosh resource file to add this functionality.
	The following information is excerpted from the FoxPro ReadMe file shipped with
	FoxPro for Macintosh.
	
	Changing Paper Sizes for the ImageWriter
	----------------------------------------
	
	To change paper sizes for the ImageWriter printer, you need to adjust the FoxPro
	for Macintosh resource file. Information about paper sizes is stored in the PREC
	resource of FoxPro and is accessed through the Page Setup dialog box.
	
	Custom page sizes are not available with all printer drivers. For example, you
	cannot change the paper size used by a LaserWriter.
	
	To add a custom paper size option to the Page Setup dialog box:
	
	1. Quit FoxPro for Macintosh.
	
	2. Open FoxPro for Macintosh in a resource editor (such as ResEdit).
	
	3. Open the PREC resource.
	
	4. Open the ID number 4.
	
	5. In the field labeled "Number of Btns," change the number from 5 to 6.
	
	6. In the fields labeled "Btn 6 Height" and "Btn 6 Width," enter the height and
	  width of the new paper size. Each number represents 1/120th of an inch. For
	  example, an 8.5-by-11-inch paper size has a height of 1320 and a width of
	  1020.
	
	7. In the field labeled "Btn 6 Name," add a descriptive name to appear next to
	  the button.
	
	8. Save your changes and exit the resource editor.
	
	To use the custom paper size option:
	
	1. Select an ImageWriter printer with the Macintosh Chooser.
	
	2. Start FoxPro.
	
	3. From the File menu, choose Page Setup.
	
	4. Choose the custom paper size.
	
	NOTE: FoxPro adds a .5-inch margin to the top of all documents printed with an
	ImageWriter. To remove this margin, select the No Gaps Between Pages check box
	in the Page Setup dialog box.
	
	Additional query words: VFoxMac FoxMac mailmerge text
	
	======================================================================
	Keywords          :  
	Technology        : kbHWMAC kbOSMAC kbVFPsearch kbAudDeveloper kbFoxproSearch kbFoxPro250bMac kbVFP300bMac
	Version           : MACINTOSH:2.5b,3.0b
	
	=============================================================================
	

{% endraw %}
