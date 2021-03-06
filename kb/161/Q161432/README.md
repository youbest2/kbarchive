---
layout: page
title: "Q161432: WINS Static Entries Overwritten by Duplicate Group Names"
permalink: /kb/161/Q161432/
---

## Q161432: WINS Static Entries Overwritten by Duplicate Group Names

{% raw %}

	Article: Q161432
	Product(s): Microsoft Windows NT
	Version(s): winnt:3.5,3.51,4.0
	Operating System(s): 
	Keyword(s): kbbuglist kbfixlist
	Last Modified: 09-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows NT Server versions 3.5, 3.51, 4.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	You have created a unique static mapping on a Windows Internet Name Service
	(WINS) server for a non-WINS-enabled computer. Another WINS-enabled workstation
	on the network configures its workgroup name with the same name as the unique
	static mapping and reboots. The static computer <00h> entry for the name
	is no longer unique, it is now a group name with multiple IP addresses, and
	other computers on the network can no longer resolve the original unique name.
	
	CAUSE
	=====
	
	The group registration for the duplicate workgroup name overwrote the static
	unique entry, creating a group registration with the original IP address and the
	new computer's IP address.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Windows NT versions 3.5, 3.51. A
	fix to this problem is in development, but has not been regression-tested and
	may be destabilizing in production environments. Microsoft does not recommend
	implementing this fix at this time. Contact Microsoft Technical Support for more
	information on the availability of this fix.
	
	Microsoft has confirmed this to be a problem in Windows NT version 4.0. This
	problem was corrected in the latest Microsoft Windows NT 4.0 U.S. Service Pack.
	For information on obtaining the service pack, query on the following word in
	the Microsoft Knowledge Base (without the spaces):
	
	  S E R V P A C K
	
	
	Additional query words: windows internet name service mappings
	
	======================================================================
	Keywords          :  kbbuglist kbfixlist
	Technology        : kbWinNTsearch kbWinNT351search kbWinNT350search kbWinNT400search kbWinNTSsearch kbWinNTS400search kbWinNTS400 kbWinNTS351 kbWinNTS350 kbWinNTS351search kbWinNTS350search
	Version           : winnt:3.5,3.51,4.0
	Issue type        : kbbug
	
	=============================================================================
	

{% endraw %}
