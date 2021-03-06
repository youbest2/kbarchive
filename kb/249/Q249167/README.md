---
layout: page
title: "Q249167: BUG: SNAOLEDB Does Not Support Pessimistic Locking"
permalink: /kb/249/Q249167/
---

## Q249167: BUG: SNAOLEDB Does Not Support Pessimistic Locking

{% raw %}

	Article: Q249167
	Product(s): Microsoft SNA Server
	Version(s): WINDOWS:4.0 SP2,4.0 SP3
	Operating System(s): 
	Keyword(s): kbOLEDB kbGrpDSVCDB kbGrpDSMDAC kbDSupport
	Last Modified: 19-JUL-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft OLE DB Provider for AS/400 and VSAM, versions 4.0 SP2, 4.0 SP3 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	The Microsoft OLEDB Provider for AS/400 and VSAM (SNAOLEDB) does not support
	pessimistic locking.
	
	In the Microsoft SNA SDK documentation under the "ADO Recordset Object in the OLE
	DB Provider for AS/400 and VSAM" topic, it is mentioned under LockType that
	SNAOLEDB supports all four lock types. Namely adLockReadOnly, adLockOptimistic,
	adLockPessimistic, and adLockBatchOptimistic. The preceding statement is not
	true and SNAOLEDB does not currently support adLockPessimistic from an ADO
	recordset object.
	
	The ADO Client side cursor does not support "pessimistic" locking. ADO server
	side cursor support "pessimistic" locking if the corresponding provider supports
	this property. SNAOLEDB does not support "pessimistic" locking. If an
	unsupported value is set, then no error occurs and the closest supported
	LockType is used instead. If from an ADO program you set the LockType property
	to adLockPessimistic, when you open an updateable recordset with server side
	cursor it automatically maps to either adLockOptimistic or
	adLockBatchOptimistic.
	
	STATUS
	======
	
	Microsoft has confirmed this to be a problem in the Microsoft SNA Server version
	4.0 Service Pack 2 (SP2) and Service Pack 3 (SP3) SDK documentation.
	
	MORE INFORMATION
	================
	
	The OLEDB Provider for AS/400 and VSAM (SNAOLEDB) comes with SNA Server/Client
	version 4.0 SP2 or SP3. It uses the DDM RLIO protocol to provide OLEDB consumers
	with access to VSAM and AS/400 record-level data. This provider complies with
	Level 4 of the IBM Distributed Data Management (DDM) architecture and the OLE DB
	architecture. It uses SNA Server, the reliable platform for host integration as
	the networking bridge between the SNA host and the Windows NT operating
	systems.
	
	The Microsoft OLE DB Provider for AS/400 and VSAM supports the following
	features:
	
	- Set attributes and a record description of a host file (column information).
	
	- Position to the beginning record or the ending record in a file.
	
	- Navigate to the previous or next record in a file.
	
	- Seek to a record based on an index.
	
	- Lock records.
	
	- Change records in a file.
	
	- Insert new records and delete records in a file.
	
	- Preserve file and record attributes.
	
	SNAOLEDB does not support "pessimistic" locking.
	
	REFERENCES
	==========
	
	For more information, please refer to the following article in the Microsoft
	Knowledge Base:
	
	  Q190625 FIX: ADO Client Cursors Report LockType = adLockPessimistic
	
	SNA SDK Documentation
	
	Additional query words:
	
	======================================================================
	Keywords          : kbOLEDB kbGrpDSVCDB kbGrpDSMDAC kbDSupport 
	Technology        : kbAudDeveloper kbOLEDBSearch kbOLEDBProvAS400VSAM400SP2 kbOLEDBProvAS400VSAM400SP3 kbOLEDBProvSearch
	Version           : WINDOWS:4.0 SP2,4.0 SP3
	Issue type        : kbbug
	Solution Type     : kbpending
	
	=============================================================================
	

{% endraw %}
