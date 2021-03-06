---
layout: page
title: "Q248987: XCLN: Out of Office Rule Does Not Work w/ Prohibit Send Option"
permalink: /kb/248/Q248987/
---

## Q248987: XCLN: Out of Office Rule Does Not Work w/ Prohibit Send Option

{% raw %}

	Article: Q248987
	Product(s): Microsoft Exchange
	Version(s): 4.0,5.0,8.0,8.01,8.02,8.03,8.04,8.1,8.2,SR-1 Enterprise Update
	Operating System(s): 
	Keyword(s): 
	Last Modified: 24-APR-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Windows 95/98 client, versions 4.0, 5.0 
	- Microsoft Exchange Windows NT client, versions 4.0, 5.0 
	- Microsoft Exchange Windows 3.x client, versions 4.0, 5.0 
	- Microsoft Outlook, Exchange Server Edition, version 8.0 
	- Microsoft Outlook for Macintosh, Exchange Server Edition, versions 8.0, 8.1, 8.2 
	- Microsoft Outlook 97, versions 8.0, 8.01, 8.02, 8.03, 8.04, SR-1 Enterprise Update 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When a Microsoft Exchange Server recipient receives an e-mail message and their
	Out of Office (OOF) rule is turned on, the OOF rule may not work. The recipient
	may also be prompted to turn off the OOF rule every time that they start the
	Microsoft Exchange client or Microsoft Outlook. Even after the recipient turns
	off the OOF rule, the rule may still be turned on. (To see that this is so, the
	recipient can view the Out of Office Assistant command on the Tools menu.)
	
	CAUSE
	=====
	
	The recipient's mailbox may have the Prohibit Send option set to a limit that
	has been reached.
	
	RESOLUTION
	==========
	
	To resolve this issue, follow these steps:
	
	1. Start the Microsoft Exchange Server Administrator program.
	
	2. Open the recipient's mailbox properties.
	
	3. On the Limits tab, increase the Prohibit Send value to allow the recipient to
	  send e-mail messages successfully.
	
	4. Log on to the recipient's mailbox and turn off the OOF rule.
	
	5. On the Tools menu, click Out of Office Assistant to turn on the OOF rule
	  again.
	
	
	Additional query words: process fire
	
	======================================================================
	Keywords          :  
	Technology        : kbHWMAC kbOSMAC kbOutlookSearch kbExchangeSearch kbExchange500 kbExchange400 kbExchangeClientSearch kbZNotKeyword kbOutlook97 kbZNotKeyword2 kbOutlook97Search kbZNotKeyword3 kbOutlookMacSearch kbOutlook801 kbOutlook802 kbOutlook803 kbOutlook804 kbOutlook97EntSR1 kbExchange400NT kbExchange500NT kbOutlook800Mac kbOutlook810Mac kbOutlook820Mac kbExchange400Win95 kbExchange500Win95
	Version           : :4.0,5.0,8.0,8.01,8.02,8.03,8.04,8.1,8.2,SR-1 Enterprise Update
	Issue type        : kbprb
	
	=============================================================================
	

{% endraw %}
