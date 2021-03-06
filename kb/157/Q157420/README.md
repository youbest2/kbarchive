---
layout: page
title: "Q157420: XFOR: Embedded Messages not Handled by MS Mail Connector"
permalink: /kb/157/Q157420/
---

## Q157420: XFOR: Embedded Messages not Handled by MS Mail Connector

{% raw %}

	Article: Q157420
	Product(s): Microsoft Exchange
	Version(s): winnt:4.0,5.0,5.5
	Operating System(s): 
	Keyword(s): kbusage exc4 exc5 exc55
	Last Modified: 19-DEC-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Server, versions 4.0, 5.0, 5.5 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	If a message that has an embedded MAPI attachment is forwarded or sent directly
	to a Microsoft Mail recipient by means of the Microsoft Mail Connector, the
	attachment will not be visible to the MS Mail user. The user may see text that
	resembles the following:
	
	  [[ MAPI 1.0 embedded message : 4663 In winmail.dat ]]
	
	or possibly just the <Attachmentname.extension>:
	
	  <word.doc>
	
	  or
	
	  <sheet.xls>
	
	RESOLUTION
	==========
	
	It is possible to convert the embedded message to text format so it will be
	visible by a Microsoft Mail client. Note that this will not occur with any
	Microsoft Exchange client accessing an Microsoft Mail postoffice, and the
	following registry value will not be required.
	
	WARNING: Using Registry Editor incorrectly can cause serious problems that may
	require you to reinstall Windows 95. Microsoft cannot guarantee that problems
	resulting from the incorrect use of Registry Editor can be solved. Use Registry
	Editor at your own risk.
	
	1. On the Microsoft Exchange Server, start Regedt32.exe.
	
	2. Under the HKEY_LOCAL_MACHINE subtree, go to the following subkey:
	
	     \System\CurrentControlSet\Services\MSExchangeMSMI\Parameters
	
	3. On the Edit menu, click Add Value.
	
	4. As the Value Name, type:
	
	     Non-MAPI Embedded Messages
	
	5. Select REG_DWORD as the Data Type.
	
	6. Click OK.
	
	7. Type 1 (the numeral one) in the Data field, and make sure you click Hex in
	  the Radix field.
	
	8. Click OK.
	
	9. Stop and restart the Microsoft Mail Connector Interchange service.
	
	This registry modification will allow MAPI embedded messages to be transmitted to
	the Microsoft Mail system in text format.
	
	
	Additional query words: PMDF attach attachments disappear forward missing SFS
	
	======================================================================
	Keywords          : kbusage exc4 exc5 exc55 
	Technology        : kbExchangeSearch kbExchange500 kbExchange550 kbExchange400 kbZNotKeyword2
	Version           : winnt:4.0,5.0,5.5
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
