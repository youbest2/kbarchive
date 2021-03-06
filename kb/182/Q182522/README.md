---
layout: page
title: "Q182522: XADM: Administrator Program Corrupts the IMC Routing Table"
permalink: /kb/182/Q182522/
---

## Q182522: XADM: Administrator Program Corrupts the IMC Routing Table

{% raw %}

	Article: Q182522
	Product(s): Microsoft Exchange
	Version(s): winnt:5.0,5.5
	Operating System(s): 
	Keyword(s): 
	Last Modified: 04-APR-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Server, versions 5.0, 5.5 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When you use the Exchange Administrator program to modify the Internet Mail
	Service (IMC) settings, the Administrator program may corrupt the Internet Mail
	Service (IMC) Routing table. When this happens, the Microsoft Exchange Internet
	Mail Service fails to start. The following event is logged in the event viewer:
	
	  Event ID: 4056
	  Source MSExchangeIMC
	  Type: Error
	  Category: Initialization/termination.
	  Description: Unable to parse the delivery route anlsf.msbp.co. Since
	  errors in delivery routing parameters  can result in misrouted mail, the
	  Internet Mail Service will not start until this error is corrected.
	
	This problem can occur when a change is made to the routing table in the Internet
	Mail Service configuration. The routing table referred to here is configured
	through the E-Mail Domain button on the Connections tab of the Internet Mail
	Service (IMC) properties page. After a change is made, the Internet Mail Service
	no longer starts.
	
	Further attempts to modify this routing table may cause the Exchange
	Administrator program to stop responding (crash). When the Exchange
	Administrator program stops responding, the following information may be found
	in the Dr. Watson log (Drwtsn32.log):
	
	  State Dump for Thread Id 0x1b0
	
	  eax=00003b00 ebx=0000003b ecx=01000000 edx=00000001 esi=00a65f90
	  edi=78005ca4
	  eip=78005d01 esp=0012a618 ebp=00a65a60 iopl=0         nv up ei pl nz na
	  pe nc
	  cs=001b  ss=0023  ds=0023  es=0023  fs=003b  gs=0000
	  efl=00000202
	
	  function: strchr
	       78005ceb 7537             jnz     strchr+0x80 (78005d24)
	       78005ced 2500010181       and     eax,0x81010100
	       78005cf2 74d3             jz      strchr+0x23 (78005cc7)
	       78005cf4 2500010101       and     eax,0x1010100
	       78005cf9 741f             jz      strchr+0x76 (78005d1a)
	       78005cfb 5e               pop     esi
	       78005cfc 5f               pop     edi
	       78005cfd 5b               pop     ebx
	       78005cfe 33c0             xor     eax,eax
	       78005d00 c3               ret
	  FAULT ->78005d01 8a0a             mov     cl,[edx]
	  ds:00000001=??
	       78005d03 42               inc     edx
	       78005d04 38d9             cmp     cl,bl
	       78005d06 0f847c1f0100     je      mbsnbicoll+0x3b (78017c88)
	       78005d0c 84c9             test    cl,cl
	       78005d0e 74ed             jz      strchr+0x59 (78005cfd)
	       78005d10 f7c203000000     test    edx,0x3
	       78005d16 74a4             jz      strchr+0x18 (78005cbc)
	       78005d18 ebe7             jmp     strchr+0x5d (78005d01)
	       78005d1a 81e600000080     and     esi,0x80000000
	       78005d20 75a5             jnz     strchr+0x23 (78005cc7)
	       78005d22 ebd7             jmp     strchr+0x57 (78005cfb)
	
	  *----> Stack Back Trace <----*
	
	  FramePtr ReturnAd Param#1  Param#2  Param#3  Param#4  Function Name
	  00a65a60 736d2e66 632e7062 613b006f 66736c6e 62736d2e msvcrt!strchr
	
	  *----> Raw Stack Dump <----*
	  0012a618  f0 5a a6 00 29 d1 8e 01 - 01 00 00 00 3b 00 00 00
	  .Z..).......;...
	  0012a628  2c ab 71 00 10 01 00 00 - c4 a9 12 00 78 aa 71 00
	  ,.q.........x.q.
	  0012a638  b8 ad 12 00 84 af 12 00 - 04 af 12 00 44 af 12 00
	  ............D...
	  0012a648  0f 00 00 00 00 00 00 00 - 97 00 00 00 78 a6 12 00
	  ............x...
	  0012a658  3c 19 c3 77 01 00 00 00 - 50 02 0a 2c 4d 00 53 00
	  <..w....P..,M.S.
	  0012a668  00 00 00 00 00 00 00 00 - 2e 01 00 00 f0 00 00 00
	  ................
	  0012a678  44 00 65 00 6c 00 69 00 - 76 00 65 00 72 00 20 00
	  D.e.l.i.v.e.r. .
	  0012a688  55 00 73 00 69 00 6e 00 - 67 00 00 00 00 00 00 00
	  U.s.i.n.g.......
	  0012a698  00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00
	  ................
	  0012a6a8  00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00
	  ................
	  0012a6b8  00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00
	  ................
	  0012a6c8  00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00
	  ................
	  0012a6d8  00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00
	  ................
	  0012a6e8  00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00
	  ................
	  0012a6f8  00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00
	  ................
	  0012a708  00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00
	  ................
	  0012a718  00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00
	  ................
	  0012a728  00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00
	  ................
	  0012a738  00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00
	  ................
	  0012a748  00 00 00 00 00 00 00 00 - 00 00 00 00 00 00 00 00
	  ................
	
	CAUSE
	=====
	
	The Imcadmin.dll file corrupts the heap when there are too many entries in the
	table.
	
	RESOLUTION
	==========
	
	The new Imcadmin.dll file only prevents the problem from reoccurring. You still
	need to perform the following steps to resolve the situation that is currently
	occurring:
	
	1. Run IMCCOPY (from the Exchange 5.5 Server CD \server\support\utils\i386) to
	  copy out the information. Command line:
	
	  IMCCOPY -save routes c:\exchsrvr\imcdata\save.txt
	
	2. Open Save.txt.
	
	3. Look for the [Routes] section. It should look similar to the following:
	
	        [Routes]
	        DeliveryRouting=+
	        +DOMAIN.COM;xxx.xxx.xxx.xxx;0
	        DefaultRouting=
	    
	
	  Note: xxx.xxx.xxx.xxx is an actual IP address for that domain
	
	4. Delete everything after DeliveryRouting= and before DefaultRouting=. The
	  updated list should look like:
	
	        [Routes]
	        DeliveryRouting=
	        DefaultRouting=
	   
	
	5. Save the updated file to save_fix.txt.
	
	6. Run IMCCOPY again to restore. Command line:
	
	  IMCCOPY -restore routes c:\exchsrvr\imcdata\save_fix.txt
	
	7. Start the Internet Mail Service and verify that it starts.
	
	8. Run ADMIN to verify routes are gone.
	
	9. Next, either re-enter the routes manually via ADMIN or "restore" the routes
	  using IMCCOPY. Edit the save_fix.txt file and add the routes using the
	  [Routes] above as a guide. Then use the following command line:
	
	  IMCCOPY -restore routes c:\exchsrvr\imcdata\save.txt
	
	10. Restart the Internet Mail Service.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in Exchange Server version 5.0.
	
	
	A supported fix is now available, but has not been fully regression-tested and
	should be applied only to systems experiencing this specific problem. Unless you
	are severely impacted by this specific problem, Microsoft recommends that you
	wait for the next Service Pack that contains this fix. Contact Microsoft
	Technical Support for more information.
	
	
	Microsoft has confirmed this to be a problem in Exchange Server version 5.5. This
	problem has been corrected in the latest U.S. Service Pack for Microsoft
	Exchange Server version 5.5. For information about obtaining the Service Pack,
	query on the following word in the Microsoft Knowledge Base (without the
	spaces):
	
	  S E R V P A C K
	
	Additional query words: route drwatson watson
	======================================================================
	Keywords          :  
	Technology        : kbExchangeSearch kbExchange500 kbExchange550 kbZNotKeyword2
	Version           : winnt:5.0,5.5
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
