---
layout: page
title: "Q122177: Systems Management Server Event Log Codes 0 Through 99"
permalink: /kb/122/Q122177/
---

## Q122177: Systems Management Server Event Log Codes 0 Through 99

{% raw %}

	Article: Q122177
	Product(s): Microsoft Systems Management Server
	Version(s): 1.0,1.1,1.2
	Operating System(s): 
	Keyword(s): kbDatabase kbInventory kbScheduler smsinv smsdatabase smsscheduler
	Last Modified: 05-FEB-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Systems Management Server versions 1.0, 1.1, 1.2 
	-------------------------------------------------------------------------------
	
	This article details Systems Management Server event log codes 0 through
	99.
	
	Event Log Codes 0 - 99
	----------------------
	
	Code   Description
	----   -----------
	
	0      Success.
	
	1      The despooler instruction file is corrupt or has a wrong version
	      stamp.
	
	2      X is missing.
	
	3      The component is unable to open registry key.
	
	4      The component is unable to read registry key.
	
	5      Unable to connect to domain.
	
	6      The job has been cancelled, the package won't be installed on any
	      servers.
	
	7      The component is unable to create share on server with path.
	
	8      The share name for a sharing job cannot be ADMIN$ share or any
	      rootdrive$ share. Hidden shares are supported, they just can't be
	      any existing system hidden shares. Please use a share name other
	      than X and resend the package.
	
	9      Unable to remove file.
	
	10     The component is unable to delete directory tree.
	
	11     Unable to find the package file. The scheduler at the sending site
	      expects the package file to be at this site, however the package is
	      either being removed via a remove package job or deleted by some
	      user. Have the administrator resend the package to correct this
	      problem.
	
	12     Unable to connect to the instruction source.
	
	13     No server is specified in the registry or in the instruction.
	
	14     X encountered a fatal error, and is unable to retry the instruction.
	
	15     Unable to decompress file X to Y, because it's corrupted.
	
	16     The component is unable to do a tree copy of files from X to Y.
	
	17     Install request: Could not obtain a SQL connection.
	
	18     Install request: Unable to obtain destination addresses.
	
	19     Install request: Unable to open outbox (X).
	
	20     Install request: Unable to insert send request into datdabase.
	
	21     Install request: Send request has permanently failed. Total
	      retries = X.
	
	22     Install Request: Unable to locate send request (X) in database.
	
	23     Install Request: Unable to reactivate request. Send request
	      access mode violation.
	
	24     Install Request: Unable to reactivate request. Cannot change status
	      to 'Pending'.
	
	25     Install Request: Unable to obtain transmit status while updating
	      request status.
	
	26     Install Request: Unable to obtain status values from job details
	      table.
	
	27     Install Request: SQL query failed on table (X).
	
	28     Server Install Job: Could not obtain a SQL connection.
	
	29     Install Request: SQL query failed on table (X).
	
	30     Install Job: Job table failed to update correctly.
	
	31     Install Job: Unable to read Job table.
	
	32     Install Job: Could not generate target machine list.
	
	33     Install Job: Could not generate destination site list.
	
	34     Install Job: Could not generate new request during job activation.
	
	35     Install Job: Could not write to the NT registry.
	
	36     Install Job: No requests found for this job while updating job
	      status.
	
	37     Install Job: Request (X) failed to activate.
	
	38     Install Job: Could not locate Package.
	
	39     Install Job: Request failed to reactivate.
	
	40     Install Job: Could not generate instruction file.
	
	41     Install Job: Job detail record missing.
	
	42     Install Job: Unable to create transfer file.
	
	43     Install Job: Could not locate request (X).
	
	44     Install Job: Could not add Job Detail record.
	
	45     Install Job: Could not locate Package.
	
	46     Install Job: Could not retrieve Package Command Manager information.
	
	47     Job Source: Could not get a SQL connection.
	
	48     Job Source: SQL query failed on table (X).
	
	49     Job Source: Directory was empty.
	
	50     Job Source: Was not able to create a new file.
	
	51     Job Source: Directory snapshot failed.
	
	52     Job Source: Job missing from source.
	
	53     Request Source: Unable to obtain a SQL connection.
	
	54     Request Source: SQL query failed.
	
	55     Machine not specified in instruction.
	
	56     Location not specified in instruction.
	
	57     Machine (X) in instruction cannot be found.
	
	58     Location (X) in instruction cannot be found.
	
	59     Cannot open file (X) for instruction.
	
	60     Cannot read file (X) for instruction.
	
	61     Cannot write file (X) for instruction.
	
	62     Machine not specified in instruction for Package Command Manager.
	
	63     Location not specified in instruction for Package Command Manager.
	
	64     Machine (X) in instruction for Package Command Manager cannot be
	      found.
	
	65     Location (X) in instruction for Package Command Manager cannot be
	      found.
	
	66     Reporting location not specified in instruction from Package
	      Command Manager .
	
	67     Reporting location (X) in instruction from Package Command Manager
	      cannot be found.
	
	68     Machine not specified in instruction from Package Command Manager.
	
	69     Location not specified in instruction from Package Command Manager.
	
	70     Machine (X) in instruction from Package Command Manager cannot be
	      found.
	
	71     Location (X) in instruction from Package Command Manager cannot be
	      found.
	
	72     Destination directory for inventory and status (delta-MIF) files not
	      specified in system job instruction.
	
	73     Destination directory (X) for inventory and status (delta-MIF) files
	      in system job instruction cannot be found.
	
	74     Cannot find package file (X) for system job instruction.
	
	75     Cannot open file (X) for system job instruction.
	
	76     Cannot read file (X) for system job instruction.
	
	77     Cannot execute system job instruction in file (X).
	
	78     Cannot write file (X) for system job instruction. Disk may be full.
	
	79     Site Reporter: Directory for inventory and status files not
	      specified.
	
	80     Site Reporter: Cannot find directory (X) for inventory and status
	      files.
	
	81     Site Reporter: Job source for inventory and status files not
	      specified.
	
	82     Site Reporter: Cannot find job source (X) for inventory and status
	      files.
	
	83     Site Reporter: Destination site not specified in inventory or status
	      file (X).
	
	84     Site Reporter: Cannot insert system job in job source (X).
	
	85     Directory Monitor: Cannot find directory (X).
	
	86     Directory Monitor: Wait function abandoned due to NT error (X).
	
	87     Directory Monitor: Cannot find site code in delta-MIF file (X).
	
	88     Database Processing: (X).
	
	89     The component is unable to create directory X.
	
	90     Unable to decompress the instruction file X into file Y.
	
	91     The instruction source X is either missing or cannot be located.
	
	92     Machine classes: Could not open file <X>.
	
	93     Machine classes: Memory allocation failure.
	
	94     Machine classes: Varfile error - file invalid.
	
	95     Machine classes: Varfile bad seek error, error number <X>.
	
	96     Machine classes: Varfile general error, error number <X>.
	
	97     Machine classes: Varfile unknown error, error number <X>.
	
	98     Machine classes: File append error.
	
	99     Machine classes: File close error.
	
	Additional query words: sms prodsms 1.0 1.1 1.2
	
	======================================================================
	Keywords          : kbDatabase kbInventory kbScheduler smsinv smsdatabase smsscheduler 
	Technology        : kbSMSSearch kbSMS100 kbSMS110 kbSMS120
	Version           : :1.0,1.1,1.2
	
	=============================================================================
	

{% endraw %}
