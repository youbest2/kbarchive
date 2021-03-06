---
layout: page
title: "Q139873: PRB: Import Wizard's Scan Option Doesn't Scan Beyond Record 50"
permalink: /kb/139/Q139873/
---

## Q139873: PRB: Import Wizard's Scan Option Doesn't Scan Beyond Record 50

{% raw %}

	Article: Q139873
	Product(s): Microsoft FoxPro
	Version(s): WINDOWS:3.0
	Operating System(s): 
	Keyword(s): 
	Last Modified: 10-FEB-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual FoxPro for Windows, version 3.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	After you select the Scan All Records option in the Import Wizard, only the
	first 50 records are actually scanned.
	
	STATUS
	======
	
	Microsoft is researching this behavior and will post new information here in the
	Microsoft Knowledge Base as it becomes available.
	
	MORE INFORMATION
	================
	
	By selecting the Scan All Records option in the Import Wizard, you might assume
	that the data is scanned and the structure of the file being imported is
	verified before the import actually occurs. This is not the case.
	
	Steps to Reproduce Behavior
	---------------------------
	
	CAUTION: For the purposes of this demonstration, you should close all critical
	data and applications other than Visual FoxPro to ensure that the results of
	this demonstration have no effect on other data or applications should an error
	occur.
	
	This demonstration requires that the Customer table from the Testdata database be
	present, intact, and available for your use. To demonstrate that the above
	situation is actually what the Import Wizard is doing, follow these steps:
	
	1. Use the Customer table from the Testdata database.
	
	2. In the Command window, enter the following line of code:
	
	     COPY TO C:\TESTTEXT.TXT TYPE DELIMITED
	
	3. Open Testtext.txt in Notepad. If your text is wrapping, turn Word wrap off.
	
	4. Scroll down to the 51st record, the first field of which should be Merep, and
	  remove the first comma (not the quotation mark) on that line. This damages
	  the structure of the text file to be imported.
	
	5. Save and close the file.
	
	6. On Visual FoxPro's Tools menu, click Wizards, and then click Import.
	
	7. Click the three-dot button located next to the Source File text box.
	
	8. Locate Testtext.txt on your hard disk, select it, and then click OK.
	
	9. Click the Next button in the Import Wizard dialog box. Note that the Status
	  bar now reads:
	
	  Record: 1/50
	
	  This indicates that the first 50 records are intact.
	
	10. Click the Option button.
	
	11. In the Import Wizard Options dialog box, click Scan All Records, and then
	  click OK.
	
	12. Click Next, click Next, and then click Finish in the Wizard's dialog boxes.
	  You may receive an error that indicates that the application has performed
	  an illegal instruction and will be shut down. The point of this exercise was
	  to demonstrate the fact that the Import Wizard never scanned the text file
	  being imported. The 51st record was damaged, and the Import Wizard only
	  displays the first 50 records.
	
	13. Browse the newly created table, and go to record 51. The data will not have
	  been imported properly. Close the table.
	
	14. In the Command window, enter the following line of code to erase the table
	  you created:
	
	      ERASE TESTTEXT.DBF
	
	To further demonstrate the fact that the Import Wizard doesn't scan the text file
	being imported, perform the following steps:
	
	1. Using Notepad, edit Testtext.txt, and repair record 51 by inserting the comma
	  that was removed earlier.
	
	2. Move up to record 49 and remove the first comma. The first field in this
	  record should be MAGAA.
	
	3. Save and close the file.
	
	4. On the Visual FoxPro Tools menu, click Wizards, and then click Import. Then
	  click the three-dot button next to the Source File text box.
	
	5. Locate Testtext.txt on your hard disk, select it, and then click OK.
	
	6. Click Next. You will receive an error stating the records in this file do not
	  appear to be delimited by commas or tabs and the record lengths are variable.
	  Fixed-length format will be used by default. This time, you did not tell the
	  Wizard to scan all records. The damaged record was within the first 50
	  records and was automatically detected by the Wizard, so it displays the
	  error message.
	
	Additional query words: VFoxWin import fail
	
	======================================================================
	Keywords          :  
	Technology        : kbVFPsearch kbAudDeveloper kbVFP300
	Version           : WINDOWS:3.0
	
	=============================================================================
	

{% endraw %}
