---
layout: page
title: "Q148783: Poor Sound Quality with Future Domain 850-Series Controllers"
permalink: /kb/148/Q148783/
---

## Q148783: Poor Sound Quality with Future Domain 850-Series Controllers

{% raw %}

	Article: Q148783
	Product(s): Microsoft Windows 95.x Retail Product
	Version(s): 95
	Operating System(s): 
	Keyword(s): win95
	Last Modified: 17-DEC-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows 95 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When you are using a Future Domain TMC-850, TMC-850M, TMC-850MER, or TMC- 850MEX
	SCSI controller with the Future Domain TMC-850/M/MER/MEX SCSI Host Adapter
	driver included with Windows 95, you may experience poor sound quality in some
	multimedia programs. This problem is known to occur with the following
	multimedia programs, but the problem is not program- specific:
	
	- George Shrinks
	
	- Infopedia
	
	CAUSE
	=====
	
	This is a known problem that can occur with the Future Domain SCSI controllers
	listed above when the corresponding protected-mode drivers included with Windows
	95 are used. The Future Domain 850-series SCSI controllers are 8-bit controllers
	that may experience performance problems with more intensive multimedia
	programs, even when the real-mode drivers included with the controller are used.
	However, this poor performance is more pronounced when the protected-mode
	drivers included with Windows 95 are used.
	
	RESOLUTION
	==========
	
	To work around this problem, use the real-mode drivers included with the Future
	Domain SCSI controller and your CD-ROM drive instead of the protected-mode
	drivers included with Windows 95. For information about how to do so, consult
	the documentation included with the devices, or contact the manufacturer. Note
	that when you are using a real-mode driver for the CD-ROM drive, you must also
	load the Mscdex.exe file located in the Windows\Command folder from the
	Autoexec.bat file.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Microsoft Windows 95. We are
	researching this problem and will post new information here in the Microsoft
	Knowledge Base as it becomes available.
	
	Additional query words: choppy repetitive
	
	======================================================================
	Keywords          : win95 
	Technology        : kbWin95search kbZNotKeyword3
	Version           : 95
	
	=============================================================================
	

{% endraw %}
