---
layout: page
title: "Q216120: HOWTO: Create and Install a One-Off Address Template"
permalink: /kb/216/Q216120/
---

## Q216120: HOWTO: Create and Install a One-Off Address Template

{% raw %}

	Article: Q216120
	Product(s): Microsoft Exchange
	Version(s): winnt:5.5
	Operating System(s): 
	Keyword(s): kbEDK kbExchange550 kbMsg kbEDK550 kbGrpDSMsg kbDSupport
	Last Modified: 09-JUL-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Exchange Server, version 5.5 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	This article demonstrates how to create a one-off address template and then
	install it to Exchange Server.
	
	MORE INFORMATION
	================
	
	Our example address template has the following format:
	
	  
	
	  SDK - TestTmpl
	
	  DisplayName:
	  AliasName:
	  DomainName:
	
	This template generates addresses of type "SDK" with the form
	"AliasName@DomainName".
	
	The process consists of three basic parts:
	
	- Create an address entry template (.blt file).
	
	- Create an address syntax template (.oel file).
	
	- Install the address template into the Exchange administration program (by
	  using the Tmplinst.exe program).
	
	Create an Address Entry Template
	--------------------------------
	
	To create an address entry template, perform the following steps:
	
	1. Create a file named Test.txt that describes the template. This file has the
	  following format:
	
	  
	
	  x-coordinate, width, y-coordinate, height, control type, control flags, MAPI property tag, size, string
	
	In our example template, Test.txt contains the following:
	
	  
	
	  0, 0, 0, 0, DTCT_PAGE, 0x00000000, 0x00000000, 0,Our New Address
	  12, 50, 20, 8, DTCT_LABEL, 0x00000000, 0x00000000, 0,Display Name:
	  75, 141, 18, 12, DTCT_EDIT, 0x00000006, 0x3001001E, 256,*
	  12, 51, 43, 8, DTCT_LABEL, 0x00000000, 0x00000000, 0,Alias Name:
	  75, 141, 41, 12, DTCT_EDIT, 0x00000006, 0x6800001E, 32,*
	  12, 51, 56, 8, DTCT_LABEL, 0x00000000, 0x00000000, 0,Domain Name:
	  75, 141, 54, 12, DTCT_EDIT, 0x00000006, 0x6801001E, 256,*
	
	Valid entries for control type include:
	
	  
	
	  DTCT_BUTTON      Creates a command button.
	  DTCT_CHECKBOX    Creates a check box.
	  DTCT_DDLBX       Creates a drop-down list box.
	  DTCT_EDIT        Creates an edit field for user input. (See control flags below.)
	  DTCT_GROUPBOX    Creates a group box.
	  DTCT_LABEL       Creates a text label.
	  DTCT_LBX         Creates a list box.
	  DTCT_PAGE        Introduces a new page in the property sheet.
	
	Control flags are used in conjunction with DTCT_EDIT control type entries. Valid
	control flag entries can be a combination of the following values:
	
	  
	
	  0x00000001   Creates a multiline edit control.
	  0x00000002   Allows the edit control to be edited.
	  0x00000004   Requires edit from the user upon OK.
	  0x00000010   Displays an asterisk (*) as user types in the edit control, such as for a password.
	
	To combine these flags, use the bitwise OR operator and enter the result in this
	field.
	
	Controls are mapped to MAPI property tags. The address generation code uses the
	property tag value to access field information that is entered by the user.
	Valid entries are:
	
	  
	
	  0x3001001E - PR_DISPLAY_NAME (display name of custom recipient).
	  0x6800001E - 0xFFFE001E - Custom string properties.
	
	Note that the low-order bits for the custom string property are always 001E,
	which indicates that the property is a string.
	
	The size entry is used only with DTCT_EDIT entries and specifies the maximum
	length of input.
	
	The string entry is the label text for the control. This can be text or an
	asterisk.
	
	NOTE: If you place a space between the last comma separator and this entry, the
	edit control is created as read-only.
	
	2. Save Test.txt as a new file, in Unicode format, with a .wtx extension. In
	  Notepad, from the File menu, click Save As, select Unicode from the Encoding
	  drop-down list box, and then enter "Test.wtx" for File name.
	
	3. Use the Template.exe program to convert the .wtx file to a .blt binary file.
	  You can obtain Template.exe at the following FTP site:
	
	  ftp://ftp.microsoft.com/softlib/mslfiles/templupd.exe
	  (ftp://ftp.microsoft.com/softlib/mslfiles/templupd.exe).
	
	  For our example, type the following command:
	
	  " c:>template test.wtx test.blt " (without the quotation marks)
	
	Create an Address Syntax Template
	---------------------------------
	
	An address syntax program works together with address entry templates to convert
	data that is entered in an address entry template dialog box into a proxy
	address string. When the user clicks OK to accept in an address template dialog
	box, the Exchange Server address book reads the data from the dialog box and
	uses it to create the custom address in the correct syntax.
	
	You need to provide an address syntax program that the address book can use to
	translate the entered data into a complete address. Written in a special address
	syntax language, this program is byte-compiled into a binary data file that is
	used by the Exchange Server address book. Because this program is not compiled
	into platform-specific executable code, it is portable across all platforms that
	are supported by Exchange Server.
	
	You start by writing symbolic code. For our example, the symbolic code looks like
	the following:
	
	  EQU	PR_Alias	0x6800001E
	  EQU	PR_Domain	0x6801001e
	  JNX	PR_Alias	Error1
	  JNX	PR_Domain	Error1
	  EMIT	PR_Alias
	  EMIT	At
	  EMIT	PR_Domain
	  HALT
	  Error1:	ERROR
	  At:	"@"
	
	Here is a line-by-line description of the above code:
	
	1. Assign 0x6800001E to the symbolic name PR_Alias. This value is the input
	  value for AliasName from the Test.txt file.
	2. Assign 0x6801001e to the symbolic name PR_Domain. (These first two lines are
	  provided soley for the readability of this example.)
	3. Look at the contents of PR_Alias. If nothing was entered on the template,
	  jump to Error:.
	4. Look at the contents of PR_Domain. If nothing was entered on the template,
	  jump to Error:.
	5. Append the contents of PR_Alias to the email address.
	6. Append the Character stored at AT: to the email Address.
	7. Append the contents of PR_Domain to the email Address.
	8. Stop execution.
	
	You then translate the symbolic code into an .oel binary file. For our example,
	the commands we are using have program codes. Here is a table of the commands
	that we use in this program:
	
	  
	
	  Command     Program Code
	  JNX         0x00000004
	  EMIT        0x6800001E
	  HALT        0x00000000
	  ERROR       0x00000001
	
	For a complete list of commands, see the following Web site:
	
	  http://msdn.microsoft.com/library/psdk/exchserv/adrssing_9p2d.htm
	  (http://msdn.microsoft.com/library/psdk/exchserv/adrssing_9p2d.htm)
	
	Our example looks like the following:
	
	  
	
	  Address   Program Code     Comment
	
	  0000      0x00000004       JNX
	  0004      0x6800001E       Property tag for PR_Alias from Test.txt
	  0008      0x00000034       Program address of Error1
	  000C      0x00000004       JNX
	  0010      0x6801001E       Property tag for PR_Domain from Test.txt
	  0014      0x00000034       Program address of Error1
	  0018      0x00000002       EMIT edit control data
	  001C      0x6800001E       Property tag for PR_Alias
	  0020      0x80000002       EMIT data from program
	  0024      0x00000038       Address of data string "/"
	  0028      0x00000002       EMIT edit control data
	  002C      0x6801001E       Property tag for PR_Domain
	  0030      0x00000000       HALT
	  0034      0x00000001       ERROR
	  0038      0x00000040       ASCII of "@", null terminated
	
	Once you have this, you need to save only the program codes to a binary file. In
	Microsoft Visual C++ version 6.0, on the File menu, click New. On the File tab,
	select Binary, click OK, and then enter the program codes in the data window.
	The program codes should look like the following:
	
	  
	
	   
	  04 00 00 00 1E 00 00 68  34 00 00 00 04 00 00 00
	  1E 00 01 68 34 00 00 00  02 00 00 00 1E 00 00 68
	  02 00 00 80 38 00 00 00  02 00 00 00 1E 00 01 68
	  00 00 00 00 01 00 00 00  40 00 00 00 
	
	Save this file as Test.oel.
	
	Install the Address Template
	----------------------------
	
	To install the one-off address template into the Exchange administration program,
	use the Tmplinst.exe utility. Once installed, the template is available to the
	clients of the Exchange Server, as well as to the administrator.
	
	In our example, the following definitions are required:
	
	  
	
	  Exchange Organization is "Organization"
	  Exchange Site is "Site"
	  Exchange server is "Server"
	
	The command line would be:
	
	  " TMPLINST /SITEDN=/o=Organization/ou=Site /DISPLAY_NAME=Testtmpl /NAME=sdk
	  /TYPE=sdk /SYNTAX=c:test.oel /SERVER=Server /MESSAGE_DT=c:\test.blt
	  /RECIPIENT_DT=c:\test.blt /ADDRESS_DT=c:\test.blt /LANGUAGE=409 " (without
	  the quotation marks)
	
	To verify that you now have a one-off address template installed into the
	Exchange site, run the Exchange administration program. You will have a Testtmpl
	object under Site\Configuration\Addressing\One-Off Address Template\English.
	
	If you compose a new note with a client, click the TO button, and then click New,
	you should see a list of one-off address templates that includes the Testtmpl
	template.
	
	Additional query words:
	
	======================================================================
	Keywords          : kbEDK kbExchange550 kbMsg kbEDK550 kbGrpDSMsg kbDSupport 
	Technology        : kbExchangeSearch kbExchange550 kbZNotKeyword2
	Version           : winnt:5.5
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
