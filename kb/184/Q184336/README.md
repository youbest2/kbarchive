---
layout: page
title: "Q184336: XCLN: Message Format Unavailable After Outlook 98 Is Installed"
permalink: /kb/184/Q184336/
---

## Q184336: XCLN: Message Format Unavailable After Outlook 98 Is Installed

{% raw %}

	Article: Q184336
	Product(s): Microsoft Exchange
	Version(s): 98
	Operating System(s): 
	Keyword(s): 
	Last Modified: 27-JUN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Outlook 98 Deployment Kit 
	- Microsoft Outlook 98 
	-------------------------------------------------------------------------------
	
	
	SYMPTOMS
	========
	
	After installing Microsoft Outlook 98 through the Outlook Deployment Kit Wizard,
	the drop-down list to change the message format options on the Mail Format tab
	(click Options on the Tools menu) is no longer available.
	
	
	CAUSE
	=====
	
	The administrator that created the Outlook install packages with the Outlook
	Deployment Kit (ODK) locked down the Mail Format setting by choosing the mail
	format before creating the install packages.
	
	An option in the fifth stage (Customize User Settings Stage) of the ODK allows
	the administrator to lock down the Mail Format setting for users. This setting
	is titled "Corporate/WorkGroup Mail Editor" for Corporate or Workgroup (CW)
	Support or "Internet Only Mail Editor" for Internet Mail Only (IMO) Support.
	These settings are in the Outlook 98/Email section in the option tree in the
	left pane of this dialog box.
	
	Administrators can select from the following four options:
	
	- HTML
	
	- Microsoft Outlook Rich Text
	
	- Plain Text
	
	- Microsoft Word
	
	RESOLUTION
	==========
	
	Administrators that want to allow users to change this setting must leave the
	Message Format option blank. When Outlook 98 is installed, the user will be able
	to change the message format.
	
	
	MORE INFORMATION
	================
	
	To find out which version of Outlook 98 you have installed, on the Help menu,
	click About Microsoft Outlook. The second line of text will read either:
	
	  Internet Only Support
	
	  -or-
	
	  Corporate or Workgroup
	
	Additional query words: missing grey greyed gray grayed
	
	======================================================================
	Keywords          :  
	Technology        : kbOutlookSearch kbExchangeSearch kbExchange550 kbZNotKeyword2 kbOutlookDeployKitSearch kbOutlook98DeployKit
	Version           : :98
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
