---
layout: page
title: "Q178492: SNA 3.0 TN3270 or TN5250 Server Traps When Configuration Saved"
permalink: /kb/178/Q178492/
---

## Q178492: SNA 3.0 TN3270 or TN5250 Server Traps When Configuration Saved

{% raw %}

	Article: Q178492
	Product(s): Microsoft SNA Server
	Version(s): WINDOWS:3.0,3.0 SP1,3.0 SP2
	Operating System(s): 
	Keyword(s): 
	Last Modified: 13-JUN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft SNA Server, versions 3.0, 3.0 SP1, 3.0 SP2 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	The TN3270 or TN5250 service may end unexpectedly with an access violation when
	saving the configuration file, even if the configuration file changes do not
	affect these services. This problem can occur if the SNA Server Manage Agent
	service (Mngagent.exe) is restarted on the SNA Server. The following symptoms
	will occur when this problem happens:
	
	- All TN3270 or TN5250 client users will lose their sessions and the TN3270 or
	  TN5250 Server service will no longer be running.
	
	- The following event will be logged in the Windows NT application event log:
	
	  
	
	  Event ID: 624 
	  Source:   TN3270 Server (or TN5250 Server)
	  Description: Creating dump file <snaroot>\traces\snadump.log for 
	               <tn3servr.exe | tn5250.exe >
	
	- A new entry will be created in the <ntroot>\drwtsn32.log file (the
	  failing routine in mngbase.dll is the same for both TN3270 or TN5250):
	
	  
	
	  Application exception occurred:
	       App: exe\tn3servr.dbg (<process id>)
	       Exception number: c0000005 (access violation)
	
	  [...]
	
	  State Dump for Thread Id <thread id>
	
	  eax=0c9dfda4 ebx=77e7a69f ecx=0b5f0000 edx=42008000 esi=00000003 
	  edi=00000003 eip=6098d4c8 esp=0c9dfd98 ebp=77e719c8 iopl=0         
	  nv up ei pl nz na po nc
	  cs=001b  ss=0023  ds=0023  es=0023  fs=0038  gs=0000 efl=00000206
	
	  function: MngGetRectypeChangeMask
	       6098d4a6 6a00             push    0x0
	       6098d4a8 682c1400c0       push    0xc000142c
	       6098d4ad 6a01             push    0x1
	       6098d4af e8fc010000       call    MngReportToEventLog (6098d6b0)
	       6098d4b4 33c0             xor     eax,eax
	       6098d4b6 33d2             xor     edx,edx
	       6098d4b8 5e               pop     esi
	       6098d4b9 81c4a0000000     add     esp,0xa0
	       6098d4bf c20400           ret     0x4
	       6098d4c2 81e6ffff0000     and     esi,0xffff
	  FAULT ->6098d4c8 8b84f1a0010000   mov     eax,[ecx+esi*8+0x1a0]  
	
	  *----> Stack Back Trace <----*
	
	  Function Name
	
	  mngbase!MngGetRectypeChangeMask  
	  mngbase!MngIsRectypeChanged
	  mngext!Mng_IsRectypeChanged 
	  tn3servr!Tn3ManageActionEx
	  tn3servr!Tn3ManageActionEx
	  tn3servr!Tn3ManageActionEx
	  mngext!CMngExtSink::OnCommand 
	  mngbase!CNotifyQueue::Dispatch 
	  mngbase!CNotifyQueue::ProcessWait  
	  mngext!Mng_IsRectypeChanged 
	  kernel32!BaseThreadStart 
	  tn3   servr!<nosymbols>
	
	CAUSE
	=====
	
	When the configuration file changes, the TN3270 and TN5250 services are both
	notified and attempt to handle dynamic changes to their configuration data.
	However, if the mngagent service had been stopped and restarted, the
	configuration data location within the Manage shared memory may change, causing
	the services to access an invalid memory location causing an access violation.
	
	WORKAROUND
	==========
	
	Do not stop and restart the SNA Server Manage Agent service (Mngagent.exe).
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in SNA Server 3.0 (including SP1
	and SP2).
	
	This problem was corrected in the latest SNA Server version 3.0 U.S. Service
	Pack. For information on obtaining this Service Pack, query on the following
	word in the Microsoft Knowledge Base (without the spaces):
	
	  S E R V P A C K
	
	Additional query words:
	
	======================================================================
	Keywords          :  
	Technology        : kbAudDeveloper kbSNAServSearch kbSNAServ300 kbSNAServ300SP1 kbSNAServ300SP2
	Version           : WINDOWS:3.0,3.0 SP1,3.0 SP2
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
