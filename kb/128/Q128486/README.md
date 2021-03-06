---
layout: page
title: "Q128486: BUG: Btrieve: Drop Table Does Not Remove Entry in SQLTables"
permalink: /kb/128/Q128486/
---

## Q128486: BUG: Btrieve: Drop Table Does Not Remove Entry in SQLTables

{% raw %}

	Article: Q128486
	Product(s): Open Database Connectivity (ODBC)
	Version(s): WINDOWS:2.0
	Operating System(s): 
	Keyword(s): kbBug kbISS
	Last Modified: 27-JUL-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Open Database Connectivity, version 2.0 
	-------------------------------------------------------------------------------
	
	BUG# QJET: 1267 (2.00.2114)
	
	SYMPTOMS
	========
	
	Use of the SQL syntax Drop Table with the ODBC Btrieve Driver from the ODBC
	Desktop Database Drivers version 2.0 will correctly delete the table from the
	.DDF file; however, the reference to this table will still be contained when
	SQLTables is called on this Btrieve database. Thus, a new table of the same name
	cannot be created even though the table is no longer physically present in the
	database.
	
	For example, use ODBC Test to try to create a Btrieve table, then drop it, and
	try to recreate it again. This should work.
	
	  create table test1  (col1 string(30))
	Returns: SQL_SUCCESS=0
	
	  drop table test1
	Returns: SQL_SUCCESS=0
	
	  create table test1  (col1 string(30))
	Return:   SQL_ERROR=-1
	stmt:szSqlState = "S0001", *pfNativeError = -1303, *pcbErrorMsg = 62
	szErrorMsg="[Microsoft][ODBC Btrieve Driver] Table 'test1' already
	exists."
	
	WORKAROUND
	==========
	
	The ODBC Btrieve driver version 2.00.2317 will resolve this problem. It must be
	used in conjunction with WBTRCALL.DLL that is dated 3/31/92 and is 51,392 bytes
	in size. This file must be obtained from Btrieve Technologies or Novell. Please
	contact these vendors for more information on this file.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in the Microsoft ODBC Btrieve
	version 2.00.2114. This problem has been fixed in the Microsoft ODBC Btrieve
	version 2.00.2317. For more information, please contact your primary support
	provider.
	
	Additional query words: 2.00.2317 ODBC Btrieve Desktop Database Drivers 2.0 MFC Word Query Excel Visual C++
	
	======================================================================
	Keywords          : kbBug kbISS 
	Technology        : kbAudDeveloper kbODBCSearch kbODBC200
	Version           : WINDOWS:2.0
	Issue type        : kbbug
	
	=============================================================================
	

{% endraw %}
