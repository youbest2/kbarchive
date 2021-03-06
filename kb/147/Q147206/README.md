---
layout: page
title: "Q147206: FIX: Border of Modeless CPropertySheet Is Not 3D in Windows NT"
permalink: /kb/147/Q147206/
---

## Q147206: FIX: Border of Modeless CPropertySheet Is Not 3D in Windows NT

{% raw %}

	Article: Q147206
	Product(s): Microsoft C Compiler
	Version(s): winnt:4.0
	Operating System(s): 
	Keyword(s): kbDlg kbMFC KbUIDesign kbVC400bug kbVC410fix kbGrpDSMFCATL
	Last Modified: 06-MAY-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- The Microsoft Foundation Classes (MFC), included with:
	   - Microsoft Visual C++, 32-bit Editions, version 4.0 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	If you create a modeless CPropertySheet under Windows NT, its outer border will
	not be a 3D border. A modal CPropertySheet will have a 3D border. Both modal and
	modeless CPropertySheets have a 3D border under Windows 95.
	
	CAUSE
	=====
	
	MFC sets up a callback function for modeless CPropertySheets called
	AfxPropSheetCallback(). This function checks for PSCB_PRECREATE, which is a
	message that is received before a property sheet is created. In this handler,
	MFC takes out the DS_MODALFRAME style.
	
	Ctl3d32.dll is used by Windows NT to paint 3D borders for controls and windows.
	For a dialog box to have a 3D border, CTL3D requires a style of DS_MODALFRAME.
	
	RESOLUTION
	==========
	
	1. Derive a class from CPropertySheet (CMySheet) and override its Create().
	  Comment the call to CWnd::Create() that the ClassWizard puts in.
	
	2. Copy code from CPropertySheet::Create() in DLGPROP.CPP (as shown below) into
	  CMySheet::Create(), and change the parameters it takes accordingly.
	
	3. Change this line:
	
	        m_psh.dwFlags |= (PSH_MODELESS|PSH_USECALLBACK);
	
	  to:
	
	        m_psh.dwFlags |= PSH_MODELESS;
	
	  The callback function isn't set so that PSCB_PRECREATE is not handled, and the
	  DS_MODALFRAME style is not removed.
	
	4. Comment out this line:
	
	     m_psh.pfnCallback = AfxPropSheetCallback;
	
	5. Include <afxpriv.h> in MySheet.h.
	
	6. In MySheet.h, change the MySheet.Create to take the corresponding
	  parameters:
	
	     BOOL Create(CWnd* pParentWnd = NULL, DWORD dwStyle = WS_SYSMENU |
	                  WS_POPUP | WS_CAPTION | DS_MODALFRAME | WS_VISIBLE,
	                  DWORD dwExStyle = WS_EX_DLGMODALFRAME );
	
	STATUS
	======
	
	Microsoft has confirmed this to be a bug in the Microsoft products listed at the
	beginning of this article. This problem was corrected in Visual C++, 32-bit
	Edition, version 4.1.
	
	MORE INFORMATION
	================
	
	Sample Code
	-----------
	
	  // in MySheet.h
	  #include <afxpriv.h>
	
	  BOOL Create(CWnd* pParentWnd = NULL, DWORD dwStyle = WS_SYSMENU |
	        WS_POPUP | WS_CAPTION | DS_MODALFRAME | WS_VISIBLE,
	        DWORD dwExStyle = WS_EX_DLGMODALFRAME );
	
	  // In MySheet.cpp
	  // CMySheet is derived from CPropertySheet
	  BOOL CMySheet::Create(CWnd* pParentWnd, DWORD dwStyle, DWORD dwExStyle)
	  {
	       _AFX_THREAD_STATE* pState = AfxGetThreadState();
	       pState->m_dwPropStyle = dwStyle;
	       pState->m_dwPropExStyle = dwExStyle;
	
	       ASSERT_VALID(this);
	       ASSERT(m_hWnd == NULL);
	
	   // WS_SYSMENU must not be set if a property sheet is created as a child
	
	       if (dwStyle & WS_CHILD)
	            dwStyle &= ~WS_SYSMENU;
	
	       // finish building PROPSHEETHEADER structure
	       BuildPropPageArray();
	       m_bModeless = TRUE;
	  // original line specifies a callback function
	  //   m_psh.dwFlags |= (PSH_MODELESS|PSH_USECALLBACK);
	  // new line does not specify a callback function
	       m_psh.dwFlags |= PSH_MODELESS;
	  //   m_psh.pfnCallback = AfxPropSheetCallback;
	       m_psh.hwndParent = pParentWnd->GetSafeHwnd();
	
	       // hook the window creation process
	       AfxHookWindowCreate(this);
	       HWND hWnd = (HWND)PropertySheet(&m_psh);
	
	       // clean up on failure, otherwise return TRUE
	       if (!AfxUnhookWindowCreate())
	            PostNcDestroy();     // cleanup if Create fails
	
	       if (hWnd == NULL || hWnd == (HWND)-1)
	            return FALSE;
	       ASSERT(hWnd == m_hWnd);
	
	       return TRUE;
	  }
	
	  /* Compile options needed: default
	  */ 
	
	Additional query words: 4.00 border CPropertySheet modeless Property Sheet vcfixlist410
	
	======================================================================
	Keywords          : kbDlg kbMFC KbUIDesign kbVC400bug kbVC410fix kbGrpDSMFCATL 
	Technology        : kbAudDeveloper kbMFC
	Version           : winnt:4.0
	Issue type        : kbbug
	Solution Type     : kbfix
	
	=============================================================================
	

{% endraw %}
