---
layout: page
title: "Q149179: SMS 1.2 and SQL Server Upgrade"
permalink: /kb/149/Q149179/
---

## Q149179: SMS 1.2 and SQL Server Upgrade

{% raw %}

	Article: Q149179
	Product(s): Microsoft Systems Management Server
	Version(s): winnt:1.0,1.1,1.2,4.21a,6.0
	Operating System(s): 
	Keyword(s): kbinterop kbsetup smssetup
	Last Modified: 27-JUL-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Systems Management Server versions 1.0, 1.1, 1.2 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	Microsoft Systems Management Server uses a SQL Server database to store its
	system information and computer inventory. Before you upgrade an early version
	(1.0 or 1.1) of SMS to version 1.2, you must consider the version of SQL Server
	that contains the SMS database. Different versions of SMS require different
	versions of Microsoft SQL Server, as detailed in the following list:
	
	- SMS version 1.0 supports SQL Server version 4.21a only.
	
	- SMS version 1.1 supports SQL Server version 4.21a and SQL Server 6.x.
	
	- SMS version 1.2 supports SQL Server SQL Server version 6.x.
	
	SQL Server version 4.21a is supported only during the upgrade phase to version
	6.x. SQL Server 4.21a is not supported for usage with SMS version 1.2.
	
	MORE INFORMATION
	================
	
	Upgrading SMS 1.1 to SMS 1.2
	----------------------------
	
	If your SMS 1.1 site has its database on SQL Server version 4.21a, complete the
	following steps, in order, to complete the upgrade:
	
	1. Shut down the site. To do this, run Setup.exe from the SMSSETUP directory on
	  the SMS compact disc, click Continue twice, click Operations, then click
	  Shutdown Site.
	
	2. Back up the SMS database.
	
	3. Upgrade SQL Server 4.21a to SQL Server 6.x.
	
	4. Reset the site. To do this, run Setup.exe from the SMSSETUP directory on the
	  SMS compact disc, click Continue twice, click Operations, then click Reset
	  Site.
	
	5. Upgrade SMS 1.1 to SMS 1.2.
	
	Note that SMS 1.1 supports both SQL Server versions 4.21a and 6.x. This means
	that you can upgrade SQL Server before upgrading from SMS 1.1 to SMS 1.2.
	However, you must perform the SMS upgrade after the SQL Server upgrade.
	
	If you plan to continue using SMS 1.1 with SQL Server 6.x, you need to run the
	sp_site.sql script to restore the stored procedures used by SMS. For more
	information, please see the following article in the Microsoft Knowledge Base:
	
	  Q149178 Upgrading SQL Server Used for an SMS Database
	
	Note that SMS 1.2 automatically restores the stored procedures if SQL Server is
	upgraded.
	
	Additional query words: prodsms
	
	======================================================================
	Keywords          : kbinterop kbsetup smssetup 
	Technology        : kbSMSSearch kbSMS100 kbSMS110 kbSMS120
	Version           : winnt:1.0,1.1,1.2,4.21a,6.0
	
	=============================================================================
	

{% endraw %}
