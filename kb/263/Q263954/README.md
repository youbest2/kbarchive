---
layout: page
title: "Q263954: Possible Loss of Transactions in Microsoft Metadirectory Service"
permalink: /kb/263/Q263954/
---

## Q263954: Possible Loss of Transactions in Microsoft Metadirectory Service

{% raw %}

	Article: Q263954
	Product(s): Microsoft Windows NT
	Version(s): 2.1
	Operating System(s): 
	Keyword(s): kberrmsg
	Last Modified: 16-JUL-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Metadirectory Services, version 2.1 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	The Microsoft Metadirectory Services (MMS) Management Agent (MA) log reports the
	following message:
	
	  Export DELTA START: 981022113642-0400 ---- END: 981030103914-0500.
	  WARNING: Possible loss of transactions [Thu May 22 11:36:42 1999 - Fri May 23
	  21:16:49 1999]
	
	The message suggests that the configuration of the transaction stack is too
	small. This means that the transaction stack does not contain transactions from
	the last update time that the MA made to the Connected Directory. This behavior
	occurs when the transaction stack rolls over.
	
	MORE INFORMATION
	================
	
	In view of this behavior, you need to perform a full synchronization at least
	once to issue possible updates that were not available in the transaction
	stack.
	
	You are able to vary the configuration of the size of the transaction stack. To
	configure the size of the transaction stack, the db5cfg file must be edited. The
	db5cfg file is located in the \zoomserv\data\config directory.
	
	The default size of the transaction stack in MMS 2.1 is 64 megabytes. The maximum
	size of the stack is 1 gigabyte. In MMS 2.2, the default size of the transaction
	stack is 512 megabytes.
	
	To edit the db5cfg file:
	
	- Stop the MMS service.
	
	- Locate the file in the \zoomserv\data\config directory.
	
	- Open the file with a text editor.
	
	- Increase the size of the transaction stack. By default, it is set to 64000000
	  (or 64 megabytes). For example, changing the value to 256000000 will save
	  256MB of transactions. It may be necessary to try several values until a
	  value large enough is found.
	
	Below is a sample file. In this example, the stack is being set to 64 megabytes.
	
	  ######################################################################
	  # FILE:  db5cfg                                                      #
	  # DATABASE CONFIGURATION FILE                                        #
	  ######################################################################
	  #
	  context_prefix                  dc=microsoft,dc=com
	  db5_local_dsa_name       
	  DsaName=test,ou=Applications,dc=microsoft,dc=com
	  db5_local_mta_name
	  MtaName=MtaName,ou=Applications,dc=microsoft,dc=com
	  db5_local_x400_domain_name      p=yourPRMD/a=yourADMD/c=yourCo
	  db5_local_x400_msg_id_sig       uniqueID
	  #db5_rel_db_dir 	           path_to_directory
	  #db5_asn_db_dir      	   path_to_directory
	  #db5_hash_db_dir     	   path_to_directory
	  #db5_tran_db_dir     	   path_to_directory
	  #db5_fileattr_dir    	   path_to_directory
	  db5_max_tran_file_size          64000000   (SET THE VALUE HERE)
	  maximum_adminpoints_cached      360
	  maximum_adminlinks_cached       4096
	  hostname       test.microsoft.com
	  Installed      2.1 Build 0804.000 04/26/2000 11:36:07
	  Upgraded       05/09/2000 14:20:16 to 2.2 Build 0504.1085
	
	Additional query words: MMS delta transactions foreign export
	
	======================================================================
	Keywords          : kberrmsg 
	Technology        : kbMMSSearch kbMMS210
	Version           : :2.1
	Issue type        : kbinfo
	
	=============================================================================
	

{% endraw %}
