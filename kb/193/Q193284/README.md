---
layout: page
title: "Q193284: XADM: Searching Folders on Server Never Finishes"
permalink: /kb/193/Q193284/
---

## Q193284: XADM: Searching Folders on Server Never Finishes

{% raw %}

	Article: Q193284
	Product(s): Microsoft Exchange
	Version(s): WINDOWS:5.5,8.5
	Operating System(s): 
	Keyword(s): 
	Last Modified: 20-MAY-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Server, version 5.5 
	- Microsoft Outlook 98, version 8.5, used with:
	   - the operating system: Microsoft Windows NT 
	- Microsoft Outlook 98, version 8.5, used with:
	   - the operating system: Microsoft Windows 98 
	   - the operating system: Microsoft Windows 95 
	-------------------------------------------------------------------------------
	
	
	SYMPTOMS
	========
	
	If you use the Advanced Find tool in the versions of Microsoft Outlook listed at
	the beginning of this article to search one or more folders located on a
	Microsoft Exchange Server computer, the search may never finish. This problem
	does not occur when you use the Advanced Find tool to search folders located in
	a set of personal folders (.pst file) or in an offline storage file (OST).
	
	Note that this problem only occurs when you are using version 5.5.2363.0 or later
	of the Emsmdb32.dll file, but earlier than version 5.5.2397.0.
	
	CAUSE
	=====
	
	This problem occurs when the Emsmdb32.dll file does not notify the server that
	the search has finished.
	
	RESOLUTION
	==========
	
	A supported fix that corrects this problem is now available from Microsoft, but
	has not been fully regression-tested and should be applied only to systems
	experiencing this specific problem. If you are not severely affected by this
	specific problem, Microsoft recommends that you wait for the next Microsoft
	Exchange Server version 5.5 service pack that contains this fix.
	
	To resolve this problem immediately, contact Microsoft Product Support Services
	to obtain the fix. For a complete list of Microsoft Product Support Services
	phone numbers and information on support costs, please go to the following
	address on the World Wide Web:
	
	  http://support.microsoft.com/default.aspx?scid=fh;EN-US;CNTACTMS
	
	The English version of this fix should have the following file attributes or
	later:
	
	  Component: Information Store
	
	  File Name      Version
	  -------------------------
	  Emsmdb32.dll   5.5.2397.0
	
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Microsoft Exchange Server
	version 5.5.
	
	======================================================================
	Keywords          :  
	Technology        : kbOutlookSearch kbExchangeSearch kbZNotKeyword2 kbOutlook98Search kbZNotKeyword3
	Version           : WINDOWS:5.5,8.5
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
