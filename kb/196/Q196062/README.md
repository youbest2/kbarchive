---
layout: page
title: "Q196062: HOWTO: Set and Get Cookies for a URL Using WinInet APIs"
permalink: /kb/196/Q196062/
---

## Q196062: HOWTO: Set and Get Cookies for a URL Using WinInet APIs

{% raw %}

	Article: Q196062
	Product(s): Microsoft Visual Basic for Windows
	Version(s): WINDOWS:5.0,6.0
	Operating System(s): 
	Keyword(s): kbAPI kbInternet kbVBp500 kbVBp600 kbGrpDSVB kbInetDev
	Last Modified: 17-MAY-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual Basic Professional Edition for Windows, versions 5.0, 6.0 
	- Microsoft Visual Basic Enterprise Edition for Windows, versions 5.0, 6.0 
	- Microsoft Windows Internet Services (WinInet) 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	From a Visual Basic application, you can set and get cookies on a client that
	corresponds to a given URL by using the InternetSetCookie and InternetGetCookie
	APIs from the WinInet.dll.
	
	MORE INFORMATION
	================
	
	1. Create a new standard .exe project in Visual Basic. Form1 is created by
	  default.
	
	2. Add the following controls to Form1:
	
	     Control           Name           Caption
	     --------------------------------------------------
	     Command Button    Command1       InternetSetCookie
	     Command Button    Command2       InternetGetCookie
	
	3. In Form1, add the following code in the code window:
	
	        Option Explicit
	
	        ' No more data is available.
	        Const ERROR_NO_MORE_ITEMS = 259
	
	        ' The data area passed to a system call is too small.
	        Const ERROR_INSUFFICIENT_BUFFER = 122
	
	        Private Declare Function InternetSetCookie Lib "wininet.dll" _
	         Alias "InternetSetCookieA" _
	         (ByVal lpszUrlName As String, _
	         ByVal lpszCookieName As String, _
	         ByVal lpszCookieData As String) As Boolean
	
	        Private Declare Function InternetGetCookie Lib "wininet.dll" _
	         Alias "InternetGetCookieA" _
	         (ByVal lpszUrlName As String, _
	         ByVal lpszCookieName As String, _
	         ByVal lpszCookieData As String, _
	         lpdwSize As Long) As Boolean
	
	        Private Sub Command1_Click()
	         Dim bRet As Boolean
	         bRet = InternetSetCookie("http://xxxx/xxxx.htm", _
	          "Test", "Sent as Test via VB")
	         If bRet = False Then
	             MsgBox "Failed"
	         End If
	        End Sub
	
	        Private Sub Command2_Click()
	          Dim sCookieVal As String * 256
	          Dim bRet As Boolean
	          bRet = InternetGetCookie("http://xxxx/xxxx.htm", _
	           "Test", sCookieVal, 255)
	          If bRet = False Then
	            MsgBox "Failed"
	          Else
	            MsgBox sCookieVal
	          End If
	        End Sub
	
	REFERENCES
	==========
	
	For more information on the WinInet APIs (and specifically the InternetSetCookie
	and InternetGetCookie functions), please see the WinInet documentation in the
	MSDN library and the following Web sites:
	
	WinInet.dll:
	
	  http://msdn.microsoft.com/workshop/networking/wininet/wininet.asp
	
	Cookie APIs:
	
	  http://msdn.microsoft.com/workshop/networking/wininet/overview/cookie.asp
	
	Additional query words:
	
	======================================================================
	Keywords          : kbAPI kbInternet kbVBp500 kbVBp600 kbGrpDSVB kbInetDev 
	Technology        : kbVBSearch kbAudDeveloper kbZNotKeyword6 kbZNotKeyword2 kbVB500Search kbVB600Search kbVB500 kbVB600
	Version           : WINDOWS:5.0,6.0
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
