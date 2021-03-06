---
layout: page
title: "Q196957: Using SFGW to Save Files May Cause Task Dump on S/36 or AS/36"
permalink: /kb/196/Q196957/
---

## Q196957: Using SFGW to Save Files May Cause Task Dump on S/36 or AS/36

{% raw %}

	Article: Q196957
	Product(s): Microsoft SNA Server
	Version(s): WINDOWS:4.0 SP1
	Operating System(s): 
	Keyword(s): 
	Last Modified: 13-JUN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft SNA Server, version 4.0 SP1 
	-------------------------------------------------------------------------------
	
	
	SYMPTOMS
	========
	
	When you use the SNA Server's Shared Folders Gateway (SFGW) feature to save
	files on a System/36 (S/36) and Advanced System/36 (AS/36) computer, the S/36 or
	AS/36 computer may issue a task dump and register a process failure. The S/36 or
	AS/36 computer will remain operational after this occurs, but the file(s) are
	not saved in the shared folder(s) on the system.
	
	This problem was observed when using Microsoft Word to edit one or more files
	located on the S/36 shared folders drive, using the Microsoft Word RFTDCA
	converter. However, this problem could also occur when using other applications
	to manipulate files on the S/36 drive.
	
	CAUSE
	=====
	
	The SFGW service has a pool of APPC conversations, which are used for processing
	file requests. A file can be created using one conversation and then accessed
	using other conversations in the pool. This mechanism can cause S/36 and AS/36
	systems to generate a task dump if a conversation is used to access multiple
	files opened for writing. This mechanism works fine with AS/400 systems.
	
	RESOLUTION
	==========
	
	Microsoft has confirmed this to be a problem in SNA Server version 4.0 Service
	Pack 1. This problem was corrected in the latest SNA Server version 4.0 U.S.
	Service Pack. For information on obtaining this Service Pack, query on the
	following word in the Microsoft Knowledge Base (without the spaces):
	
	  S E R V P A C K
	
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in SNA Server version 4.0 Service
	Pack 1 when using the update that adds S/36 support to the SFGW feature.
	
	MORE INFORMATION
	================
	
	The SFGW feature requires the SNA Server 4.0 post-Service Pack 1 update referred
	to in the following Knowledge Base article to support connections to S/36 and
	AS/36 systems:
	
	  Q194934 Shared Folders Gateway Doesn't Support S/36 or AS/36
	
	The problem described in this article only applies to SNA Server 4.0 Service Pack
	1 systems that have applied the update described in the article listed here.
	
	After you apply the update to prevent a task dump from occurring on S/36 and
	AS/36 systems when saving files through SFGW, the number of files that can be
	opened for write access will be limited to the number of parallel sessions
	negotiated for the QPCSUPP mode. If the QPCSUPP mode is configured for a
	parallel session limit of 8, only eight files can be opened for write access on
	the S/36 or AS/36 computer through the SFGW service. If another request to open
	a file for write access is received while eight files are open, the request will
	be queued until one of the previous eight files is closed. The limit of open
	files only applies to SFGW connections to S/36 or As/36 systems. Other SFGW
	connections to AS/400 systems on the same SNA Server will not be affected by
	this limitation.
	
	NOTE: When using Microsoft Word to edit files located on the S/36 computer
	(through the shared folders gateway), Word creates a temporary file on the
	destination directory. When the user saves their changes (or if Word is
	configured to autosave), the temporary file is copied over the original file
	name.
	
	Additional query words:
	
	======================================================================
	Keywords          :  
	Technology        : kbAudDeveloper kbSNAServSearch kbSNAServ400SP1
	Version           : WINDOWS:4.0 SP1
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
