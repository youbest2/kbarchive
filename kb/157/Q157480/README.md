---
layout: page
title: "Q157480: INFO: STL Sample for the rotate_copy Function"
permalink: /kb/157/Q157480/
---

## Q157480: INFO: STL Sample for the rotate_copy Function

{% raw %}

	Article: Q157480
	Product(s): Microsoft C Compiler
	Version(s): winnt:4.2,5.0,6.0
	Operating System(s): 
	Keyword(s): _IK kbVC420 kbVC500 kbVC600 kbDSupport
	Last Modified: 05-MAY-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- The Standard C++ Library, used with:
	   - Microsoft Visual C++, 32-bit Enterprise Edition, version 4.2 
	   - Microsoft Visual C++, 32-bit Professional Edition, version 4.2 
	   - Microsoft Visual C++, 32-bit Enterprise Edition, version 5.0 
	   - Microsoft Visual C++, 32-bit Professional Edition, version 5.0 
	   - Microsoft Visual C++, 32-bit Enterprise Edition, version 6.0 
	   - Microsoft Visual C++, 32-bit Professional Edition, version 6.0 
	   - Microsoft Visual C++, 32-bit Learning Edition, version 6.0 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	The sample code below illustrates how to use the rotate_copy STL function in
	Visual C++.
	
	MORE INFORMATION
	================
	
	Required Header
	---------------
	
	     <algorithm>
	
	Prototype
	---------
	
	     template<class ForwardIterator, class OutputIterator> inline
	     OutputIterator rotate_copy(BidirectionalIterator first,
	
	                                BidirectionalIterator middle,
	                                BidirectionalIterator last,
	                                OutputIterator result)
	
	NOTE: The class/parameter names in the prototype do not match the version in the
	header file. Some have been modified to improve readability.
	
	Description
	-----------
	
	The rotate_copy algorithm rotates the elements in the range [first, last), to the
	right by N positions (where N = middle - first), and copies the result into a
	sequence of the same size, starting at result. It returns an iterator positioned
	immediately after the last new element in the resulting sequence.
	
	Note that the OutputIterator should be different from the sequence to be rotated.
	If they are the same, the result will depend on the implementation.
	
	Sample Code
	-----------
	
	  ////////////////////////////////////////////////////////////////////// 
	  // 
	  // Compile options needed: /GX
	  // 
	  // rotate_copy.cpp : Illustrates how to use the rotate_copy function.
	  // 
	  // Functions:
	  // 
	  //    rotate_copy - Rotate a sequence by n positions, copy the
	  //                  results to another same sized sequence.
	  // 
	  // Written by Kalindi Sanghrajka
	  // of Microsoft Product Support Services,
	  // Software Core Developer Support.
	  // Copyright (c) 1996 Microsoft Corporation. All rights reserved.
	  ////////////////////////////////////////////////////////////////////// 
	
	  // disable warning C4786: symbol greater than 255 character,
	  // okay to ignore
	
	  #pragma warning(disable: 4786)
	
	  #include <iostream>
	  #include <vector>
	  #include <string>
	  #include <algorithm>
	  #include <functional>
	  using namespace std;
	
	  #if _MSC_VER > 1020   // if VC++ version is > 4.2
	     using namespace std;  // std c++ libs implemented in std
	     #endif
	
	  void main()
	
	  {
	
	      const int VECTOR_SIZE = 8 ;
	
	      // Define a template class vector of strings
	      typedef vector<string, allocator<string> > StrVector ;
	
	      //Define an iterator for template class vector of strings
	      typedef StrVector::iterator StrVectorIt ;
	
	      StrVector Tongue_Twister(VECTOR_SIZE) ;
	      StrVector Rotated_Twister(VECTOR_SIZE) ;
	
	      StrVectorIt start, middle, end, it, RTstart, RTend ;
	
	      start = Tongue_Twister.begin() ;    // location of first
	                                          // element of Tongue_Twister
	
	      end = Tongue_Twister.end() ;        // one past the location last
	                                          // element of Tongue_Twister
	
	      middle = start + 3 ;                // start position for
	                                          // rotating elements
	
	      RTstart = Rotated_Twister.begin() ; // location of first
	                                          // element of Rotated_Twister
	
	      RTend = Rotated_Twister.end() ;     // one past the location last
	                                          // element of Rotated_Twister
	
	      //Initialize vector Tongue_Twister
	      Tongue_Twister[0] = "she" ;
	      Tongue_Twister[1] = "sells" ;
	      Tongue_Twister[2] = "sea" ;
	      Tongue_Twister[3] = "shells" ;
	      Tongue_Twister[4] = "by";
	      Tongue_Twister[5] = "the";
	      Tongue_Twister[6] = "sea" ;
	      Tongue_Twister[7] = "shore" ;
	
	      cout << "Before calling rotate_copy:\n" << endl ;
	
	      // print content of Tongue_Twister
	      cout << "Try this Tongue Twister: " ;
	      for(it = start; it != end; it++)
	          cout << *it << " " ;
	      cout << "\n\n" ;
	
	      // rotate the items in the vector Tongue_Twist to the right by
	      // 3 positions and copy the results to Rotated_Twister
	      rotate_copy(start, middle, end, RTstart) ;
	
	      cout << "After calling rotate_copy:\n" << endl ;
	
	      // print content of Tongue_Twister
	      cout << "Tongue_Twister: " ;
	      for(it = start; it != end; it++)
	          cout << *it << " " ;
	      cout << "\n\n" ;
	
	      // print content of Rotated_Twister
	      cout << "Now try the rotated Tongue Twister: " ;
	      for(it = RTstart; it != RTend; it++)
	          cout << *it << " " ;
	      cout << "\n\n" ;
	
	  }
	
	Program Output is:
	------------------
	
	Before calling rotate_copy:
	
	Try this Tongue Twister: she sells sea shells by the sea shore
	
	After calling rotate_copy:
	
	Tongue_Twister: she sells sea shells by the sea shore
	
	Now try the rotated Tongue Twister: shells by the sea shore she sells sea
	
	REFERENCES
	==========
	
	Visual C++ Books On Line: Visual C++ Books:C/C++:Standard C++ Library Reference.
	
	Additional query words: STL STLSample rotate_copy
	
	======================================================================
	Keywords          : _IK kbVC420 kbVC500 kbVC600 kbDSupport 
	Technology        : kbVCsearch kbAudDeveloper kbVCLibrary
	Version           : winnt:4.2,5.0,6.0
	Issue type        : kbinfo
	
	=============================================================================
	

{% endraw %}
