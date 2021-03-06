---
layout: page
title: "Q95665: How to Use the UPDATE Command"
permalink: /kb/095/Q95665/
---

## Q95665: How to Use the UPDATE Command

{% raw %}

	Article: Q95665
	Product(s): Microsoft FoxPro
	Version(s): 2.1,3.0,6.0
	Operating System(s): 
	Keyword(s): 
	Last Modified: 22-FEB-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual FoxPro for Windows, versions 3.0, 6.0 
	- Microsoft FoxBASE+ for MS-DOS, version 2.1 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	The UPDATE command updates the currently selected table with data from a table
	open in another work area. The current table must be indexed or sorted on the
	key field. Data is replaced for records with matching key fields. The FROM table
	must also be indexed or sorted unless the RANDOM option is specified.
	
	MORE INFORMATION
	================
	
	For each record in the currently selected table, there may be multiple matching
	records in the update table. If this is the case, the record in the currently
	selected table is updated by each of these matching records. After the update is
	completed, the record in the currently selected table will contain the data from
	the last matching record in the update table.
	
	Also, if the currently selected table contains records with duplicate key fields,
	only the first record is updated.
	
	Example
	-------
	
	     SELECT 1
	     USE invoices INDEX invoices
	     SELECT 2
	     USE detail
	     SELECT 1
	     UPDATE ON ino FROM detail ;
	     REPLACE itotal WITH detail.qty * detail.price RANDOM
	
	In the above example, the key field is INO. The INVOICES table is indexed on INO.
	The detail table is not indexed, so the RANDOM clause is used with the UPDATE
	command. If the RANDOM clause is not used, the INVOICES table will not be
	updated properly because the UPDATE command is expecting the DETAIL table to be
	in indexed order. The UPDATE command looks for a matching record in the DETAIL
	table; when it finds one, it replaces ITOTAL with the result of qty * price. In
	the DETAIL table, there are multiple matching records, so the INVOICES table
	will be updated only with data from the last matching record.
	
	NOTE: The key field can be only one field. Two fields cannot be concatenated
	together, as in INO+ITOTAL.
	
	WARNING: SET DELETED ON ignores deleted records in the source file (DETAIL
	table), but deleted records in the target file (INVOICES) are updated.
	
	Additional query words:
	
	======================================================================
	Keywords          :  
	Technology        : kbVFPsearch kbAudDeveloper kbFoxproSearch kbFoxBASE210DOS kbFoxBASESearch kbVFP300 kbVFP600
	Version           : :2.1,3.0,6.0
	
	=============================================================================
	

{% endraw %}
