---
layout: page
title: "Q156773: PRB: COPY TO TYPE DELIMITED Differs in Various FP Versions"
permalink: /kb/156/Q156773/
---

## Q156773: PRB: COPY TO TYPE DELIMITED Differs in Various FP Versions

{% raw %}

	Article: Q156773
	Product(s): Microsoft FoxPro
	Version(s): WINDOWS:5.0,6.0
	Operating System(s): 
	Keyword(s): kbvfp500 kbvfp600
	Last Modified: 14-DEC-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual FoxPro for Windows, versions 5.0, 6.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	In Visual FoxPro 5.0, the COPY TO <filename> DELIMITED WITH BLANK command
	places quotation marks around character fields and preserves leading blank
	spaces within character fields. Other versions of FoxPro create text files that
	are slightly different in their format. You should be aware of the possible
	differences if you use this command under a previous version of FoxPro to port
	to Visual FoxPro 5.0.
	
	WORKAROUND
	==========
	
	If the character fields do not need quotation marks around them, use the COPY TO
	<filename> TYPE SDF command.
	
	STATUS
	======
	
	This behavior is by design.
	
	MORE INFORMATION
	================
	
	Different versions of FoxPro produce slightly different text files using the
	same command. Depending on the version, leading spaces may be truncated or
	quotation marks may be added to character fields. For example, COPY TO
	<filename> DELIMITED WITH BLANK in FoxPro 2.6a for Windows produces a text
	file that does not contain quotation marks around the character fields. If a
	character field contains leading spaces, they remain. However, Visual FoxPro
	3.0b exhibits different behavior. The text file contains no quotation marks
	around the character fields and leading spaces are trimmed from the fields.
	
	Visual FoxPro 5.0 produces a text file that preserves leading spaces and places
	quotation marks around each character field. This is the intended behavior of
	the product.
	
	The following text comes from the "COPY TO" Help file topic:
	
	  DELIMITED Creates a delimited file. A delimited file is an ASCII text file in
	  which each record ends with a carriage return and linefeed. The default field
	  separator is a comma. Since character data may include commas, character
	  fields are additionally delimited with double quotation marks.
	
	Steps to Reproduce Behavior
	---------------------------
	
	1. Create a table in the Command window by typing:
	
	     CREATE TABLE test (ctest C (30))
	
	2. In the Command window, type the following commands:
	
	     INSERT INTO test (ctest) VALUE ('This is a test')
	     INSERT INTO test (ctest) VALUE ('    This is another test')
	     INSERT INTO test (ctest) VALUE ('   This is a third test')
	
	3. Create a text file by typing the following command in the Command window:
	
	     COPY TO test.txt DELIMITED WITH BLANK
	
	4. Open the text file by typing the following in the Command window:
	
	     MODIFY COMMAND test.txt
	
	Note that the leading spaces are preserved and each field is surrounded by
	quotation marks.
	
	Additional query words: VFoxWin kbdsd
	
	======================================================================
	Keywords          : kbvfp500 kbvfp600 
	Technology        : kbVFPsearch kbAudDeveloper kbVFP500 kbVFP600
	Version           : WINDOWS:5.0,6.0
	
	=============================================================================
	

{% endraw %}
