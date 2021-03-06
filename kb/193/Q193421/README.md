---
layout: page
title: "Q193421: SMS: Audit16 Fails on Long User Names"
permalink: /kb/193/Q193421/
---

## Q193421: SMS: Audit16 Fails on Long User Names

{% raw %}

	Article: Q193421
	Product(s): Microsoft Systems Management Server
	Version(s): WINNT:1.2
	Operating System(s): 
	Keyword(s): kbsms120 kbAudit kbDSupport smsaudit
	Last Modified: 20-MAY-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Systems Management Server version 1.2 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	Audit16 will fail if it encounters a user name string that is longer than 32
	characters. An audit MIF will not be produced, and the following error will be
	in the audit log file:
	
	  A File error occurred:  File read error in SMS.INI file.
	
	CAUSE
	=====
	
	Audit16 reads the user name from the [User Name] section of the Sms.ini file.
	Audit16 stores this user name in a 32-character buffer. If the string is longer
	than 32 characters, Audit16 gets a fatal error and is stopped.
	
	Typically, these long user names occur on Novell NDS clients, and are of the
	form:
	
	  username.department.section.division.Corporate
	
	RESOLUTION
	==========
	
	A supported fix that corrects this problem is now available from Microsoft, but
	has not been fully regression tested and should be applied only to systems
	experiencing this specific problem. If you are not severely affected by this
	specific problem, Microsoft recommends that you wait for the next Systems
	Management Server service pack that contains this fix.
	
	To resolve this problem immediately, contact Microsoft Product Support Services
	to obtain the fix. For a complete list of Microsoft Product Support Services
	phone numbers and information on support costs, please go to the following
	address on the World Wide Web:
	
	  http://support.microsoft.com/default.aspx?scid=fh;EN-US;CNTACTMS
	
	The English version of this fix should have the following file attributes or
	later:
	
	  Date       Time               Size    File name   Platform
	  ----------------------------------------------------------
	  09/28/98   02:19pm            134,348 Audit16.exe (x86)
	
	
	WORKAROUND
	==========
	
	To work around this problem, you can manually reduce the user name string in the
	[User Name] section of the Sms.ini to fewer than 32 characters.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Systems Management Server
	version 1.2.
	
	MORE INFORMATION
	================
	
	To install the hotfixm perform the following steps:
	
	1. Replace the Audit16.exe file in the
	  <Sms_root>\Primsite.srv\Audit\Package\X86.bin directory with the
	  hotfixed version.
	
	  NOTE: You can perform Step 1 automatically by using Hotfix.exe with the
	  provided Hotfix.ini file.
	
	2. If you have already distributed an audit job to your clients, send a new job
	  and select the Send Even If Previously Sent option. This will cause the
	  despooler to update the package on the distribution servers.
	
	Additional query words: prodsms win16 wfw username terminates
	
	======================================================================
	Keywords          : kbsms120 kbAudit kbDSupport smsaudit 
	Technology        : kbSMSSearch kbSMS120
	Version           : WINNT:1.2
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
