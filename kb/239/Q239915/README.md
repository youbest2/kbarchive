---
layout: page
title: "Q239915: SMS: &quot;Insert Disk in Drive A:&quot; Message During Hardware Inventory"
permalink: /kb/239/Q239915/
---

## Q239915: SMS: &quot;Insert Disk in Drive A:&quot; Message During Hardware Inventory

{% raw %}

	Article: Q239915
	Product(s): Microsoft Systems Management Server
	Version(s): winnt:2.0,2.0 SP1
	Operating System(s): 
	Keyword(s): kbHinv
	Last Modified: 06-AUG-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Systems Management Server versions 2.0, 2.0 SP1 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	During a hardware inventory cycle of Microsoft Windows NT, Microsoft Windows 95,
	or Microsoft Windows 98 clients, you may receive the following prompt:
	
	  Insert disk in drive A:
	
	If you examine the client's Hinv32.log file, hardware inventory was enumerating
	the Windows Management Instrumentation (WMI) class Win32_LogicalDisk when the
	prompt was generated.
	
	CAUSE
	=====
	
	The WMI class Win32_LogicalDisk is enumerated during the hardware inventory
	cycle, which queries for volume information on drives attached to the client.
	WMI normally suppresses the "Insert disk in drive" prompt, but on occasion may
	be overridden.
	
	
	RESOLUTION
	==========
	
	A supported fix is now available from Microsoft, but it is only intended to
	correct the problem that is described in this article. Only apply it to systems
	that are experiencing this specific problem. This fix may receive additional
	testing. Therefore, if you are not severely affected by this problem, Microsoft
	recommends that you wait for the next Systems Management Server service pack
	that contains this fix.
	
	To resolve this problem immediately, contact Microsoft Product Support Services
	to obtain the fix. For a complete list of Microsoft Product Support Services
	phone numbers and information about support costs, visit the following Microsoft
	Web site:
	
	  http://support.microsoft.com/default.aspx?scid=fh;EN-US;CNTACTMS
	
	NOTE: In special cases, charges that are ordinarily incurred for support calls
	may be canceled if a Microsoft Support Professional determines that a specific
	update will resolve your problem. The usual support costs will apply to
	additional support questions and issues that do not qualify for the specific
	update in question.
	
	The English-language version of this fix should have the following file
	attributes or later:
	
	  Date        Version          Size    File name   Platform
	  -----------------------------------------------------------
	  08/04/99   2.00.1380.1013  3,806,179 Wbemsdk.exe   x86
	  08/10/99   2.00.1380.1013         67 Compver.ini   x86
	  08/04/99   2.00.1380.1013  7,163,252 Wbemsdk.exe   Alpha
	  08/10/99   2.00.1380.1013         67 Compver.ini   Alpha
	
	
	
	WORKAROUND
	==========
	
	To temporarily work around the problem, you can disable the WMI class
	Win32_LogicalDisk enumeration. To disable hardware inventory of the
	Win32_Logical disk class, you can edit the Sms_def.mof file.
	
	WARNING: Exercise caution when editing .mof files. You should create a backup
	copy of the .mof file before editing it.
	
	Modify the master Sms_def.mof file on each site server in turn, or modify it on
	one server and then copy it to all others. The Sms_def.mof file is located in
	the X:\SMS\Inboxes\Clifiles.src\Hinv folder. You can open the file with WordPad
	or Notepad. To disable win32_LogicalDisk enumeration, locate the following
	entry:
	
	  [SMS_Report (TRUE), SMS_Group_Name ("Logical Disk"),
	  ResID(2100),ResDLL("SMS_RXPL.dll"),
	  SMS_Class_ID("MICROSOFT|LOGICAL_DISK|1.0")]
	  class Win32_LogicalDisk : SMS_Class_Template
	
	Change the first line "[SMS_Report (TRUE)" to "(FALSE)" to disable the entire
	class.
	
	STATUS
	======
	
	Microsoft has confirmed that this is a problem in Systems Management Server
	versions 2.0 and 2.0 Service Pack 1.
	
	MORE INFORMATION
	================
	
	To install the hotfix, follow these steps on each Systems Management Server 2.0
	and 2.0 Service Pack 1 site server :
	
	1. Stop the SMS_SITE_COMPONENT_MANAGER and SMS_EXECUTIVE site services.
	
	2. Copy the updated Wbemsdk.exe file to the site server's
	  SMS\bin\<Platform> folder.
	
	3. Copy the updated Wbemsdk.exe file to the site server's
	  SMS\Inboxes\Clicomp.src\Wbem\<Platform> folder.
	
	4. Copy the updated Compver.ini file to the site server's
	  SMS\Inboxes\Clicomp.src\WBEM folder.
	
	5. Start the SMS_SITE_COMPONENT_MAANGER and SMS_EXECUTIVE services.
	
	NOTE: After the SMS Inbox Manager component updates the Client Access Points
	(CAP), the clients can gain access to the updated files. The default Client
	Configuration Installation Manager (CCIM) polling interval is 23 hours.
	Therefore, it may take up to 23 hours for the hotfix files to be propagated to
	the clients. To speed up this process, you can stop and restart the SMS Client
	service on each client. You can also create a software distribution for one of
	the Resource Kit tools (Setevnt.exe or Cliutils.exe), along with the appropriate
	parameter(s) to start a CCIM work cycle. For information about the proper syntax
	to use with these tools, see the Resource Kit documentation.
	
	Additional query words: prodsms
	
	======================================================================
	Keywords          : kbHinv 
	Technology        : kbSMSSearch kbSMS200 kbSMS200SP1
	Version           : winnt:2.0,2.0 SP1
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
