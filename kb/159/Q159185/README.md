---
layout: page
title: "Q159185: Exchange X.400 MTA over TP4 Sends Only 2 Queued Messages, Stops"
permalink: /kb/159/Q159185/
---

## Q159185: Exchange X.400 MTA over TP4 Sends Only 2 Queued Messages, Stops

{% raw %}

	Article: Q159185
	Product(s): Microsoft Exchange
	Version(s): winnt:4.0
	Operating System(s): 
	Keyword(s): 
	Last Modified: 16-MAR-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Server, version 4.0 
	-------------------------------------------------------------------------------
	
	
	SYMPTOMS
	========
	
	The Microsoft Exchange Server message transfer agent (MTA) configured with an
	X.400 Connector over TP4, (1988, monolog) to a foreign X.400 MTA, only transmits
	two queued messages and fails to send more. Additionally, the association
	between MTAs will not be released.
	
	CAUSE
	=====
	
	Expedited data at the transport layer is being improperly handled by components
	of Winsock and the TP4 protocol driver, Afd.sys and Isotp.sys respectively.
	
	
	WORKAROUND
	==========
	
	To work around this problem:
	
	- Configure the foreign MTA's TP4 (OSI) stack to disable or refuse the use of
	  Transport Expedited Data during transport session negotiation of the
	  association between the MTAs.
	
	Consult the documentation of the foreign MTA for information on how to disable
	this OSI feature.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Windows NT version 3.5x. A
	supported fix is now available, but has not been fully regression-tested and
	should be applied only to systems experiencing this specific problem. This is a
	post-SP5 fix. No additional official service packs are planned for Windows NT
	3.51. Contact Microsoft Technical Support for more information.
	
	
	MORE INFORMATION
	================
	
	Transport Expedited Data is a special feature of the transport portion OSI
	protocol that allows a frame to have a "higher priority" on the network. It is
	the intention that this frame would be processed (up the stack) before other
	pending, but non-expedited frames. It is typically used to signal th t an
	important and timely change is requested, or about to occur (For instance, a
	user hits Ctrl-C on a terminal to signal the other side to cancel the previous
	request and return control to the user. The Ctrl-C may be sent in an expedited
	frame if the application was coded to do so, and expedited data support was
	negotiated by the transport layer).
	
	Microsoft Exchange Server has a "Use Expedited data" check box in the X.400
	Connector's Stack property page. This specifies only whether the MTA will send
	data via expedited transport frames (if that service has been negotiated by the
	transport for the current association). The MTA does not respond any differently
	to incoming data that has arrived via expedited transport frames than it does to
	regular data, nor does selecting this check box change the Windows NT TP4 stack
	behavior.
	
	The Exchange X.400 MTA, when viewed as an OSI application, does not configure or
	directly influence network features of any layer below the Session layer of the
	OSI model. The Windows NT TP4 transport layer was designed to negotiate for the
	use of expedited data, but to honor a refusal of that feature when initiating a
	session. When responding to session establishment requests, the Windows NT TP4
	transport layer accepts whatever the initiating side requests with regard to
	expedited data. There is no way to override or force the Windows NT TP4
	transport layer to require or deny the use of transport expedited data.
	
	Additional query words: hang
	
	======================================================================
	Keywords          :  
	Technology        : kbExchangeSearch kbExchange400 kbZNotKeyword2
	Version           : winnt:4.0
	
	=============================================================================
	

{% endraw %}
