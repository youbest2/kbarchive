---
layout: page
title: "Q313677: BUG: Servers Are Removed from List When There Is a Blank String"
permalink: /kb/313/Q313677/
---

## Q313677: BUG: Servers Are Removed from List When There Is a Blank String

{% raw %}

	Article: Q313677
	Product(s): Microsoft SNA Server
	Version(s): 4.0,4.0 SP1,4.0 SP2,4.0 SP3,4.0 SP4
	Operating System(s): 
	Keyword(s): sna4 kbsna400sp1 kbsna400sp2 kbsna400sp3 kbSNA400sp4fix Kbhostintegserv2000
	Last Modified: 22-JAN-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft SNA Server, versions 4.0, 4.0 SP1, 4.0 SP2, 4.0 SP3, 4.0 SP4 
	- Microsoft Host Integration Server 2000 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	If a blank string (one or more spaces) is displayed in the "Locate servers by
	Server Name" box in the SNA Server client or Host Integration Server (HIS) 2000
	End-User client for Microsoft Windows 95 or Microsoft Windows 98, the next time
	that you view the client configuration, no servers are listed. When you access a
	host session, you may receive a message indicating that no SNA Servers or Host
	Integration Servers can be found in the subdomain.
	
	NOTE: This issue is not seen with SNA Server for Microsoft Windows NT or the HIS
	2000 Admin client.
	
	In some cases, when the SNABase service is stopped and restarted, a Drwtsn32.log
	file is generated if Drwtsn32.exe is configured as the default debugger. When
	this occurs, the Drwtsn32.log file will look similar to the following:
	
	  Application exception occurred:
	          App: exe\snabase.dbg (pid=209)
	          When: 7/25/2000 @ 14:12:10.423
	          Exception number: c0000005 (access violation)
	  .
	  .[Data omitted]
	  .
	  State Dump for Thread Id 0xce
	
	  eax=00000001 ebx=00000000 ecx=00000001 edx=00baf12c esi=00000001    edi=00000000
	  eip=77f93e0c esp=00bae944 ebp=00baeda8 iopl=0         nv up ei pl nz na    po nc
	  cs=001b  ss=0023  ds=0023  es=0023  fs=003b  gs=0000                efl=00000206
	
	  function: wcstombs
	          77f93de8 f645f820         test    byte ptr [ebp-0x8],0x20         ss:01aad7ae=??
	          77f93dec 0f8451030000     je      wcstombs+0x15e4 (77f94143)
	          77f93df2 3bc3             cmp     eax,ebx
	          77f93df4 7508             jnz     wcstombs+0x129f (77f93dfe)
	          77f93df6 a14c70fa77   mov eax,[fltused+0x35c (77fa704c)]    ds:77fa704c=77f9daa0
	          77f93dfb 8945f0           mov     [ebp-0x10],eax            ss:01aad7ae=????????
	          77f93dfe 8b4df0           mov     ecx,[ebp-0x10]            ss:01aad7ae=????????
	          77f93e01 33ff             xor     edi,edi
	          77f93e03 395df4           cmp     [ebp-0xc],ebx             ss:01aad7ae=????????
	          77f93e06 0f8e6c030000     jle     wcstombs+0x1619 (77f94178)
	  FAULT ->77f93e0c 8a01             mov     al,[ecx]                        ds:00000001=??
	          77f93e0e 84c0             test    al,al
	          77f93e10 0f8462030000     je      wcstombs+0x1619 (77f94178)
	          77f93e16 8b15186efa77 mov edx,[fltused+0x128 (77fa6e18)]    ds:77fa6e18=77fa6e22
	          77f93e1c 0fb6c0           movzx   eax,al
	          77f93e1f f644420180       test   byte ptr [edx+eax*2+0x1],0x80    ds:00efea08=??
	          77f93e24 7401             jz      wcstombs+0x12c8 (77f93e27)
	          77f93e26 41               inc     ecx
	          77f93e27 41               inc     ecx
	          77f93e28 47               inc     edi
	          77f93e29 3b7df4           cmp     edi,[ebp-0xc]             ss:01aad7ae=????????
	          77f93e2c 7cde             jl      wcstombs+0x12ad (77f93e0c)
	
	WORKAROUND
	==========
	
	To work around this issue, remove any spaces in the client configuration.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in SNA Server 4.0.
	
	
	Microsoft has confirmed this to be a problem in Host Integration Server 2000.
	
	
	Additional query words:
	
	======================================================================
	Keywords          : sna4 kbsna400sp1 kbsna400sp2 kbsna400sp3 kbSNA400sp4fix Kbhostintegserv2000 
	Technology        : kbAudDeveloper kbSNAServSearch kbHostIntegServ2000 kbSNAServ400 kbSNAServ400SP1 kbSNAServ400SP2 kbSNAServ400SP3 kbSNAServ400SP4
	Version           : :4.0,4.0 SP1,4.0 SP2,4.0 SP3,4.0 SP4
	Issue type        : kbbug
	Solution Type     : kbnofix
	
	=============================================================================
	

{% endraw %}
