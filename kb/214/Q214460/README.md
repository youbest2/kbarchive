---
layout: page
title: "Q214460: DSMN - Access Violation in Swsvc.exe When Comparing Two Strings"
permalink: /kb/214/Q214460/
---

## Q214460: DSMN - Access Violation in Swsvc.exe When Comparing Two Strings

{% raw %}

	Article: Q214460
	Product(s): Microsoft Windows NT
	Version(s): winnt:4.0
	Operating System(s): 
	Keyword(s): kbWinNT400sp5fix
	Last Modified: 16-MAY-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Server version 4.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	Directory Services for NetWare (DSMN) fails intermittently, generating the
	following Dr. Watson error:
	
	  The application swsvc.exe has generated an application error.
	
	The following message is also written to the System Event Log:
	
	  Event ID: 4097: The application, exe\swsvc.dbg, generated an application
	  error. The exception is c0000005 at address 77a056e1 (wcsicmp).
	
	CAUSE
	=====
	
	The DSMN service will fail periodically when attempting to rename an account
	(user, or local or a global group). For example, it fails when the
	pszOldAcctName is set to a null value and Windows NT attempts to dereference
	this Null pointer in the _wcsicmp() routine. There are several conditions in the
	SwpRenameAccount() routine where the pszOldAcctName string can be set to a Null
	value; however, Windows NT never tests this string before making a call to
	_wcsicmp() routine.
	
	
	RESOLUTION
	==========
	
	To resolve this problem, obtain the latest service pack for Windows NT 4.0 or
	the individual software update. For information on obtaining the latest service
	pack, please go to:
	
	- http://www.microsoft.com/Windows/ServicePacks/
	
	-or-
	
	- Q152734 How to Obtain the Latest Windows NT 4.0 Service Pack
	
	For information on obtaining the individual software update, contact Microsoft
	Product Support Services. For a complete list of Microsoft Product Support
	Services phone numbers and information on support costs, please go to the
	following address on the World Wide Web:
	
	  http://support.microsoft.com/default.aspx?scid=fh;EN-US;CNTACTMS
	
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Windows NT version 4.0. This
	problem was first corrected in Windows NT version 4.0 Service Pack 5.
	
	Additional query words: 4.00 swchglog.c
	
	======================================================================
	Keywords          : kbWinNT400sp5fix 
	Technology        : kbWinNTsearch kbWinNT400search kbWinNTSsearch kbWinNTS400search kbWinNTS400
	Version           : winnt:4.0
	Hardware          : ALPHA x86
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
