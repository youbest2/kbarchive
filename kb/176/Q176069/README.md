---
layout: page
title: "Q176069: HOWTO: Print a Range of Pages in Word Using OLE Automation"
permalink: /kb/176/Q176069/
---

## Q176069: HOWTO: Print a Range of Pages in Word Using OLE Automation

{% raw %}

	Article: Q176069
	Product(s): Microsoft FoxPro
	Version(s): 
	Operating System(s): 
	Keyword(s): kbinterop kbAutomation kbvfp300 kbvfp500 kbvfp600 kbVS97 kbVS97sp2 kbWord MSGRAPH
	Last Modified: 07-DEC-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual FoxPro for Windows, versions 3.0b, 5.0a, 6.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	Printing either a range or selection of pages in a Word for Windows document
	from Visual FoxPro for Windows using OLE automation requires additional
	parameters for the PrintOut method of Word for Windows 97 or the FilePrint
	command in Word for Windows 95.
	
	All the parameters passed to Word in an OLE automation statement are positional.
	For example, the Range parameter is the third argument out of 15 in the
	parameter list for the Printout method. Therefore, arguments 1 and 2 must have
	the appropriate value for the argument and cannot be left out. However, any
	arguments past the last argument with a value do not need to be included in the
	command. For example, if no other parameters require a value after the Range is
	set, then Range could be the last argument passed to the PrintOut method.
	
	MORE INFORMATION
	================
	
	The code samples in this article are written to run exclusively with a
	particular version of Word. The examples for Word for Windows 95 were written to
	work with both Visual FoxPro for Windows versions 3.0b, 5.0a, and 6.0. The Word
	97 example works only with Visual FoxPro for Windows versions 5.0a with Service
	Pack 2 installed and 6.0. If the code is used with any other version of Word or
	Visual FoxPro for Windows, the following OLE error may occur:
	
	  OLE error code 0x80020005: Type Mismatch.
	
	The Range parameter accepts five valid values. Therefore, unless the Range
	parameter is properly set, Word will not print. The valid Range values are
	listed below with a description of the their action:
	
	  0 Prints the entire document
	  1 Prints the selection
	  2 Prints the current page
	  3 Prints the range of pages specified by the From and To parameters
	  4 Prints the range of pages specified by Pages parameter
	
	For more information on the FilePrint command in Word 95 and PrintOut command in
	Word 97, see the Word for Windows documentation. The format of the Word 97
	PrintOut method and the Word 95 FilePrint command are listed below:
	
	  PrintOut(Background, Append, Range, OutputFileName, From, To,
	  Item, Copies, Pages, PageType, PrintToFile, Collate, FileName,
	  ActivePrinterMacGX, ManualDuplexPrint)
	
	  FilePrint(.Background, .AppendPrFile, .Range, .PrToFileName, .From,
	  .To, .Type, .NumCopies, .Pages, .Order, .PrintToFile, .Collate,
	  .FileName, .OutputPrinter)
	
	In the code examples below a Word document named Testdoc.doc is used that
	contains at least 10 pages.
	
	Printing Contiguous Range of pages
	----------------------------------
	
	There are two ways to print a contiguous range of pages using the Range
	parameter. Both methods depend on the value of Range. For instance, if the Range
	is set to 3, then set the From and To parameters. If the Range is 4, use the
	Pages parameter. Both methods are discussed below. In each code example, the
	FilePrint and PrintOut commands are shown using both variables and the explicit
	values for the arguments. This provides a better representation of the positions
	these arguments will take in the statement. The command using variables is
	commented out.
	
	Method 1: Range Argument Set to 3
	---------------------------------
	
	With the Range set to 3, the From and To parameters need to set for both the
	PrintOut method in Word 97 and FilePrint command in Word 95.
	
	For example, to print pages 4 through 8 of Testdoc.doc use the following Code.
	
	NOTE: This works with Word 95 and Visual FoxPro for Windows versions 3.0, 5.0,
	and 6.0.
	
	       range = "3"
	       from = "4"
	       to = "8"
	       oword = CreateObject("Word.Basic")
	       WITH oword
	        .FileOpen("C:\winword\testdoc.doc")   && Enter appropriate path.
	
	        * FilePrint statement using variables.
	        *.FilePrint(0,"0","",0,range,"",from,to)
	
	        * FilePrint using explicit values
	        .FilePrint(0,"0","",0,"3","","4","8")
	        .FileClose(2)
	       ENDWITH
	       oword=""
	
	NOTE: This works with Word 97 and Visual FoxPro for Windows version 5.0a with
	Service Pack 2 and 6.0:
	
	       range = "3"
	       from = "4"
	       to = "8"
	       oword = CreateObject("Word.Application")
	       WITH oword
	        .Documents.Open("C:\winword\testdoc.doc")  && Enter appropriate path.
	
	        * PrintOut statement using variables
	        *.ActiveDocument.PrintOut(0,0,range,"",from,to)
	
	        * PrintOut using explicit values
	        .ActiveDocument.PrintOut(0,0,"3","","4","8")
	        .Quit
	       ENDWITH
	
	Method 2: Range Argument Set to 4
	---------------------------------
	
	Assign 4 to the Range argument, then assign the pages to be printed to the Pages
	argument. To print pages 4 through 8, the Pages argument would be "4- 8."
	
	NOTE: This works with Word 95 and Visual FoxPro for Windows versions 3.0, 5.0,
	and 6.0:
	
	       range = "4"
	       pages = "4-8"
	       oword = CreateObject("Word.Basic")
	       WITH oword
	        .FileOpen("C:\winword\testdoc.doc")   && Enter appropriate path.
	
	        * FilePrint statement using variables.
	        *.FilePrint(0,"0","",0,range,"","","",0,1,pages)
	
	        * FilePrint using explicit values
	        .FilePrint(0,"0","",0,"4","","","",0,1,"4-8")
	        .FileClose(2)
	       ENDWITH
	       oword=""
	
	NOTE: This works with Word 97 and Visual FoxPro for Windows version 5.0a with
	Service Pack 2 and 6.0:
	
	       range = "4"
	       pages = "4-8"
	       oword = CreateObject("Word.Application")
	       WITH oword
	        .Documents.Open("C:\winword\testdoc.doc")  && Enter appropriate path.
	
	        * PrintOut statement using variables
	        *.ActiveDocument.PrintOut(0,0,range,"","","",0,1,pages)
	
	        * PrintOut using explicit values
	        .ActiveDocument.PrintOut(0,0,"4","","6","8",0,1,"4-8")
	        .Quit
	       ENDWITH
	
	Printing Non-Contiguous Range of Pages
	--------------------------------------
	
	To print non-contiguous pages, set the Range parameter to 4 and the Pages
	parameter to the pages to print. For example, to print page 2 and then pages 6
	through 9, the Pages argument would be "2,6-9." The Pages parameter is set the
	same for both Word 95 and Word 97.
	
	NOTE: This works in Word 95 and Visual FoxPro for Windows versions 3.0, 5.0, and
	6.0:
	
	       range = "4"
	       pages = "2,6-9"
	       oword = CreateObject("Word.Basic")
	       WITH oword
	        .FileOpen("C:\winword\testdoc.doc")   && Enter appropriate path.
	
	        * FilePrint statement using variables.
	        *.FilePrint(0,"0","",0,range,"","","",0,1,pages)
	
	        * FilePrint using explicit values
	        .FilePrint(0,"0","",0,"4","","","",0,1,"2,6-9")
	        .FileClose(2)
	       ENDWITH
	       oword=""
	
	NOTE: This works with Word 97 and Visual FoxPro for Windows version 5.0a with
	Service Pack 2 and 6.0:
	
	       range = "4"
	       pages = "2,6-9"
	       oword = CreateObject("Word.Application")
	       WITH oword
	        .Documents.Open("C:\winword\testdoc.doc")  && Enter appropriate path.
	
	        * PrintOut statement using variables
	        *.ActiveDocument.PrintOut(0,0,range,"","","",0,1,pages)
	
	        * PrintOut using explicit values
	        .ActiveDocument.PrintOut(0,0,"4","","","",0,1,"2,6-9")
	        .Quit
	        ENDWITH
	
	(c) Microsoft Corporation 1997, All Rights Reserved. Contributions by Dean
	Christopher, Microsoft Corporation
	
	
	REFERENCES
	==========
	
	Microsoft Word Visual Basic Help
	
	Additional query words:
	
	======================================================================
	Keywords          : kbinterop kbAutomation kbvfp300 kbvfp500 kbvfp600 kbVS97 kbVS97sp2 kbWord MSGRAPH 
	Technology        : kbVFPsearch kbAudDeveloper kbVFP300b kbVFP600 kbVFP500a
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
