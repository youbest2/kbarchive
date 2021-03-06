---
layout: page
title: "Q166312: XADM: Replication or Knowledge Consistency Check Fails"
permalink: /kb/166/Q166312/
---

## Q166312: XADM: Replication or Knowledge Consistency Check Fails

{% raw %}

	Article: Q166312
	Product(s): Microsoft Exchange
	Version(s): 5.0
	Operating System(s): 
	Keyword(s): kbusage
	Last Modified: 24-APR-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Server, version 5.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When attempting to perform a knowledge consistency check (KCC), you receive the
	following warning:
	
	  An error was encountered by the knowledge consistency checker on server
	  'ServerName'. <<0xc1030b1e - The knowledge consistency check did not
	  correct directory inconsistencies. Be sure the directory service is
	  running, and then try again. If the error recurs, try stopping the
	  directory service and the Administrator program and then restarting
	  them. To view details of the error, see the application event log in
	  the Windows NT Event Viewer on the Microsoft Exchange Server computer
	  on which you checked knowledge consistency.
	
	You will also receive the following replication error in the application log:
	
	  Event ID: 1091
	  Source: MSExchangeDS
	  Type: Warning
	  Category: Replication
	
	  The directory replication agent (DRA) attempted to open mail with name
	  /o=Organization/ou=SITE/cn=Configuration/cn=Servers/cn=ServerName/cn=
	  Microsoft DSA:ServerName but received error 2147942487. Messages could
	  not be sent. Make sure that the mail service on this Microsoft Exchange
	  Server computer is running.
	
	MORE INFORMATION
	================
	
	Error 2147942487 is a Jet-level error indicating that an invalid MAPI parameter
	has been passed on by the messaging service (MAPI_E_INVALID_PARAMETER). This
	could happen if Mapi32.dll is not a supported version or the latest version
	supplied with Exchange or the latest service pack.
	
	RESOLUTION
	==========
	
	Stop all Exchange services and copy the Mapi32.dll file from the Exchange Server
	5.0 CD. Replace the Mapi32.dll file in the \<system>\system32 with the
	correct Mapi32.dll file. Remove the read-only attribute on the Mapi32.dll file
	and restart the Exchange services.
	
	======================================================================
	Keywords          : kbusage 
	Technology        : kbExchangeSearch kbExchange500 kbZNotKeyword2
	Version           : 5.0
	
	=============================================================================
	

{% endraw %}
