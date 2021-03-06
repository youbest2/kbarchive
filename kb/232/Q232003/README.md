---
layout: page
title: "Q232003: HOWTO: Determine the Version of DCOM 95/98 Using Visual Basic"
permalink: /kb/232/Q232003/
---

## Q232003: HOWTO: Determine the Version of DCOM 95/98 Using Visual Basic

{% raw %}

	Article: Q232003
	Product(s): Microsoft Visual Basic for Windows
	Version(s): 5.0,6.0
	Operating System(s): 
	Keyword(s): kbAPI kbDCOM kbRegistry kbSDKWin32 kbVBp kbVBp500 kbVBp600 kbGrpDSVB
	Last Modified: 11-JAN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual Basic Learning Edition for Windows, versions 5.0, 6.0 
	- Microsoft Visual Basic Professional Edition for Windows, versions 5.0, 6.0 
	- Microsoft Visual Basic Enterprise Edition for Windows, versions 5.0, 6.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	The version of DCOM95 or DCOM98 installed on a Windows 9x system may be
	determined by checking the registry using Visual Basic. If DCOM is installed on
	the system, the default value of the registry key:
	
	HKCR\CLSID\{bdc67890-4fc0-11d0-a805-00aa006d2ea4}\InstalledVersion
	
	will contain the version of DCOM installed on the system. The version number in
	the registry is stored in the format "a,b,c,d", where a, b, c, and d are numeric
	values. These values form the version number of the DCOM install:
	
	+-----------------------------------------------------------------------+
	| InstalledVersion | DCOM Version                                       | 
	+-----------------------------------------------------------------------+
	| "4,71,0,3328"    | DCOM95 and DCOM98 1.3 4.71.0.3328                  | 
	+-----------------------------------------------------------------------+
	| "4,71,0,2618"    | DCOM95 1.2 Web Release 4.71.0.2618                 | 
	+-----------------------------------------------------------------------+
	| "4,71,0,2612"    | DCOM 1.2 4.71.0.2612 DCOM98.exe shipped with VS6.0 | 
	+-----------------------------------------------------------------------+
	| "4,71,0,1719"    | DCOM Win98 Gold 4.71.0.1719                        | 
	+-----------------------------------------------------------------------+
	| "4,71,0,1718"    | DCOM95 1.1 4.71.0.1718                             | 
	+-----------------------------------------------------------------------+
	| "4,71,0,1120"    | DCOM 1.x 4.71.0.1120                               | 
	+-----------------------------------------------------------------------+
	
	MORE INFORMATION
	================
	
	The following steps outline this process from Visual Basic:
	
	1. Start a new Visual Basic Standard EXE project. Form1 is created by default.
	
	2. Add a CommandButton (Command1) to Form1.
	
	3. Add the following code to the General Declarations section of Form1:
	
	  Option Explicit
	
	  Private Const ERROR_SUCCESS = 0&
	
	  Private Const HKEY_LOCAL_MACHINE = &H80000002
	  Private Const HKEY_CLASSES_ROOT = &H80000000
	
	  Private Const STANDARD_RIGHTS_ALL = &H1F0000
	  Private Const KEY_QUERY_VALUE = &H1
	  Private Const KEY_SET_VALUE = &H2
	  Private Const KEY_CREATE_SUB_KEY = &H4
	  Private Const KEY_ENUMERATE_SUB_KEYS = &H8
	  Private Const KEY_NOTIFY = &H10
	  Private Const KEY_CREATE_LINK = &H20
	  Private Const SYNCHRONIZE = &H100000
	
	  Private Const KEY_ALL_ACCESS = _
	     ((STANDARD_RIGHTS_ALL Or _
	       KEY_QUERY_VALUE Or _
	       KEY_SET_VALUE Or _
	       KEY_CREATE_SUB_KEY Or _
	       KEY_ENUMERATE_SUB_KEYS Or _
	       KEY_NOTIFY Or _
	       KEY_CREATE_LINK _
	      ) _
	      And (Not SYNCHRONIZE) _
	     )
	
	  Private Declare Function RegOpenKeyEx _
	     Lib "advapi32.dll" Alias "RegOpenKeyExA" _
	     (ByVal hKey As Long, _
	      ByVal lpSubKey As String, _
	      ByVal ulOptions As Long, _
	      ByVal samDesired As Long, _
	      phkResult As Long) _
	     As Long
	
	  Private Declare Function RegCloseKey Lib _
	     "advapi32.dll" _
	     (ByVal hKey As Long) _
	     As Long
	
	  Private Declare Function RegQueryValueEx Lib _
	     "advapi32.dll" Alias "RegQueryValueExA" _
	     (ByVal hKey As Long, _
	      ByVal lpValueName As String, _
	      ByVal lpReserved As Long, _
	      lpType As Long, _
	      ByVal lpData As String, _
	      lpcbData As Long) _
	     As Long
	     
	  ' Note that if you declare the lpData
	  ' parameter as String, you must pass it
	  ' By Value as is done here.
	
	  Private Declare Function GetProcAddress _
	     Lib "kernel32" _
	     (ByVal hModule As Long, _
	      ByVal lpProcName As String) _
	     As Long
	
	  Private Declare Function GetModuleHandle _
	     Lib "kernel32" Alias "GetModuleHandleA" _
	     (ByVal lpModuleName As String) _
	     As Long
	     
	  Private Function DCOMEnabled() As Boolean
	  ' We need to check two things
	  ' 1- OLE32 supports free threading
	  ' 2- DCOM is enabled in the registry
	  ' See Inside COM, Rogerson, pp 276-277
	
	     DCOMEnabled = False
	     
	  ' First, check to see if OLE32 supports free threading.
	  ' You need to check for the CoInitializeEx function's
	  ' presence in OLE32.
	  ' 1- Get a handle to the OLE32 module
	  ' 2- Try to get a ProcAddress for CoInitializeEx
	
	     Dim OLE32ModuleHandle As Long
	     Dim CoInitializeExProcAddress As Long
	     
	     OLE32ModuleHandle = GetModuleHandle("OLE32")
	     Debug.Assert (Not OLE32ModuleHandle = 0)
	     
	     CoInitializeExProcAddress = GetProcAddress( _
	             OLE32ModuleHandle, _
	             "CoInitializeEx")
	           
	     Debug.Print "CoInitializeExProcAddress = " _
	                 & CoInitializeExProcAddress
	                 
	     If CoInitializeExProcAddress = 0 Then
	        DCOMEnabled = False
	        Exit Function
	     End If
	     
	  ' Now check the registry to see if DCOM is enabled.
	     
	     Dim lResult As Long
	     Dim hKey As Long
	
	     lResult = RegOpenKeyEx(HKEY_LOCAL_MACHINE, _
	                     "SOFTWARE\Microsoft\Ole", _
	                     0, _
	                     KEY_ALL_ACCESS, _
	                     hKey)
	     
	     Debug.Assert (lResult = ERROR_SUCCESS)
	
	     Dim rgch As String
	     rgch = String(2, 0)
	     
	     Dim cbrgch As Long
	     cbrgch = Len(rgch)
	     
	     lResult = RegQueryValueEx(hKey, "EnableDCOM", 0, 0&, rgch, cbrgch)
	
	     Debug.Assert (lResult = ERROR_SUCCESS)
	
	     Debug.Print "Mid$(rgch, 1) is " & Mid$(rgch, 1)
	
	     If (Mid$(rgch, 1, 1) = "Y" Or Mid$(rgch, 1, 1) = "y") Then
	        ' DCOM is Enabled
	        DCOMEnabled = True
	     Else
	        DCOMEnabled = False
	     End If
	                     
	     lResult = RegCloseKey(hKey)
	             
	  End Function
	
	  Public Function GetDCOMVersion() As String
	      ' Check the registry key "InstalledVersion" to see which
	      ' version of DCOM is installed.
	
	     Dim hKey As Long
	     Dim lResult As Long
	
	  ' First confirm that DCOM is installed
	     If Not DCOMEnabled() Then
	         MsgBox "Can't check version.  DCOM is not installed."
	         Exit Function
	     End If
	
	  ' open the the proper registry key
	     lResult = RegOpenKeyEx(HKEY_CLASSES_ROOT, _
	           "CLSID\{bdc67890-4fc0-11d0-a805-00aa006d2ea4}\InstalledVersion", _
	           0, _
	           KEY_ALL_ACCESS, _
	           hKey)
	
	     If Not lResult = ERROR_SUCCESS Then
	         MsgBox "Could not open registry key"
	         Exit Function
	     End If
	
	     Dim rgch As String
	     rgch = String(64, 0)
	
	     Dim cbrgch As Long
	     cbrgch = Len(rgch)
	
	     lResult = RegQueryValueEx(hKey, "", 0, 0&, rgch, cbrgch)
	
	     lResult = RegCloseKey(hKey)
	
	     Dim temp As String
	
	     temp = Mid$(rgch, 1, cbrgch)
	
	     GetDCOMVersion = temp
	
	  End Function
	
	  Private Sub Command1_Click()
	     MsgBox GetDCOMVersion()
	  End Sub
	
	4. Run the program and click Command1.
	
	Result: If DCOM is installed on the system, the message box will display the
	version number.
	Notes:
	
	The function DCOMEnabled may be used separately to determine if DCOM has been
	installed on a system without checking for the version.
	
	It is not necessary to test for DCOM on Windows NT 4.0 or Windows 2000 because it
	is already installed. (See REFERENCES below.)
	
	The most current version of DCOM for Windows 95 and 98 might be downloaded from:
	
	http://www.microsoft.com/com/resources/downloads.asp
	
	REFERENCES
	==========
	
	For additional information about DCOM, please see the following:
	
	"Inside COM", Dale Rogerson, c1997 Microsoft Press pp. 276-277
	
	For additional information, click the article numbers below to view the articles
	in the Microsoft Knowledge Base:
	
	  Q266717 HOWTO: Create a DCOM Client/Server Application by Using Visual Basic
	
	  Q267836 HOWTO: Create a DCOM Client/Server with Events by Using Visual Basic
	
	  Q268550 HOWTO: Use Dcomcnfg for a Visual Basic DCOM Client/Server Application
	
	  Q269330 HOWTO: Troubleshoot DCOM for Visual Basic Client/Server Applications
	
	For information about programmatically determining the OS, please see the
	following article in the Microsoft Knowledge Base:
	
	  Q189249 HOWTO: Determine Which 32-Bit Windows Version Is Being Used
	
	(c) Microsoft Corporation 1999, All Rights Reserved.
	Contributions by Gray McDonald, Microsoft Corporation
	
	
	Additional query words:
	
	======================================================================
	Keywords          : kbAPI kbDCOM kbRegistry kbSDKWin32 kbVBp kbVBp500 kbVBp600 kbGrpDSVB 
	Technology        : kbVBSearch kbAudDeveloper kbZNotKeyword6 kbZNotKeyword2 kbVB500Search kbVB600Search kbVBA500 kbVBA600 kbVB500 kbVB600
	Version           : :5.0,6.0
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
