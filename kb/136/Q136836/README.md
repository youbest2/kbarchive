---
layout: page
title: "Q136836: Disk Defragmenter May Seem to Stop Responding"
permalink: /kb/136/Q136836/
---

## Q136836: Disk Defragmenter May Seem to Stop Responding

{% raw %}

	Article: Q136836
	Product(s): Microsoft Windows 95.x Retail Product
	Version(s): WINDOWS:95
	Operating System(s): 
	Keyword(s): win95 defrag kbDefrag
	Last Modified: 01-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows 95 
	- Microsoft Plus! for Windows 95 
	- Microsoft Windows 95 OEM Service Release, version 1.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When you run Disk Defragmenter, the progress gauge may not move for a long time,
	even though it seems that the hard disk is being accessed. In some cases, Disk
	Defragmenter may seem to stop responding (hang). This problem frequently occurs
	when Disk Defragmenter is between 5 and 10 percent finished.
	
	CAUSE
	=====
	
	This problem can occur when Disk Defragmenter encounters an area on the hard
	disk that takes a long time to defragment, but for which Disk Defragmenter did
	not reserve space on the progress gauge. This problem typically occurs when Disk
	Defragmenter underestimates the amount of time it will take to defragment a
	particular area of the drive.
	
	In particular, because removing deleted folder entries can take a long time,
	emptying the Temporary Internet Files folder or deleting a large number of files
	from another folder on your hard disk can cause this problem to occur. When the
	problem occurs for this reason, it occurs when Disk Defragmenter is between 5
	and 10 percent finished because this is when Disk Defragmenter removes deleted
	folder entries.
	
	The Norton Desktop for Windows Smartcan tool creates an empty folder whose format
	can also cause this problem to occur. Disk Defragmenter reserves no progress
	gauge space for this folder, but often takes up to 30 minutes to process the
	folder, making sure that the folder is actually empty and marking the
	corresponding clusters so that they can be used.
	
	RESOLUTION
	==========
	
	Allow Disk Defragmenter to continue as long as the hard disk light indicates
	that the drive is being accessed. Do not use the Close Program dialog box to
	quit Disk Defragmenter. The process gauge will start moving again and Disk
	Defragmenter will start responding again when Disk Defragmenter finishes
	processing the area on the hard disk that is taking a long time to defragment.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Windows 95, Windows 95 OEM
	Service Release 1, and Microsoft Plus! for Windows 95. This problem does not
	occur with Windows 95 OEM Service Release 2.
	
	======================================================================
	Keywords          : win95 defrag kbDefrag 
	Technology        : kbWin95search kbGamesSearch kbPlusSearch kbOPKSearch kbZNotKeyword3 kbPlus95
	Version           : WINDOWS:95
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
