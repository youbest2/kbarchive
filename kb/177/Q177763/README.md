---
layout: page
title: "Q177763: XADM: Troubleshooting Failure to Generate Offline Address Book"
permalink: /kb/177/Q177763/
---

## Q177763: XADM: Troubleshooting Failure to Generate Offline Address Book

{% raw %}

	Article: Q177763
	Product(s): Microsoft Exchange
	Version(s): 4.0,5.0
	Operating System(s): 
	Keyword(s): exc4 exc5
	Last Modified: 02-AUG-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Server, versions 4.0, 5.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	This article is a troubleshooting guide to use when an attempt to generate the
	offline address book (OAB) fails with errors.
	
	One or more of the following errors may occur. Note that other symptoms besides
	the ones listed may also occur.
	
	- Event ID 5004: Generation of the offline Address Book is complete.
	  Result: The MAPI call failed.<<80004005>>.
	
	- Event ID 5012: Failed to generate offline address book for container: /.
	  Results: An unexpected, unknown error occurred. 8004010b.
	
	- The clients can download the Offline Address Book, without any errors.
	
	- You get the same Event IDs connecting locally and remotely.
	
	- You may also see Errors 1232 or 1233.
	
	MORE INFORMATION
	================
	
	Troubleshooting Procedure
	-------------------------
	
	To troubleshoot, perform the following steps:
	
	1. Ensure that you are logged on as a user with at least Administrator
	  permissions at the Organization, Site, and Configuration levels. If not,
	  change the permissions or log on as someone with those permissions, and then
	  attempt to generate the Offline Address Book. Ensure that the offline address
	  book server is the server you are connected to when generating the OAB.
	
	2. Ensure that the Offline Address Book folder is listed in the Folders on this
	  Information Store option. To confirm whether it is listed, perform the
	  following steps:
	
	  a. In the Administrator window, click Servers, and select a server.
	
	  b. Double-click Public Information Store.
	
	  c. Click Instances.
	
	  If the OAB is not listed, add it to this location and allow time for it to
	  replicate. You should be able to view the properties of the OAB. Now try
	  generating the Address Book.
	
	
	3. If steps 1 and 2 both fail, try generating the OAB on different servers in
	  the site. To do this, use these steps:
	
	  a. Connect to the Exchange Administrator program on another server, and then
	     change the OAB server entry to the new server.
	
	  b. In the Administrator window, click Configuration, and then double- click
	     DS Site Configuration.
	
	  c. Click Offline Address Book and change the OAB server entry to the new
	     server.
	
	  d. Try to generate the OAB.
	
	4. Next try different containers (Recipients, Custom, or Global Address List).
	  Also, create a new container to test.
	
	5. Start the Microsoft Exchange Server Administrator program in raw mode.
	
	  WARNING: Using raw mode of Exchange Server Administrator incorrectly can cause
	  serious problems that may require you to reinstall Windows NT Server and/or
	  Exchange Server. Microsoft cannot guarantee that problems resulting from the
	  incorrect use of raw mode can be solved. Use raw mode at your own risk.
	
	  Expand the site that contains the server. In the Configuration container,
	  expand the Information Store Site Configuration. On the File menu, click Raw
	  Properties. Check the server name listed for Site- Folder-Server, making sure
	  that there is a Replica of the offline address book on this server, and that
	  you can access the properties while you are connected to this server. If not,
	  follow the instructions in step 2, and then try generating the Address Book.
	
	6. If steps 3,4, and 5 fail, restart the Exchange Services in Control Panel.
	  Double-click the Services icon, and run DS/IS consistency adjustment on the
	  server indicated in Site-Folder-Server.
	
	  NOTE: Do not perform the DS/IS consistency adjustment if the replication
	  connection has been broken and will be reconnected later or if Directory
	  Replication is occurring.
	
	  Now try generating the OAB.
	
	7. Check to see if there is more than one Language Template installed in any
	  site. To verify this:
	
	  a. Connect to one server in each site.
	
	  b. Double-click the site name.
	
	  c. Under the Site globe, click Configuration, Addressing, Details, Templates.
	
	  This can also be verified at the following location:
	  Configuration/Addressing/One-Off Address Templates.
	
	  If more than one language is listed, make sure the server generating the OAB
	  has the same languages installed in its site. When this situation exists, it
	  can be resolved by either removing the additional language(s) from the other
	  sites or installing the language templates in the site that is having
	  problems generating the OAB.
	
	8. Check the version of the Mapi32.dll file. It should match the appropriate
	  version of Exchange Server. The version numbers can be verified according to
	  the instructions in Microsoft Knowledge Base article Q172036, "INFO: MAPI
	  Version Cross Reference."
	
	
	9. Shut down the Exchange Server computer and restart it. There may be an issue
	  involving cached information or a locked open file that's needed for address
	  book generation.
	
	10. If all of the above steps seem to result in the same errors and/or events,
	  it will be necessary to implement Guidgen on the Exchange Server computer.
	
	CAUTION: The Guidgen utility should be used with caution. Guidgen will rebuild
	(erase) all the site folders. Before using Guidgen, Oabgen.dll may be the better
	solution.
	
	NOTE: At each step, check the application log for errors. Run the Guidgen utility
	on the server that will become the new Site-Folder-Server. This will delete the
	existing Offline Address Book. After this has been successfully done, the
	Information Store on each server in the site, must be stopped and restarted
	before generating the offline address Book.
	
	
	Additional query words:
	
	======================================================================
	Keywords          : exc4 exc5 
	Technology        : kbExchangeSearch kbExchange500 kbExchange400 kbZNotKeyword2
	Version           : :4.0,5.0
	Issue type        : kbinfo
	
	=============================================================================
	

{% endraw %}
