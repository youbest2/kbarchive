---
layout: page
title: "Q164845: XADM: Access Violation in Srvrmax.exe During Setup"
permalink: /kb/164/Q164845/
---

## Q164845: XADM: Access Violation in Srvrmax.exe During Setup

{% raw %}

	Article: Q164845
	Product(s): Microsoft Exchange
	Version(s): 5.0
	Operating System(s): 
	Keyword(s): 
	Last Modified: 20-FEB-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Server, version 5.0 
	-------------------------------------------------------------------------------
	
	
	SYMPTOMS
	========
	
	During setup of Microsoft Exchange Server 5.0 (enterprise or standard), the
	process may terminate unexpectedly with an access violation (Dr. Watson). The
	Drwtsn32.log will look similar to the following:
	
	  Application exception occurred:
	     App: srvrmax.dbg (pid=161)
	     When: 3/7/1997 @ 13:21:20.829
	     Exception number: c0000005 (access violation)
	
	  function: <nosymbols>
	
	  *----> Stack Back Trace <----*
	
	  FramePtr ReturnAd Param#1  Param#2  Param#3  Param#4  Function Name
	  0012de3c 00000000 004c004e 00000059 00000000 0012de5c <nosymbols>
	  0012ffc0 77f1b26b 00000208 00000000 7ffdf000 c0000005
	srvrmax!<nosymbols>
	  0012fff0 00000000 00460af0 00000000 00000000 77fa5aa0
	  kernel32!BaseProcessStart (FPO: Non-FPO [1,8,3])
	  00000000 00000000 00000000 00000000 00000000 00000000
	srvrmax!<nosymbols>
	
	NOTE: The <no symbols> appears because the RTL build does not have symbols
	for Srvrmax.exe. This is how Drwtsn32.log will look even with Windows NT and
	Microsoft Exchange symbols installed. Srvrmax.exe is really Setup.exe on an
	enterprise installation; Srvrmin.exe is Setup.exe on a standard installation.
	
	CAUSE
	=====
	
	The allocated buffer to hold the length of the domain's PDC name is too small. A
	primary domain controller (PDC) computer name with a length of 14 characters or
	more will overrun the buffer and corrupt the stack, causing heap corruption and
	the access violation.
	
	
	
	
	RESOLUTION
	==========
	
	The buffer to hold the domain's PDC name was increased by two characters.
	
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Microsoft Exchange Server
	version 5.0. This problem was corrected in the latest Microsoft Exchange Server
	5.0 U.S. Service Pack. For information on obtaining the service pack, query on
	the following word in the Microsoft Knowledge Base (without the spaces):
	
	  S E R V P A C K
	
	
	MORE INFORMATION
	================
	
	Build 1457.10 was the original release-to-manufacturing version of Microsoft
	Exchange Server version 5.0. As soon as this issue was detected, the product was
	recalled and Microsoft issued Build 1457.11 as the current release to
	manufacturing revision of the product.
	
	Customers impacted by this issue include only those that have obtained Build
	1457.10 through "non-channel" means. This build was only briefly available as a
	download from the http://www.microsoft.com/exchange/ site and could have been
	obtained through Microsoft's own internal servers.
	
	
	Additional query words: crash
	
	======================================================================
	Keywords          :  
	Technology        : kbExchangeSearch kbExchange500 kbZNotKeyword2
	Version           : :5.0
	
	=============================================================================
	

{% endraw %}
