---
layout: page
title: "Q221992: HOWTO: Add Support for Hosting VBScript to Your MFC Application"
permalink: /kb/221/Q221992/
---

## Q221992: HOWTO: Add Support for Hosting VBScript to Your MFC Application

{% raw %}

	Article: Q221992
	Product(s): Microsoft C Compiler
	Version(s): winnt:5.0,6.0
	Operating System(s): 
	Keyword(s): kbole kbActiveX kbAXScript kbCOMt kbJScript kbMFC kbVBScript kbVC500 kbVC600 kbGrpDSO k
	Last Modified: 01-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Visual C++, 32-bit Enterprise Edition, versions 5.0, 6.0 
	- Microsoft Visual C++, 32-bit Professional Edition, versions 5.0, 6.0 
	- Microsoft Visual C++, 32-bit Learning Edition, version 6.0 
	- The Microsoft Foundation Classes (MFC) 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	You can add VBA-like scripting capability to your MFC application with little
	overhead, using Microsoft ActiveX Scripting technologies. This article
	demonstrates how to create a new MFC application, or modify an existing one,
	that incorporates support for VBScript.
	
	MORE INFORMATION
	================
	
	Follow the steps below to build and run the example:
	
	1. Create a new MFC dialog-based application, or use an application you already
	  have to which you would like to add scripting support.
	
	2. Add an edit box and button to your dialog, and enable the "Want return" and
	  "Multiline" styles in the properties for the edit box.
	
	3. Use ClassWizard (CTRL-W), under the Member Variables tab, to associate
	  IDC_EDIT1 with a member variable of type CEdit named m_edit1.
	
	4. Use ClassWizard to create a new class called MyScriptObject, derived from
	  CCmdTarget, with support for Automation. Click OK if you see a warning about
	  an ODL file.
	
	5. Under the Automation tab in ClassWizard, select MyScriptObject, and add the
	  following methods:
	
	  long gcd(long a, long b);
	  void HelpAbout();
	  void ShowValue(LPCTSTR prompt, long n);
	
	6. Implement gcd, HelpAbout, and ShowValue as follows:
	
	     long MyScriptObject::gcd(long a, long b) 
	     {
	        int l, h, t;
	        if(a < b) {
	           l = a;
	           h = b;
	        }
	        else if(a > b) {
	           l = b;
	           h = a;
	        }
	        else return a;
	
	        while(h%l != 0) {
	           t = l;
	           l = (h%l);
	           h = t;
	        }
	        return l;
	     }
	
	     void MyScriptObject::HelpAbout() 
	     {
	        AfxMessageBox("HelpAbout: My Script Object!", 0x10000);
	     }
	
	     void MyScriptObject::ShowValue(LPCTSTR prompt, long n) 
	     {
	        CString str;
	        str.Format("%s%d", prompt, n);
	        AfxMessageBox(str, MB_SETFOREGROUND);
	     }
	
	7. Open MyScriptObject.h, and move the virtual destructor ~MyScriptObject from
	  the protected section of the class to a public section.
	
	8. Double-click the dialog button to create a handler function for it, and
	  implement it as follows:
	
	     // Initialize our IActiveScriptSite implementation with your
	     // script object's IUnknown interface...
	     g_iActiveScriptSite.m_pUnkScriptObject = 
	        m_myScriptObject.GetInterface(&IID_IUnknown);
	
	     // Start inproc script engine, VBSCRIPT.DLL
	     HRVERIFY(CoCreateInstance(CLSID_VBScript, NULL, CLSCTX_INPROC_SERVER, 
	        IID_IActiveScript, (void **)&m_iActiveScript), 
	        "CoCreateInstance() for CLSID_VBScript");
	
	     // Get engine's IActiveScriptParse interface.
	     HRVERIFY(m_iActiveScript->QueryInterface(IID_IActiveScriptParse, 
	        (void **)&m_iActiveScriptParse), 
	        "QueryInterface() for IID_IActiveScriptParse");
	
	     // Give engine our IActiveScriptSite interface...
	     HRVERIFY(m_iActiveScript->SetScriptSite(&g_iActiveScriptSite), 
	        "IActiveScript::SetScriptSite()");
	
	     // Give the engine a chance to initialize itself...
	     HRVERIFY(m_iActiveScriptParse->InitNew(),
	        "IActiveScriptParse::InitNew()");
	
	     // Add a root-level item to the engine's name space...
	     HRVERIFY(m_iActiveScript->AddNamedItem(L"MyObject", 
	        SCRIPTITEM_ISVISIBLE | SCRIPTITEM_ISSOURCE),
	        "IActiveScript::AddNamedItem()");	
	
	     // Get script code...
	     CString csScriptText;
	     m_edit1.GetWindowText(csScriptText);
	
	     // Parse the code scriptlet...
	     EXCEPINFO ei;
	     BSTR pParseText = csScriptText.AllocSysString();
	     m_iActiveScriptParse->ParseScriptText(pParseText, L"MyObject", NULL,
	        NULL, 0, 0, 0L, NULL, &ei);
	
	     // Set the engine state. This line actually triggers the execution
	     // of the script.
	     m_iActiveScript->SetScriptState(SCRIPTSTATE_CONNECTED);
	
	     // Release engine...
	     m_iActiveScriptParse->Release();
	     m_iActiveScript->Release();
	
	9. Open your [projectname]Dlg.h file and add the following member variables to a
	  public section of your class:
	
	     MyScriptObject m_myScriptObject;
	     IActiveScript *m_iActiveScript;
	     IActiveScriptParse *m_iActiveScriptParse;
	
	10. Also in [projectname]Dlg.h, add the following #include statements, just
	  before the declaration of your class:
	
	     // Include ActiveX Script definitions...
	     #include <activscp.h>
	     // Include definition for MyScriptObject...
	     #include "MyScriptObject.h"
	
	11. Add the following code to your [projectname]Dlg.cpp file, just before the
	  implementation of your button handler:
	
	  // Your IActiveScriptSite implementation...
	  class MyActiveScriptSite : public IActiveScriptSite {
	  private:
	     ULONG m_dwRef; // Reference count
	  public:
	     IUnknown *m_pUnkScriptObject; // Pointer to your object that is exposed
	                                   // to the script engine in GetItemInfo().
	     
	     MyActiveScriptSite::MyActiveScriptSite() {m_dwRef = 1;}
	     MyActiveScriptSite::~MyActiveScriptSite() {}
	     
	     // IUnknown methods...
	     virtual HRESULT _stdcall QueryInterface(REFIID riid, void **ppvObject) {
	        *ppvObject = NULL;
	        return E_NOTIMPL;
	     }
	     virtual ULONG _stdcall AddRef(void) {
	        return ++m_dwRef;
	     }
	     virtual ULONG _stdcall Release(void) {
	        if(--m_dwRef == 0) return 0;
	        return m_dwRef;
	     }
	     
	     // IActiveScriptSite methods...
	     virtual HRESULT _stdcall GetLCID(LCID *plcid) {
	        return S_OK;
	     }
	     
	     virtual HRESULT _stdcall GetItemInfo(LPCOLESTR pstrName,
	        DWORD dwReturnMask, IUnknown **ppunkItem, ITypeInfo **ppti) {
	
	        // Is it expecting an ITypeInfo?
	        if(ppti) {
	           // Default to NULL.
	           *ppti = NULL;
	           
	           // Return if asking about ITypeInfo... 
	           if(dwReturnMask & SCRIPTINFO_ITYPEINFO)
	              return TYPE_E_ELEMENTNOTFOUND;
	        }
	        
	        // Is the engine passing an IUnknown buffer?
	        if(ppunkItem) {
	           // Default to NULL.
	           *ppunkItem = NULL;
	           
	           // Is Script Engine looking for an IUnknown for our object?
	           if(dwReturnMask & SCRIPTINFO_IUNKNOWN) {
	              // Check for our object name...
	              if (!_wcsicmp(L"MyObject", pstrName)) {
	                 // Provide our object.
	                 *ppunkItem = m_pUnkScriptObject;
	                 // Addref our object...
	                 m_pUnkScriptObject->AddRef();
	              }
	           }
	        }
	        
	        return S_OK;
	     }
	     
	     virtual HRESULT __stdcall GetDocVersionString(BSTR *pbstrVersion) {
	        return S_OK;
	     }
	     
	     virtual HRESULT __stdcall OnScriptTerminate(const VARIANT *pvarResult,
	        const EXCEPINFO *pexcepInfo) {
	        return S_OK;
	     }
	     
	     virtual HRESULT __stdcall OnStateChange(SCRIPTSTATE ssScriptState) {
	        return S_OK;
	     }
	     
	     virtual HRESULT __stdcall OnScriptError(
	        IActiveScriptError *pscriptError) {
	        static BSTR pwcErrorText;
	        pscriptError->GetSourceLineText(&pwcErrorText);
	
	        AfxMessageBox(
	           CString("IActiveScriptSite::OnScriptError()\n") + 
	           CString("Line: ") + 
	           CString(pwcErrorText),
	           MB_SETFOREGROUND);
	        ::SysFreeString(pwcErrorText);
	        return S_OK;
	     }
	     
	     virtual HRESULT __stdcall OnEnterScript(void) {
	        return S_OK;
	     }
	     
	     virtual HRESULT __stdcall OnLeaveScript(void) {
	        return S_OK;
	     }
	  };
	
	  // Global instance of our IActiveScriptSite implementation.
	  MyActiveScriptSite g_iActiveScriptSite;
	
	  // Script Engine CLSIDs...
	  #include <initguid.h>
	  DEFINE_GUID(CLSID_VBScript, 0xb54f3741, 0x5b07, 0x11cf, 0xa4, 0xb0, 0x0,
	     0xaa, 0x0, 0x4a, 0x55, 0xe8);
	  DEFINE_GUID(CLSID_JScript, 0xf414c260, 0x6ac0, 0x11cf, 0xb6, 0xd1, 0x00,
	     0xaa, 0x00, 0xbb, 0xbb, 0x58);
	
	  // Ole-initialization class.
	  class OleInitClass {
	  public:
	     OleInitClass() {
	        OleInitialize(NULL);
	     }
	     ~OleInitClass() {
	        OleUninitialize();
	     }
	  };
	  // This global class calls OleInitialize() at
	  // application startup, and calls OleUninitialize()
	  // at application exit...
	  OleInitClass g_OleInitClass;
	
	  void HRVERIFY(HRESULT hr, char * msg)
	  {
	     if(FAILED(hr)) {
	        CString str;
	        str.Format("Error: 0x%08lx (%s)", hr, msg);
	        AfxMessageBox(str, 0x10000);
	        _exit(0);
	     }
	
	  }
	
	12. Compile and run.
	
	After you build the project, run it, add the following VBScript to your
	application's edit box, then click the button:
	
	     dim x
	     dim y
	     dim z
	     x = 101*199
	     y = 313*199
	     z = gcd(x, y)
	
	     ShowValue "gcd(" & x & ", " & y & ") = ", z
	
	     HelpAbout
	
	The basic work flow is as follows:
	
	1. You start the VBScript engine, vbscript.dll, and obtain IActiveScript and
	  IActiveScriptParse interfaces.
	
	2. You give the VBScript engine your implementation of IActiveScriptSite, which
	  the engine uses later to obtain and call to your objects.
	
	3. You add the objects that you implement and want to make available to scripts
	  by calling IActiveScript::AddNamedItem().
	
	4. You provide the script text to execute through
	  IActiveScriptParse::ParseScriptText(). Note that this doesn't actually run
	  the script yet.
	
	5. The script engine will now call into your IActiveScriptSite::GetItemInfo()
	  for any objects it doesn't recognize, to get their interface pointers.
	
	6. You call IActiveScript::SetScriptState() with SCRIPT_STATE_CONNECTED to run
	  the script.
	
	7. The VBScript engine parses the text in the script for you and when it
	  encounters a method call or property reference, it delegates the
	  implementation to your provided interfaces.
	
	REFERENCES
	==========
	
	For additional information about Microsoft ActiveX Script Hosting, please see
	the following articles in the Microsoft Knowledge Base:
	
	  Q183698 SAMPLE: AXSH.EXE Demonstrates Implementing ActiveX Script Hosts
	
	  Q168214 SAMPLE: MFCAXS Implements an Active Script Host Using MFC
	
	(c) Microsoft Corporation 1999, All Rights Reserved.
	Contributions by Joe Crump, Microsoft Corporation
	
	
	Additional query words: vba sdk
	
	======================================================================
	Keywords          : kbole kbActiveX kbAXScript kbCOMt kbJScript kbMFC kbVBScript kbVC500 kbVC600 kbGrpDSO kbActiveXScript 
	Technology        : kbVCsearch kbAudDeveloper kbMFC kbVC500 kbVC600 kbVC32bitSearch kbVC500Search
	Version           : winnt:5.0,6.0
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
