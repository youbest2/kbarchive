---
layout: page
title: "Q251059: HOWTO: Provide Your Own Window Class Name for an MFC Dialog Box"
permalink: /kb/251/Q251059/
---

## Q251059: HOWTO: Provide Your Own Window Class Name for an MFC Dialog Box

{% raw %}

	Article: Q251059
	Product(s): Microsoft C Compiler
	Version(s): 5.0,6.0
	Operating System(s): 
	Keyword(s): _IK920 kbDlg kbMFC kbResource kbVC500 kbVC600 kbWndw kbWndwClass kbDSupport kbGrpDSMFCA
	Last Modified: 15-MAY-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- The Microsoft Foundation Classes (MFC), included with:
	   - Microsoft Visual C++, 32-bit Enterprise Edition, versions 5.0, 6.0 
	   - Microsoft Visual C++, 32-bit Professional Edition, versions 5.0, 6.0 
	   - Microsoft Visual C++, 32-bit Learning Edition, version 6.0 
	   - Microsoft Visual C++.NET (2002) 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	This article shows you how to provide your own Window Class Name for a dialog
	box created in an MFC-based application.
	
	You may encounter this need when you try to limit your dialog-based MFC
	application to a single instance.
	
	MORE INFORMATION
	================
	
	Follow the steps outlined below to provide your own Window Class Name.
	
	1. Open your project work space containing the dialog box and click
	  ResourceView.
	
	2. Open the dialog box in Resource Editor. Right-click the dialog box, and then
	  select Properties. Notice an entry for Class Name at the bottom right. This
	  edit box appears disabled if you are using a resource file with Microsoft
	  Foundation Class Library support. To enable this option, switch to the
	  top-level node on the resource view, and then right-click and select
	  Properties. Clear the Enable MFC Features check box. Or for Visual C++ .NET,
	  clear the "MFC Mode property to FALSE". Now display the properties for your
	  dialog box. The Class Name edit box should be enabled. Type the class name;
	  for instance MyPrivateClassName.
	
	3. Alternatively, open the .rc file as a text file. Go to the desired DIALOG
	  resource and add the CLASS option.
	
	  IDD_LIMITDLGINSTANCE_DIALOG DIALOGEX 0, 0, 195, 44
	  STYLE DS_MODALFRAME | WS_POPUP | WS_VISIBLE | WS_CAPTION | WS_SYSMENU
	  EXSTYLE WS_EX_APPWINDOW
	  CAPTION "LimitDlgInstance"
	  CLASS "MyPrivateClassName" // Add your class name here!
	  FONT 8, "MS Sans Serif"
	  BEGIN
	      DEFPUSHBUTTON   "OK",IDOK,138,7,50,14
	      PUSHBUTTON      "Cancel",IDCANCEL,138,23,50,14
	      PUSHBUTTON      "&Test!",IDC_BUTTON1,48,14,49,15
	  END
	
	4. Add the following code in the InitInstance() function of the CWinApp-derived
	  class.
	
	  BOOL CLimitDlgInstanceApp::InitInstance()
	  {
	  	///////////////////////////////////////////////////////////////////////// 
	  	///////////////////////////////////////////////////////////////////////// 
	  	WNDCLASS wc;
	
	  	// Get the info for this class.
	           // #32770 is the default class name for dialogs boxes.
	  	::GetClassInfo(AfxGetInstanceHandle(), "#32770", &wc);
	
	  	// Change the name of the class.
	  	wc.lpszClassName = "MyPrivateClassName";
	
	  	// Register this class so that MFC can use it.
	  	AfxRegisterClass(&wc);	
	  	///////////////////////////////////////////////////////////////////////// 
	  	///////////////////////////////////////////////////////////////////////// 
	
	  // ...
	  }
	
	5. In the step above, in the call to ::GetClassInfo(), make sure to use the
	  correct HINSTANCE call if your dialog resource is located in a separate DLL.
	
	6. Build and run your application. Use the Spy++ tool to verify that the dialog
	  now uses the new class name.
	
	REFERENCES
	==========
	
	- Q141752 Limiting 32-Bit MFC SDI/MDI Applications to a Single Instance
	
	- Q109175 How to Limit an MFC Application to a Single Instance
	
	- Q238100 Limiting 32-bit MFC SDI Applications to a Single Instance in WinCE
	
	- Window Classes
	
	- Dialog Boxes
	
	Additional query words: one instance single limit restrict define personal
	
	======================================================================
	Keywords          : _IK920 kbDlg kbMFC kbResource kbVC500 kbVC600 kbWndw kbWndwClass kbDSupport kbGrpDSMFCATL kbArchitecture kbfaq
	Technology        : kbAudDeveloper kbMFC kbVCNET
	Version           : :5.0,6.0
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
