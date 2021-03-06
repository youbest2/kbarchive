---
layout: page
title: "Q247291: XFOR: Migration Slow to Enumerate Names from a Large NAB"
permalink: /kb/247/Q247291/
---

## Q247291: XFOR: Migration Slow to Enumerate Names from a Large NAB

{% raw %}

	Article: Q247291
	Product(s): Microsoft Exchange
	Version(s): 5.5
	Operating System(s): 
	Keyword(s): exc55 kbExchange550preSP4fix kbExchange550sp4Fix
	Last Modified: 11-NOV-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Server, version 5.5 
	-------------------------------------------------------------------------------
	
	
	SYMPTOMS
	========
	
	If you migrate from a Lotus Notes server that has a large Notes Address Book
	(NAB), it may be 15 to 20 minutes before any data is migrated.
	
	This is especially time consuming if you only need to migrate a small group of
	users from that server.
	
	CAUSE
	=====
	
	The migration program enumerates the entire NAB. The program builds a list of
	all of the users on that server and then migrates the names that are provided by
	either the Control file or the user selection.
	
	RESOLUTION
	==========
	
	To resolve this problem, obtain the latest service pack for Exchange Server 5.5.
	For additional information, please see the following article in the Microsoft
	Knowledge Base:
	
	  Q191014 XGEN: How to Obtain the latest Exchange Server 5.5 Service Pack
	
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Microsoft Exchange Server
	version 5.5. This problem was first corrected in Exchange Server 5.5 Service
	Pack 4.
	
	MORE INFORMATION
	================
	
	This hotfix provides for the use of a Userlist in a control file that does not
	enumerate the Notes Address Book (NAB). This Userlist is triggered using the
	'Accounts' keyword in a Control file. If the user names are provided to the
	migration program, the entire NAB is not generated into a migration list. This
	faster method is only available from the Command Line migration.
	
	  Q263755 XFOR: Lotus Notes Command-Line Migration Instructions
	  Incomplete[exchange]
	
	NOTE: Q198957 also addresses the control file but it is missing information that
	is better addressed by the above Q263755.
	
	Additional query words:
	
	======================================================================
	Keywords          : exc55 kbExchange550preSP4fix kbExchange550sp4Fix 
	Technology        : kbExchangeSearch kbExchange550 kbZNotKeyword2
	Version           : :5.5
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
