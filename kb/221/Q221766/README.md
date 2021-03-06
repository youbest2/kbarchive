---
layout: page
title: "Q221766: Registry Permissions Not Inherited Properly"
permalink: /kb/221/Q221766/
---

## Q221766: Registry Permissions Not Inherited Properly

{% raw %}

	Article: Q221766
	Product(s): Microsoft Windows NT
	Version(s): winnt:4.0
	Operating System(s): 
	Keyword(s): 
	Last Modified: 10-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Server version 4.0 
	- Microsoft Windows NT Server version 4.0, Terminal Server Edition 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	After securing the registry with C2Config, subkeys created in the
	HKEY_LOCAL_MACHINE\SOFTWARE, HKEY_LOCAL_MACHINE\SOFTWARE\Classes,
	HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft, and HKEY_LOCAL_MACHINE\SOFTWARE\Secure
	keys do not inherit the expected permissions.
	
	CAUSE
	=====
	
	C2Config sets the inherited permissions separately from the object permissions.
	The permissions to be set are defined in the C2RegACL.inf file, and it does not
	include the permissions to be inherited by subkeys.
	
	RESOLUTION
	==========
	
	To resolve this problem you should add the permissions to be inherited to the
	C2RegACL.inf file.
	
	Example:
	
	Section of C2RegACL.inf before modifications:
	
	  [HKEY_LOCAL_MACHINE\SOFTWARE]
	  BUILTIN\Administrators = FULL
	  CREATOR OWNER =  FULL
	  SYSTEM = FULL
	  Everyone = QV, SV, CS, ES, NT, DE, RC
	
	Section of C2RegACL.inf after adding inherited permissions:
	
	  [HKEY_LOCAL_MACHINE\SOFTWARE]
	  BUILTIN\Administrators = FULL
	  BUILTIN\Administrators = INHERIT, FULL
	  CREATOR OWNER =  FULL
	  CREATOR OWNER =  INHERIT, FULL
	  SYSTEM = FULL
	  SYSTEM = INHERIT, FULL
	  Everyone = QV, SV, CS, ES, NT, DE, RC
	  Everyone = INHERIT, QV, SV, CS, ES, NT, DE, RC
	
	Note the INHERIT entry in the permissions. This is the option that sets the
	permissions that will be inherited by subkeys.
	
	Additional query words: SECURITY CONFIGURATION EDITOR
	
	======================================================================
	Keywords          :  
	Technology        : kbWinNTsearch kbWinNT400search kbWinNTSsearch kbWinNTS400search kbWinNTS400 kbNTTermServ400 kbNTTermServSearch
	Version           : winnt:4.0
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
