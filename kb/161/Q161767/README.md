---
layout: page
title: "Q161767: Wnap.exe GP Faults During a Windows NT Password Change"
permalink: /kb/161/Q161767/
---

## Q161767: Wnap.exe GP Faults During a Windows NT Password Change

{% raw %}

	Article: Q161767
	Product(s): Microsoft SNA Server
	Version(s): WINDOWS:2.11 SP1,3.0
	Operating System(s): 
	Keyword(s): kbnetwork
	Last Modified: 13-JUN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft SNA Server, versions 2.11 SP1, 3.0 
	-------------------------------------------------------------------------------
	
	
	SYMPTOMS
	========
	
	During a Windows NT password change, the SNA Server Windows 3.x client software
	may encounter a general protection fault (GPF) and display the following error:
	
	  WNAP caused a General Protection Fault in module WDMOD.DLL at 0015:038E
	
	This problem occurs if the combined user ID and domain name field length is seven
	or eight characters. This problem may also lead to a buffer pool corruption
	error on the server, causing SnaBase to fail abnormally with the following
	Windows NT application event log errors:
	
	  Event: 624
	  Source: SNA Server
	  Creating dump file C:\SNA\traces\snadump.log for SNABASE.EXE
	
	  Event: 686
	  Source: SNA Base Service
	  SNA Server Internal buffer pool error.
	   Reason  = Invalid Owner Id
	   Module  = C:\SNA\system\SNABASE.EXE
	   Process = 143
	   Pool    = TRUSTED ELTS
	   Details = Current Owner Id <value>, Correct ID <value>
	
	NOTE: The SNA Server 2.0, 2.1 and 2.11 Windows 3.x clients do not support the
	Windows NT password change feature if the user's password has expired or if the
	user is required to change his or her password on the next logon. Password
	change support was added to the SNA Server Windows 3.x client software in 2.11
	Service Pack 1.
	
	CAUSE
	=====
	
	The SNA Server client improperly generates the client logon response to send to
	the server when the combined user ID and domain are seven or eight characters
	long. In some cases, this causes an invalid message to be sent to the server,
	leading to an SnaBase buffer pool error.
	
	RESOLUTION
	==========
	
	To resolve this problem, obtain the hotfix mentioned below.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in SNA Server version 2.11 Service
	Pack 1 and 3.0.
	
	
	A supported fix is now available, and should be applied only to systems
	experiencing this specific problem. Unless you are severely impacted by this
	specific problem, Microsoft recommends that you wait for the next Service Pack
	that contains this fix. Contact Microsoft Technical Support for more
	information.
	
	
	
	Additional query words: prodsna 2.11.SP1 3.00 SP1
	
	======================================================================
	Keywords          : kbnetwork 
	Technology        : kbAudDeveloper kbSNAServSearch kbSNAServ300 kbSNAServ211SP1
	Version           : WINDOWS:2.11 SP1,3.0
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
