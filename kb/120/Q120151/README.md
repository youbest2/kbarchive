---
layout: page
title: "Q120151: Browsing a Wide Area Network with WINS"
permalink: /kb/120/Q120151/
---

## Q120151: Browsing a Wide Area Network with WINS

{% raw %}

	Article: Q120151
	Product(s): Microsoft Windows NT
	Version(s): 3.1 3.11 3.5 4.0
	Operating System(s): 
	Keyword(s): kbnetwork
	Last Modified: 08-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows for Workgroups version 3.11 
	- Microsoft Windows NT Server version 3.1 
	- Microsoft Windows NT Workstation version 3.1 
	- Microsoft Windows NT Advanced Server, version 3.1 
	- Microsoft Windows NT Workstation versions 3.5, 3.51, 4.0 
	- Microsoft Windows NT Server versions 3.5, 3.51, 4.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	This article discusses how resource browsing works across a Wide Area Network
	(WAN) and how Microsoft's Windows Internet Name Service (WINS) improves
	cross-subnet browsing.
	
	MORE INFORMATION
	================
	
	Browsing with Windows NT version 3.1 (pre-WINS)
	-----------------------------------------------
	
	In Windows NT version 3.1, browser information transmission relies almost
	entirely on network broadcasts. In a WAN environment (using a network protocol
	such as TCP\IP) domains are typically separated by routers. To reduce bandwidth
	usage, broadcast packets are often filtered and do not pass through routers thus
	limiting them to the local subnet.
	
	As a result, the Windows NT version 3.1 default B-Node name resolution cannot
	resolve names on remote subnets. Each local subnet functions as an independent
	browsing entity, with its own Master Browser and Backup Browsers. Browse
	elections occur on a per subnet basis.
	
	Windows NT Advanced Server version 3.1 supports cross-subnet browsing. To browse
	across a WAN, at least one Windows NT Advanced Server is required in each
	subnet. The Domain Master Browser is responsible for maintaining a WAN wide
	browse list of available servers in the domain and all accessible domains.
	
	When a domain spans multiple subnets, the Master Browsers for each subnet
	announce themselves to the Domain Master Browser using the directed datagram,
	"MasterBrowserAnnouncement". The Domain Master Browser then remotes a
	"NetServerEnum" call to the Master Browser that announced itself in order to
	collect that subnet's list of servers. The Domain Master Browser merges the
	server list from the Master Browser with its own server list. This process is
	done every 15 minutes to guarantee that the Domain Master Browser has a complete
	list of servers in the domain.
	
	Now, when a client remotes a "NetServerEnum" call to the Master Browser, the
	Master Browser will be able to return all of the servers in the domain,
	regardless of what subnet they are on.
	
	NOTE: A Windows NT workgroup cannot span multiple subnets. If a Windows NT
	workgroup is implemented across two or more subnets, it will function as
	separate workgroups.
	
	
	To ensure each subnet's Master Browser can access every domain's Primary Domain
	Controller (PDC), the Master Browser must maintain a LMHOSTS file containing the
	name of each domain's PDC and Backup Domain Controllers (BDC) with a #DOM
	extension. To guarantee that each PDC can access the local browse list from each
	subnet's Master Browser, TCP/IP (and other WAN protocols) must cache the client
	address for a reasonable period of time.
	
	Browsing with Windows NT Server version 3.5 or later with WINS
	--------------------------------------------------------------
	
	Windows NT Server versions 3.5 or later include the Windows Internet Name Service
	(WINS). WINS is basically a directory service for NetBIOS names and IP
	addresses.
	
	The Domain Master Browser registers a unique Browser name of "<DOMAIN>[1B]"
	with the WINS server. Other Domain Master Browsers will periodically query the
	WINS server for a list of domains. They then merge this list into their local
	domain browse list. They then propagate this list to the Master Browser on each
	subnet via the mechanism mentioned above.
	
	The Domain Master Browser queries the WINS server in a two part process:
	
	1. The Browser does a wild card lookup of all domain names ending in [1b].
	
	2. Then the Browser does a reverse query for each individual <DOMAIN>[1B]
	  name to learn the unique name of the Domain Master Browser for that domain.
	
	In addition to querying the WINS server, the Domain Master Browsers continue to
	collect server lists and domain names in the above mentioned ways.
	
	NOTE: Only WINS-aware Domain Master Browsers (those in Windows NT versions 3.5 or
	later) will register their <DOMAIN>[1B] name with the WINS server. Windows
	NT version 3.1 Domain Master Browsers will not use WINS.
	
	Windows NT Workstation versions 3.5 or later are WINS-Aware
	-----------------------------------------------------------
	
	Windows NT Workstation versions 3.5 or later remote the "NetServerEnum" call to a
	Backup Browser Master for its domain. The list of domains returned includes
	those the Domain Master Browser discovered via the WINS server. When the
	Workstation browses a remote domain it will query the WINS server for the IP
	address of the computer that registered the <DOMAIN>[1b] name. The
	Workstation then sends a "GetBackupListReq" to the IP address and picks one of
	the machine names from the response and remotes a "NetServerEnum" call to that
	name to get a list of computers in that domain.
	
	Windows NT version 3.1 Clients are Not WINS-Aware
	-------------------------------------------------
	
	When the Windows NT 3.1 client browses a remote domain, it sends a
	"GetBackupListReq" to the name <DOMAIN>[1d], not <DOMAIN>[1b].
	Because there is no Domain Master Browser for this domain in its subnet. The
	client will eventually give up and will perform a "double hop" to its local
	Domain Browser Master. The browser server will remote the NetServerEnum API for
	the client. How the remote is resolved depends on if the browser server is WINS
	aware or not.
	
	Windows for Workgroups version 3.11 Clients with TCP/IP-32 are WINS-Aware
	-------------------------------------------------------------------------
	
	Windows for Workgroups version 3.11 clients can be WINS aware through TCP/IP-32
	for Windows for Workgroups. WINS will help with standard workstation
	connections. However, the browser code that they use is not WINS or WAN aware.
	If the Windows for Workgroups client is in local browser domain that has a
	Windows NT 3.5 or later browser server, the client will see a list of all remote
	domains. However, if the client selects one of these names it will not be able
	to resolve it. The client is unaware of the special [1b] name.
	
	
	Additional query words: prodtcp32 prodnt 3.10 enterprise arp wfw wfwg
	
	======================================================================
	Keywords          : kbnetwork 
	Technology        : kbWinNTsearch kbWinNTWsearch kbWinNTW400 kbWinNTW400search kbWinNT351search kbWinNT350search kbWinNT400search kbWinNTW350 kbWinNTW350search kbWinNTW351search kbWinNTW351 kbWinNTW310 kbWinNTSsearch kbWinNTS400search kbWinNTS400 kbWinNTS351 kbWinNTS350 kbWinNTS310 kbWinNTAdvSerSearch kbWinNTAdvServ310 kbWinNTS351search kbWinNTS350search kbWinNTS310search kbAudDeveloper kbWinNT310Search kbWinNTW310Search kbWFWSearch kbWFW311
	Version           : 3.1 3.11 3.5 4.0
	
	=============================================================================
	

{% endraw %}
