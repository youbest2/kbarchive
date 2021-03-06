---
layout: page
title: "Q161368: Service Pack 2 May Cause Loss of Connectivity in Remote Access"
permalink: /kb/161/Q161368/
---

## Q161368: Service Pack 2 May Cause Loss of Connectivity in Remote Access

{% raw %}

	Article: Q161368
	Product(s): Microsoft Windows NT
	Version(s): 
	Operating System(s): 
	Keyword(s): kbenvkbbuglist kbfixlist
	Last Modified: 09-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Server version 4.0 SP2 
	- Microsoft Windows NT Workstation version 4.0 SP2 
	-------------------------------------------------------------------------------
	
	
	SYMPTOMS
	========
	
	After you install Service Pack 2 for Windows NT 4.0, you may not be able to ping
	or otherwise make use of the connection you have established with an ISP when
	using RAS to dial out.
	
	Additionally, the route table may not have a route for the remote connection.
	
	CAUSE
	=====
	
	The Multilinking Protocol (MP) option is always negotiated during the Link
	Control Protocol (LCP)-phase of negotiation in Service Pack 2 for Windows NT
	4.0. This occurs if the Enable PPP LCP Extensions check box on the Server tab of
	the Edit Phonebook Entry dialog box is enabled or disabled.
	
	Although MP is an extension of LCP, it is not part of RFC 1570 -- LCP Extensions.
	In Service Pack 2 for Windows NT 4.0, it is no longer necessary to enable this
	check box to attempt MP negotiation.
	
	NOTE: Some Internet service providers (ISP) cannot deal with the MP options
	correctly. This problem is resolved by changing the conditions in which RAS
	sends multilink information to the remote server.
	
	RESOLUTION
	==========
	
	The binaries below resolve this issue by making an attempt at MP negotiation
	only if there is more than one link in the phonebook entry.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Microsoft Windows NT version
	4.0. This problem was corrected in the latest Microsoft Windows NT 4.0 U.S.
	Service Pack. For information on obtaining the service pack, query on the
	following word in the Microsoft Knowledge Base (without the spaces):
	
	  S E R V P A C K
	
	NOTE: This fix is to be applied only to computers with Service Pack 2 for Windows
	NT 4.0 installed.
	
	This hotfix has been posted to the following Internet location:
	
	  ftp://ftp.microsoft.com/bussys/winnt/winnt-public/fixes/usa/NT40/hotfixes-postsp2/ras-fix
	
	
	MORE INFORMATION
	================
	
	
	For additional information, please see the following article in the Microsoft
	Knowledge Base:
	
	  ARTICLE-ID: Q166090
	  TITLE : MSN Support in Windows NT
	
	
	Additional query words: sp2 prodnt dun dial-up networking Bad IP Address RAS
	
	======================================================================
	Keywords          : kbenv kbbuglist kbfixlist
	Technology        : kbWinNTsearch kbWinNTWsearch kbWinNTW400search kbWinNT400search kbWinNTW400sp2 kbWinNTSsearch kbWinNTS400sp2 kbWinNTS400search
	Issue type        : kbbug
	
	=============================================================================
	

{% endraw %}
