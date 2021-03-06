---
layout: page
title: "Q110609: How to Use STYLE Clause for @ ... GETs in FoxBASE+/Mac"
permalink: /kb/110/Q110609/
---

## Q110609: How to Use STYLE Clause for @ ... GETs in FoxBASE+/Mac

{% raw %}

	Article: Q110609
	Product(s): Microsoft Fox Miscellaneous Products
	Version(s): MACINTOSH:2.01
	Operating System(s): 
	Keyword(s): 
	Last Modified: 23-OCT-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft FoxBASE+ for Macintosh, version 2.01 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	The @ ... GET command has an optional STYLE clause, which provides a method for
	determining certain characteristics of objects to be displayed to an output
	device. Specifically, the STYLE clause is used to specify the pen pattern, pen
	width, fill pattern, radius, and transfer mode of an object. When a screen is
	generated, the STYLE clause is automatically calculated for all the objects
	created for the screen.
	
	When you are porting a format file created in FoxBASE+ for MS-DOS to the
	Macintosh, it may be more feasible to modify the existing format file to give it
	a Macintosh "look and feel", as opposed to starting from scratch with the
	FoxBASE+/Mac Screen Builder. If you decide to modify the format file, you will
	need to understand how the STYLE clause is calculated. The calculation of this
	clause is explained below.
	
	MORE INFORMATION
	================
	
	The value contained in the STYLE clause affects five different object settings:
	
	  Pen pattern - The shade of a line or box outline.
	  Pen width - The width of a line or box outline.
	  Fill pattern - The shade used to fill box objects.
	  Radius - The amount of curvature in rounded rectangles.
	  Transfer mode - How the current object blends when placed on top of existing
	  objects.
	
	Each setting can have 1 of 16 possible values, with a range of 0 to 15. In
	general, the values are such that the lower numbers correspond to less (for
	example, lighter, thinner, and less curved), and the higher numbers correspond
	to more (for example, darker, thicker, and more curved). All possible values for
	each of the five settings are listed in pages 3-8 through 3-10 of the
	FoxBASE+/Mac "Commands & Functions" manual.
	
	To calculate the STYLE clause, do the following:
	
	1. Choose a value between 0 and 15 for each of the five settings.
	
	2. Perform the following calculations:
	
	  a. Multiply your pen width value by 16.
	
	  b. Multiply your fill pattern value by 256.
	
	  c. Multiply your radius value by 4096.
	
	  d. Multiply your transfer mode value by 65536.
	
	3. Sum together the pen pattern with the newly calculated values for pen width,
	  fill pattern, radius, and transfer mode. The result is the value of the STYLE
	  clause needed to create the desired effect for your object.
	
	The following program demonstrates how the STYLE clause is calculated. The
	formula used to calculate the STYLE clause is shown in the CALCSTYLE procedure
	at the end of this code example.
	
	  *Set up the environment.
	     SCREEN 1 TOP
	     SET TALK OFF
	     filename = SYS(16)
	     SET PROCEDURE to "&filename"
	     CLEAR
	     STORE 0 TO penpat, penwidth, fillpat, radius, xmode
	
	     *Create a plain rectangle with a dark border.
	     penpat = 15                 && 1 is lightest, 15 is darkest
	     penwidth = 1                && 1 is thinnest, 12 is thickest
	     styleval = calcstyle(penpat, penwidth, fillpat, radius, xmode)
	     @ 2,2 TO 4,8 STYLE styleval
	     WAIT "Press any key for a thicker outline..."
	
	     *Make the border thicker.
	     CLEAR
	     penwidth = 6                && make the outline 6 pixels wide
	     styleval = calcstyle(penpat, penwidth, fillpat, radius, xmode)
	     @ 2,2 TO 4,8 STYLE styleval
	     WAIT "Press any key for a gray fill..."
	
	     *Give the box a medium fill.
	     CLEAR
	     fillpat = 6                 && 1 is white, 15 is black
	     styleval = calcstyle(penpat, penwidth, fillpat, radius, xmode)
	     @ 2,2 TO 4,8 STYLE styleval
	     WAIT "Press any key for rounded corners..."
	
	     *Round the corners.
	     CLEAR
	     radius = 12                 && 0 is no rounding, 15 is an oval
	     styleval = calcstyle(penpat, penwidth, fillpat, radius, xmode)
	     @ 2,2 TO 4,8 STYLE styleval
	     WAIT "Press any key for some color..."
	
	     *Add a COLOR clause for a red foreground and a blue background.
	     CLEAR
	     styleval = calcstyle(penpat, penwidth, fillpat, radius, xmode)
	     @ 2,2 TO 4,8 STYLE styleval COLOR "r/b"
	     WAIT "Press any key to end this program..."
	
	     *Clean up before closing
	     CLEAR ALL
	     CLOSE ALL
	     CLEAR
	     SET PROCEDURE TO
	
	     *Here is the procedure that calculates the STYLE clause
	     PROCEDURE calcstyle
	     PARAMETERS penpat, penwidth, fillpat, radius, xmode
	
	     newpwid = penwidth * 16     && multiply by 16 to the power of 1
	     newfpat = fillpat * 256     && multiply by 16 to the power of 2
	     newrad = radius * 4096      && multiply by 16 to the power of 3
	     newxmode = xmode * 65536    && multiply by 16 to the power of 4
	
	     *Sum all the values together
	     newstyle = penpat + newpwid + newfpat + newrad + newxmode
	
	     RETURN newstyle             && return the new result
	
	REFERENCES
	==========
	
	"Commands & Functions" pages 3-7 through 3-11
	
	Additional query words: 2.10 hard code
	
	======================================================================
	Keywords          :  
	Technology        : kbHWMAC kbOSMAC kbAudDeveloper kbFoxproSearch kbFoxBASE201Mac kbFoxBASESearch
	Version           : MACINTOSH:2.01
	
	=============================================================================
	

{% endraw %}
