---
layout: page
title: "Q139365: Capabilities of the &quot;Add Workstations To Domain&quot; Right"
permalink: /kb/139/Q139365/
---

## Q139365: Capabilities of the &quot;Add Workstations To Domain&quot; Right

{% raw %}

	Article: Q139365
	Product(s): Microsoft Windows NT
	Version(s): 3.5 3.51 4.0
	Operating System(s): 
	Keyword(s): kbnetwork kbusage
	Last Modified: 08-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Workstation versions 3.5, 3.51, 4.0 
	- Microsoft Windows NT Server versions 3.5, 3.51, 4.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	If you are not a member of the domain Administrators or Account Operators group,
	the Add Workstations To Domain right allows you to perform all the actions
	explained below.
	
	This right does not exist in Windows NT 3.1.
	
	MORE INFORMATION
	================
	
	The Add Workstations To Domain right allows you to do all of the following:
	
	- Remotely add workstation and server (non-domain controller) computer accounts
	  to a domain. To add computer accouts use the Add To Domain command in Server
	  Manager.
	
	- Remotely remove computer accounts that you created. To do remove computer
	  accounts select the computer account in Server Manager and use the Remove
	  From Domain command.
	
	  NOTE: Regarding the first two listings above, if you only have the Add
	  Workstations To Domain right, but not the Administrator or Account Operator
	  right, you can use your right only remotely. You must be connected to the
	  server as a client user having the rights, and you must use Server Manager
	  for Domains from the Windows NT Resource kit on the client computer to make
	  the change.
	
	- 
	
	  Join the domain from a Windows NT client. To join the domain
	                         run Control
	   Panel and choose Network and specify your username and
	                          password.
	
	  NOTE: The following Network Settings popup may appear:
	
	     Unable to add or change accounts on the domain. The
	     account information entered does not grant sufficient
	     privilege to create
	     or change accounts.
	
	  You can join a domain under a computer account only if the
	  computer account does not exist or if you add the computer
	  account. If an Administrator or Account Operator adds the
	  computer account, the computer account must be removed by an
	  Administrator or Account Operator before you can join the
	  domain under that computer account.
	
	Additional query words: prodnt machine security
	
	======================================================================
	Keywords          : kbnetwork kbusage 
	Technology        : kbWinNTsearch kbWinNTWsearch kbWinNTW400 kbWinNTW400search kbWinNT351search kbWinNT350search kbWinNT400search kbWinNTW350 kbWinNTW350search kbWinNTW351search kbWinNTW351 kbWinNTSsearch kbWinNTS400search kbWinNTS400 kbWinNTS351 kbWinNTS350 kbWinNTS351search kbWinNTS350search
	Version           : 3.5 3.51 4.0
	
	=============================================================================
	

{% endraw %}
