---
layout: page
title: "Q156083: SNA Server APPC Error Communicating to Software AG Entire APPC"
permalink: /kb/156/Q156083/
---

## Q156083: SNA Server APPC Error Communicating to Software AG Entire APPC

{% raw %}

	Article: Q156083
	Product(s): Microsoft SNA Server
	Version(s): WINDOWS:2.0,2.1,2.11
	Operating System(s): 
	Keyword(s): kb3rdparty kbnetwork kbprogramming
	Last Modified: 12-JUN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft SNA Server, versions 2.0, 2.1, 2.11 
	-------------------------------------------------------------------------------
	
	
	SYMPTOMS
	========
	
	You may see the following message sequence when you run an APPC TP on SNA Server
	communicating to a partner APPC TP on an MVS host (running on Software AG Entire
	APPC server v1.2.4), over a mapped conversation:
	
	SNA Server            Host
	
	                 <- RH=039020  RU=00 A2 12 FF <lu6.2 data>
	                 <- RH=039020  RU=00 A2 12 FF <lu6.2 data>
	                 <- RH=019020  RU=00 04 12 F3 00 A2 12 FF <lu6.2 data>
	
	RH=879000, RU=08460000 ->
	RH=0A8900, RU=07070889010000 ->
	
	The APPC application running on SNA Server is notified of a conversation failure,
	when the host TP receives an FMH-7 error with a sense code of 08890100, or the
	Transaction Program Error: No data truncation.
	
	CAUSE
	=====
	
	This is a problem in the Software AG Entire APPC Server running on MVS. The RU
	in the third LU6.2 data message sent by the host includes a "Map name" GDS
	command prior to the LU6.2 application data:
	
	  000412F300A212FF....
	
	where 000412F3 = Map Name GDS variable (NULL map name) 00A212FF = LU6.2 data
	(data length of A2)
	
	The SNA Server APPC interface does not support the "Map name" function and
	rejects the data with a sense code of 08460000 (error forthcoming) followed by
	an FMH-7 error and sense data = 08890100.
	
	RESOLUTION
	==========
	
	Currently no fix is available from Software AG.
	
	The APPC application could work around the problem by using basic conversation
	verbs on the mapped conversation, allowing the application to ignore the Map
	Name GDS variable. Here is how the application would need to be modified to
	accomplish this:
	
	- For all APPC calls, change the opcode field to indicate that the Basic verb
	  function is to be called, and change the opext field in the verb control
	  block to AP_BASIC_CONVERSATION.
	
	- To simplify handling of received data, set fill = AP_LL on all receive verbs,
	  to restrict received data records to single LLs only.
	
	- Change the send and receive verbs to handle the 4 leading bytes at the start
	  of the LU6.2 data as follows:
	
	  byte 1,2 = LL field (length of LU6.2 data + 4 bytes, or 32767 max)
	  byte 3,4 = GDS variable, where
	              x12FF = LU6.2 application data, or
	              x12F3 = Map Name GDS variable
	  byte 5+  = LU6.2 application data (32763 bytes max)
	
	  When you get a message containing the Map Name GDS variable, ignore it and
	  look for LU6.2 application data which may follow.
	
	
	NOTE: If the leading bit of the LL field is set to "1", this indicates that
	another LL follows the LU6.2 data. For example, if an APPC application writes
	8KB of data, and if it uses a GDS LU6.2 data size of 4KB, the receiving TP would
	receive the data as follows (if fill=AP_LL is used):
	
	  Data from first receive:   9000 12FF <4KB of data - 4 bytes>
	  Data from second receive:  9000 <4KB of data - 2 bytes>
	  Data from third receive:   0008 <last 6 bytes of data>
	
	where:
	
	  9000 = LL field: continuation bit + 4KB of data to follow
	  12FF = LU6.2 application data GDS variable
	
	NOTE: It is up to the APPC sender to format the GDS variables and length values.
	The SNA Server APPC interface sends GDS data in 4KB chunks, though other
	implementations may use the max size of 32767.
	
	For more information about LL and GDS variables, see Chapter 12 of the "IBM SNA
	Formats Guide" (GDS ID Description and Assignments), IBM document number
	GA27-3136.
	
	Additional query words: prodsna
	
	======================================================================
	Keywords          : kb3rdparty kbnetwork kbprogramming 
	Technology        : kbAudDeveloper kbSNAServSearch kbSNAServ200 kbSNAServ211 kbSNAServ210
	Version           : WINDOWS:2.0,2.1,2.11
	
	=============================================================================
	

{% endraw %}
