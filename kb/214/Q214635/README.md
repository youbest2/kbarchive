---
layout: page
title: "Q214635: XADM: ESEUTIL /P Crashes on a Corrupt Database"
permalink: /kb/214/Q214635/
---

## Q214635: XADM: ESEUTIL /P Crashes on a Corrupt Database

{% raw %}

	Article: Q214635
	Product(s): Microsoft Exchange
	Version(s): winnt:5.5
	Operating System(s): 
	Keyword(s): exc55 EXC55SP3Fix
	Last Modified: 30-SEP-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Server, version 5.5 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	ESEUTIL may crash when trying to repair a corrupt database. The following
	information may be found in the Drwtsn32.log file regarding the crash:
	
	  FramePtr ReturnAd Param#1 Param#2 Param#3 Param#4 Function Name
	  0012f54c 6ff02fee 00a10200 fffff9bd 00000000 02830280
	  ese!FILEIReportIndexCorrupt [omap]
	
	CAUSE
	=====
	
	The error reporting code in ESEUTIL tries to use a pointer that was freed
	resulting in an access violation. The fix for this problem allows Eseutil.exe to
	report back the error that it found when trying to repair the database. This is
	a rare case and the database is possibly too corrupt to be repaired.
	
	
	RESOLUTION
	==========
	
	To resolve this problem, obtain the latest service pack for Exchange Server
	version 5.5. For additional information, please see the following article in the
	Microsoft Knowledge Base:
	
	  Q191014 XGEN: How to Obtain the latest Exchange Server 5.5 Service Pack
	
	The English version of this fix should have the following file attributes or
	later:
	
	Component: Information Store
	
	+------------------------+
	| File name | Version    | 
	+------------------------+
	| Ese.dll   | 5.5.2534.0 | 
	+------------------------+
	
	This hotfix has been posted to the following Internet location as Psp2esei.exe
	(x86) and Psp2esea.exe (Alpha):
	
	  ftp://ftp.microsoft.com/bussys/exchange/exchange-public/fixes/Eng/Exchg5.5/PostSP2/ESE-fix/
	
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Microsoft Exchange Server
	version 5.5. This problem was first corrected in Exchange Server 5.5 Service
	Pack 3.
	
	Additional query words: recover repair defrag -1605 1605 JET_errKeyDuplicate
	======================================================================
	Keywords          : exc55 EXC55SP3Fix 
	Technology        : kbExchangeSearch kbExchange550 kbZNotKeyword2
	Version           : winnt:5.5
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
