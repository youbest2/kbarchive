---
layout: page
title: "Q301428: Troubleshooting Outlook Web Access from an IIS Perspective"
permalink: /kb/301/Q301428/
---

## Q301428: Troubleshooting Outlook Web Access from an IIS Perspective

{% raw %}

	Article: Q301428
	Product(s): Internet Information Server
	Version(s): 4.0,5.0
	Operating System(s): 
	Keyword(s): 
	Last Modified: 02-OCT-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Internet Information Server versions 4.0, 5.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	This article describes several ways to troubleshoot two of the most common
	problems that affect Outlook Web Access (OWA) from an IIS perspective:
	
	- Users cannot access the OWA logon page.
	
	- Users cannot change passwords from OWA, either when they log on or from the
	  Options page after logon.
	
	MORE INFORMATION
	================
	
	Troubleshooting OWA Access Problems
	-----------------------------------
	
	Common error messages that users receive when they attempt to access the OWA
	logon page (also called the Gold Page) include the following:
	
	  HTTP 500 Internal Server Error
	
	-or-
	
	  Directory Listing Denied
	
	-or-
	
	  VBScript Runtime Error
	
	To troubleshoot this problem, follow these steps:
	
	1. Verify that the Default Web Site is configured properly. To do this, follow
	  these steps:
	
	  a. Open the Internet Services Manager and expand Default Web Site.
	
	  b. Right-click the Default Web Site and click Properties.
	
	  c. On the Home Directory tab, verify that a Remove button exists next to the
	     Application name box. If you do not see the Remove button, click Create to
	     create the default application.
	
	  d. Click the Directory Security tab. Under Anonymous Access and
	     Authentication Control, click the Edit button.
	
	  e. Verify that Anonymous Access and Windows NT Challenge/Response (in IIS
	     version 4.0) or Integrated Windows Authentication (in IIS version 5.0) are
	     both selected.
	
	  f. Click OK twice to close the property sheet.
	
	2. After you have made sure that the Default Web Site is configured properly,
	  verify that the Exchange virtual folder is configured properly. To do this,
	  follow these steps:
	
	  a. Verify that a virtual folder named Exchange is listed below the Default
	     Web Site.
	
	  b. Right-click the folder and click Properties.
	
	  c. Verify that a Remove button exists next to the Application name box. If
	     you do not see it, click Create to create the Exchange application.
	
	  d. On the Documents tab, verify that Logon.asp is the top default document.
	     If it is not listed, click Add, type "Logon.asp" (without the quotation
	     marks), and move this file to the top of the list.
	
	  e. Click the Directory Security tab. Under Anonymous Access and
	     Authentication Control, click the Edit button.
	
	  f. Verify that Anonymous Access and Windows NT Challenge/Response (in IIS
	     4.0) or Integrated Windows Authentication (in IIS 5.0) are both selected.
	
	  g. Click OK twice to close the property sheet.
	
	Troubleshooting Password Change Problems
	----------------------------------------
	
	When users attempt to change passwords in OWA, they may receive a blank white
	page or the following error message:
	
	  Access Denied
	
	To resolve this problem, do either of the following:
	
	- Verify that the Iisadmpwd folder has been set up correctly. To do this,
	  follow these steps:
	
	NOTE: By default, IIS 5.0 does not create the Iisadmpwd folder. You must create
	this folder to change passwords.
	
	  1. Open the Internet Services Manager and expand Default Web Site.
	
	  2. Verify that a folder named Iisadmpwd exists below the Default Web Site. If
	     you do not see this folder, follow these steps:
	
	     a. Right-click the Default Web Site, click New, click Virtual Directory,
	        and then click Next.
	
	     b. For the alias, type "Iisadmpwd" (without the quotation marks) and click
	        Next.
	
	     c. Browse to \Winnt\System32\Inetsrv\Iisadmpwd, click OK, and then click
	        Next.
	
	     d. Verify that both Run Scripts and Execute are selected and click Next.
	
	     e. Click Finish.
	
	  3. Right-click the Iisadmpwd folder and click Properties.
	
	  4. Verify that Read, Write, and Directory Browsing are cleared.
	
	  5. In IIS 4.0, verify that Permissions are set to Execute (including script).
	     In IIS 5.0, verify that Execute permissions are set to Scripts and
	     Executables.
	
	  6. Click the Directory Security tab. Under Anonymous Access and
	     Authentication Control, click the Edit button.
	
	  7. Verify that Anonymous Access and Windows NT Challenge/Response (in IIS
	     4.0) or Integrated Windows Authentication (in IIS 5.0) are both selected.
	
	  8. Click OK twice to close the property sheet.
	
	- Verify that the domain policy does not prevent password changes.
	
	To do this in Windows NT Server 4.0, follow these steps:
	
	  1. In Administrative Tools, open User Manager for Domains.
	
	  2. On the Policies menu, click Account.
	
	  3. At the bottom of the Account Policy window, ensure that Users must log on
	     in order to change password is cleared.
	
	  4. Click OK.
	
	  5. On the Policies menu, click User Rights.
	
	  6. In the list, select Log on locally and verify that the
	     IUSR_<servername> and IWAM_<servername> accounts are listed.
	     If these accounts are not listed, you must add them. To do so, follow
	     these steps:
	
	     a. Click Add, then click Show Users.
	
	     b. Select the IUSR_<servername> and IWAM_<servername> accounts
	        and click Add.
	
	     c. Click OK.
	
	  7. In the list, select Access this computer from the network and verify that
	     the IUSR_<servername> and IWAM_<servername> accounts are
	     listed. If these accounts are not listed, add them as described
	     previously.
	
	  8. Click OK to close the User Rights Policy window.
	
	  9. Close the User Manager window.
	
	To do this in Windows 2000 Server, follow these steps:
	
	  1. In Administrative Tools, open Local Security Policy.
	
	  2. Expand Local Policies and select User Rights Assignment.
	
	  3. Double-click Log on locally. Verify that the IUSR_<servername> &
	     IWAM_<servername> accounts are listed and that both Local Policy
	     Setting and Effective Policy Setting are selected.
	
	  4. Double-click Log on as a batch job. Verify that the
	     IUSR_<servername> & IWAM_<servername> accounts are listed
	     and that both Local Policy Setting and Effective Policy Setting are
	     selected.
	
	  5. Double-click Access this computer from the network. Verify that the
	     IUSR_<servername> & IWAM_<servername> accounts are listed
	     and that both Local Policy Setting and Effective Policy Setting are
	     selected.
	
	NOTE: If Effective Policy Setting is not selected, check the User Rights
	Assignment on the domain controller and ensure that Define these policy settings
	is not selected for these user rights.
	
	  6. Close the Local Security Settings window.
	
	Additional query words: IIS4, IIS5, OWA
	
	======================================================================
	Keywords          :  
	Technology        : kbiisSearch kbiis500 kbiis400
	Version           : :4.0,5.0
	Issue type        : kbinfo
	
	=============================================================================
	

{% endraw %}
