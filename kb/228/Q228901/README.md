---
layout: page
title: "Q228901: XCON: Account Validation Problems with Dynamic RAS Installation"
permalink: /kb/228/Q228901/
---

## Q228901: XCON: Account Validation Problems with Dynamic RAS Installation

{% raw %}

	Article: Q228901
	Product(s): Microsoft Exchange
	Version(s): winnt:4.0,5.0,5.5
	Operating System(s): 
	Keyword(s): exc4 exc5 exc55
	Last Modified: 30-DEC-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Server, versions 4.0, 5.0, 5.5 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	A Dynamic Remote Access Service (RAS) connection configured with override
	account information may not authenticate. Consequently, the servers cannot bind
	over remote procedure call (RPC), and may generate the following events:
	
	  Dialing Server
	  Event ID 9318
	  An RPC communications error occurred. Unable to bind over RPC. Locality Table
	  (LTAB) index: 5, NT/MTA error code: 1722. Comms error 1722, Bind error 0,
	  Remote Server Name SREX [MAIN BASE 1 500 %10] (14)
	
	The following events are written to the system log:
	
	  Event ID: 5719
	  Source: Netlogon
	  Type: error
	  No Windows NT Domain Controller is available for domain CRM. (This event is
	  expected and can be ignored when booting with the 'No Net' Hardware Profile.)
	  The following error occurred:
	  There are currently no logon servers available to service the logon request.
	
	  Event ID 9322:
	  An interface error has occurred mta bind back over rpc has failed locatility
	  table 108, mta error: 1722 1722 bind error 0, remote server name... protocol
	  string id-tcp:ipaddress of server.
	
	  9316
	  An RPC communications error occurred. No data was sent over the RPC
	  connection. Locality table (LTAB) index: 4. Windows NT error: 0. The MTA will
	  attempt to recover the RPC connection. [BASE IL KERNEL 26 512] (12)
	
	MORE INFORMATION
	================
	
	There is empirical evidence that supports that servers handling Dynamic RAS
	connectors be Windows NT backup or primary domain controllers. Member servers
	handling Dynamic RAS connectors add an extra step of querying the domain
	controllers for account validation. This extra step can add additional overhead,
	which prevents the connection from being established, so that mail flow cannot
	occur.
	
	Additional query words:
	
	======================================================================
	Keywords          : exc4 exc5 exc55 
	Technology        : kbExchangeSearch kbExchange500 kbExchange550 kbExchange400 kbZNotKeyword2
	Version           : winnt:4.0,5.0,5.5
	Issue type        : kbinfo
	
	=============================================================================
	

{% endraw %}
