---
layout: page
title: "Q85647: PC Adm: Err Msg: Notice 56: Error Deleting User Address"
permalink: /kb/085/Q85647/
---

## Q85647: PC Adm: Err Msg: Notice 56: Error Deleting User Address

{% raw %}

	Article: Q85647
	Product(s): Microsoft Mail For PC Networks
	Version(s): 
	Operating System(s): 
	Keyword(s): 
	Last Modified: 11-JUL-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Mail for PC Networks, versions 2.1, 3.0, 3.2 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When a Mail administrator tries to delete a user from the Postoffice Address
	List (POL) using the Mail Administrator (ADMIN.EXE) program provided with
	Microsoft Mail for PC Networks, the following error message may appear:
	
	  Notice 56
	  Error deleting user address in Postoffice Address list.
	
	CAUSE
	=====
	
	This problem occurs if the POL has a missing or corrupted record for the user
	(for example, if the UserID is missing from the POL). The cause of the problem
	can be one of the following:
	
	1. The user is a local user, and the record is missing from the ADMIN.NME file;
	  however, the access (ACCESS*.GLB) files contain information about this user.
	
	2. The user record is present in the POL but is corrupted.
	
	3. The user is an external postoffice user added to the POL. The user record is
	  present in the POL; however, the record is corrupted.
	
	RESOLUTION
	==========
	
	The POL information is contained in the ADMINSHD.NME and ADMIN.NME files. These
	two files should always have the same exact size, date, and relative time.
	
	The following are corresponding workarounds for the above causes. These steps are
	geared for the Mail administrator:
	
	1. If the user is a local user and the record is missing from the ADMIN.NME
	  file, copy the POL to your Personal Address List (PAL), add the user there,
	  and then copy your PAL to the POL.
	
	  The following procedure assumes that the administrator mailbox still exists
	  and the 8-digit hexadecimal ID (hexid) is 00000000. If you are using an
	  account other than 00000000, substitute the 8-digit hexid for that account
	  for 00000000.
	
	  a. Obtain the user's mailbox name. From the Administrator program Config
	     menu, choose Password. Note the postoffice and network names.
	
	  b. At the MS-DOS command prompt, change to the NME subdirectory of the Mail
	     database.
	
	  c. Make a backup of the POL by typing the following command:
	
	  " copy admin.nme admin.old " (without the quotation marks)
	
	  d. Make a backup of your PAL by typing:
	
	  " copy 00000000.nme 00000000.old " (without the quotation marks)
	
	     If 00000000.NME is a 0-byte file, copying may not work. You can safely skip
	     this step.
	
	  e. Copy the POL to the PAL by typing:
	
	  " copy admin.nme 00000000.nme " (without the quotation marks)
	
	  f. Move up one directory level from the NME subdirectory (by typing CD..).
	
	  g. Start the MS-DOS Mail client and sign in using the admin mailbox by
	     typing:
	
	  " mail admin -p<password> " (without the quotation marks)
	
	  h. From the Address menu, choose Enter. At the prompts, type in the mailbox,
	     postoffice, and network names you noted in step a above. (If you have
	     other address types, choose the Microsoft Mail type and the Admin program
	     will then prompt you for the above.) Type in the data noted from Step 1.
	     It will bring up the alias. Press the ENTER key.
	
	  i. Quit out of the Mail client.
	
	  j. At the MS-DOS command prompt, change to the NME directory of the Mail
	     database.
	
	  k. Copy the PAL to the POL by typing:
	
	  " copy 00000000.nme admin.nme
	  copy 00000000.nme adminshd.nme " (without the quotation marks)
	
	  l. Move up one directory level from the NME subdirectory (by typing CD..).
	
	  m. Start the Administrator program. You should now be able to delete the
	     problem user account.
	
	  Once you have successfully deleted the user account, delete the ADMIN.OLD file
	  and copy 00000000.OLD to 00000000.NME. (If you skipped step d above, you do
	  not need to copy 00000000.OLD to 00000000.NME.)
	
	2. If the user record is present in the POL but is corrupted, perform the
	  following steps:
	
	  a. Send to Microsoft Product Support Services (PSS) the access (ACCESS.*)
	     files and the ADMIN.NME file.
	
	     A Support Professional will verify information in the access file, correct
	     the record in the ADMIN.NME file, and return your ADMIN.NME file to you.
	
	
	  b. Copy the corrected ADMIN.NME over ADMINSHD.NME. You should be able to
	     delete the user.
	
	     Note: Do not make any modifications to the POL between the time you send
	     the ADMIN.NME and the time you receive the corrected ADMIN.NME from PSS.
	
	3. If the user is an external postoffice user added to the POL and the user
	  record is present in the POL but is corrupted, send to PSS the ADMIN.NME file
	  and the xxxxxxxx.USR file for the external postoffice the user is on.
	
	  To find out the xxxxxxxx number, perform the following steps:
	
	  a. Type out the NETWORK.GLB file. Find the 8-digit number of the network the
	     user is on.
	
	  b. Type out that 8-digit.XTN file. This file should show the 8-digit numbers
	     for the external postoffices. Find the 8-digit number of the postoffice
	     the user is on. That number is the USR file needed by PSS.
	
	     With the ADMIN.NME and xxxxxxxx.USR files, the PSS engineer will verify the
	     information in the USR file, correct the record in the ADMIN.NME file, and
	     return your ADMIN.NME file to you.
	
	
	  c. Copy ADMIN.NME to ADMINSHD.NME. You should be able to delete the user.
	
	     Note: Do not make any modifications to the POL between the time you send
	     the ADMIN.NME and the time you receive the corrected ADMIN.NME from PSS.
	
	MORE INFORMATION
	================
	
	If the steps above do not work, try one of the following:
	
	1. Double-check the spelling of all problem names, along with the network and
	  postoffice names. Often the type number is corrupted to 00, and the name will
	  be blank or will contain garbage characters.
	
	2. Obtain and use the ACCTONME utility that is available as part of the Database
	  Maintenance Utilities document. To obtain the document containing the
	  Database Maintenance Utilities, please see the following article in the
	  Microsoft Knowledge Base:
	
	  Q99419 PC DB: Database Maintenance Utilities (Complete)
	
	  There are some side effects to using this utility that are explained in the
	  ACCTONME.TXT file included with the utility.
	
	Additional query words: 2.10 3.00 3.20 Admin PO err msg errmsg alert
	
	======================================================================
	Keywords          :  
	Technology        : kbMailSearch kbZNotKeyword3 kbMailPCN320 kbMailPCN300 kbMailPCN210
	
	=============================================================================
	

{% endraw %}
