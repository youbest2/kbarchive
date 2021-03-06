---
layout: page
title: "Q193322: XCON: Route Selection Criteria"
permalink: /kb/193/Q193322/
---

## Q193322: XCON: Route Selection Criteria

{% raw %}

	Article: Q193322
	Product(s): Microsoft Exchange
	Version(s): winnt:4.0,5.0,5.5
	Operating System(s): 
	Keyword(s): exc4 exc5 exc55
	Last Modified: 06-AUG-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Server, versions 4.0, 5.0, 5.5 
	-------------------------------------------------------------------------------
	
	
	SUMMARY
	=======
	
	After the message transfer agent (MTA) has used the Gateway Address Routing
	Table (GWART) to determine an appropriate list of possible connectors, the MTA
	must then decide which connector is the best one to use. The following criteria
	are processed in sequential elimination order to determine the appropriate
	connector or connectors. Each connector or group of connectors that meets the
	criteria for each step is passed to the next step for testing.
	
	1. Eliminate any inbound connector that may have delivered the message from
	  another site.
	
	2. Select the connectors that are not at maximum retry. The selection process
	  checks two counters: Retry Count and Max Open Retries. The Retry Count
	  counter of the message is compared to the Max Open Retries counter of the
	  connector. Only connectors that are not at maximum pass this step.
	
	3. Select the connectors that will connect the soonest, also called the
	  activation schedule, which has four states:
	
	   - Active Now
	
	   - Will Become Active in the Future
	
	   - Never
	
	   - Remote Initiated
	
	4. Select the connectors that have tried to connect the fewest times. The
	  message Retry Count counter and the Max Open Retries counter are compared
	  again. This time, only the connectors that have been attempted the fewest
	  times are selected.
	
	5. Select the connectors that are not currently retrying a connection. Each MTA
	  maintains an Open Retry timer. This timer indicates how long it has been
	  since the MTA attempted a failed association. The MTA can only know the Open
	  Retry timer for any connectors on itself. Because of that, if the connectors
	  being considered are on different computers, this step is bypassed.
	
	6. Select the connectors that have the lowest cost value assignment.
	
	7. Select local connectors over remote connectors. Local connectors exist when
	  the MTA that is processing the selection criteria has the authorization to
	  send the message directly to the remote site (for example, an X.400 messaging
	  bridgehead server). Remote connectors require the MTA that is processing the
	  selection criteria to pass the message to a messaging bridgehead server
	  before it can be passed to the remote site.
	
	MORE INFORMATION
	================
	
	Exchange Server version 4.0 Service Pack 4 and Exchange Server version 5.0
	Service Pack 1 offer a registry entry to alter the selection criteria.
	
	For additional information about instructions on how to enable this feature,
	click the article number below to view the article in the Microsoft Knowledge
	Base:
	
	  Q166567 XCON: How to Enable Lowest Cost Routes Only
	
	This feature adds a new "Use Lowest Cost Routes Only" registry flag. If this flag
	is set, the MTA always routes to the lowest cost link. The one exception is
	that, if the activation schedule of the lower cost link is currently inactive
	and the higher cost link is active, the rerouting is to the higher cost link.
	
	NOTE: A route with an address space of * is chosen over an address space of
	<blank> and overrides the cost value for connectors. The most common
	occurrence of this is with the Internet Mail Service (Internet Mail Connector in
	Exchange Server version 4.0).
	
	Additional query words:
	
	======================================================================
	Keywords          : exc4 exc5 exc55 
	Technology        : kbExchangeSearch kbExchange500 kbExchange550 kbExchange400 kbZNotKeyword2
	Version           : winnt:4.0,5.0,5.5
	Issue type        : kbinfo
	
	=============================================================================
	

{% endraw %}
