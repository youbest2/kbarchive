---
layout: page
title: "Q148230: FIX: TypeLibs with Large Argument Lists May Crash ClassWizard"
permalink: /kb/148/Q148230/
---

## Q148230: FIX: TypeLibs with Large Argument Lists May Crash ClassWizard

{% raw %}

	Article: Q148230
	Product(s): Microsoft C Compiler
	Version(s): winnt:
	Operating System(s): 
	Keyword(s): kbole kbwizard kbMFC kbVC400bug kbVC410fix kbClassWizard kbGrpDSTools kbNoUpdate
	Last Modified: 06-MAY-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- The ClassWizard, used with:
	   - Microsoft Visual C++ 32-bit Edition, version 4.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	The Developer Studio crashes or abruptly terminates when attempting to add a new
	class from an OLE TypeLib with the ClassWizard.
	
	CAUSE
	=====
	
	ClassWizard allocates a 1024 byte buffer to store member function prototypes
	based on the information it finds in the specified OLE TypeLib. If the
	ClassWizard-generated prototype for a member function exceeds this limit,
	Developer Studio will crash or abruptly terminate.
	
	This problem only occurs when attempting to create a new class from an OLE
	TypeLib, where one or more of the automation methods contains a large argument
	list. For example, both Microsoft Schedule+ 7.0 and Microsoft Project 4.0 expose
	automation methods with large argument lists. Attempting to create a new class
	from either the Schedule+ type library (SP7EN32.OLB) or the Microsoft Project
	type library (PJ4EN32.OLB) may cause Developer Studio to crash.
	
	When the crash occurs, you will notice that a header (.H) file and an
	implementation (.CPP) file were added to your project's directory. These files
	will most likely be corrupted and should be deleted from your project directory.
	
	RESOLUTION
	==========
	
	Avoid using the ClassWizard to generate new classes with the previously listed
	type libraries. Microsoft has provided a self-extracting file, called
	TLBWRAP.EXE, that contains the COleDispatchDriver-derived classes that wrap the
	automation objects exposed by the SP7EN32.OLB and PJ4EN32.OLB type libraries.
	
	The following file is available for download from the Microsoft Software
	Library:
	
	  Tlbwrap.exe
	  (http://support.microsoft.com/download/support/mslfiles/Tlbwrap.exe)
	
	For more information about downloading files from the Microsoft Software Library,
	please see the following article in the Microsoft Knowledge Base:
	
	  Q119591 How to Obtain Microsoft Support Files from Online Services
	
	
	STATUS
	======
	
	Microsoft has confirmed this to be a bug in the Microsoft products listed at the
	beginning of this article. This bug was corrected in Visual C++ 4.1.
	
	Additional query words: kbVC400bug 4.00 4.10 softlib software library
	
	======================================================================
	Keywords          : kbole kbwizard kbMFC kbVC400bug kbVC410fix kbClassWizard kbGrpDSTools kbNoUpdate 
	Technology        : kbVCsearch kbAudDeveloper kbClassWizard
	Version           : winnt:
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
