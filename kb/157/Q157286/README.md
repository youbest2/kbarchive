---
layout: page
title: "Q157286: STL Sample for the includes Function"
permalink: /kb/157/Q157286/
---

## Q157286: STL Sample for the includes Function

{% raw %}

	Article: Q157286
	Product(s): Microsoft C Compiler
	Version(s): winnt:
	Operating System(s): 
	Keyword(s): _IK
	Last Modified: 05-MAY-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- The Standard C++ Library, included with:
	   - *EDITOR Please do not choose this product*Microsoft Visual C++ 32-bit Edition* use 241, 265, 225, version 4.2 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	The sample code below illustrates how to use the includes STL function in Visual
	C++.
	
	MORE INFORMATION
	================
	
	Required Header
	---------------
	
	     <algorithm>
	
	Prototype
	---------
	
	     template<class InputIterator1, class InputIterator2>
	     inline bool includes(InputIterator1 first1,
	                          InputIterator1 last1,
	                          InputIterator2 first2,
	                          InputIterator2 last2)
	
	NOTE: The class/parameter names in the prototype do not match the original
	version in the header file. Some have been modified to improve readability.
	
	Description
	-----------
	
	The includes algorithm searches for one sequence of values in another sequence of
	values. includes returns true if every element in the range [first2 ..last2) is
	in the sequence [first1 .. last1). This version of includes assumes that both
	the sequences are sorted using operator<.
	
	Sample Code
	-----------
	
	  ////////////////////////////////////////////////////////////////////// 
	  // 
	  // Compile options needed: /GX
	  // 
	  // includesP.cpp : Illustrates how to use the includes function.
	  // 
	  // Functions:
	  // 
	  //    includes - Search for one sequence in another.
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
	  #include <algorithm>
	  #include <functional>
	  #include <string>
	  #include <vector>
	  #include <deque>
	  using namespace std;
	
	  void main()
	  {
	      const int VECTOR_SIZE = 5 ;
	
	      // Define a template class vector of strings
	      typedef vector<string, allocator<string> > StringVector ;
	
	      //Define an iterator for template class vector of strings
	      typedef StringVector::iterator StringVectorIt ;
	
	      // Define a template class deque of strings
	      typedef deque<string, allocator<string> > StringDeque ;
	
	      //Define an iterator for template class deque of strings
	      typedef StringDeque::iterator StringDequeIt ;
	
	      StringVector CartoonVector(VECTOR_SIZE) ;
	      StringDeque CartoonDeque ;
	
	      StringVectorIt start1, end1, it1 ;
	      StringDequeIt start2, end2, it2 ;
	
	      // Initialize vector Vector1
	      CartoonVector[0] = "Aladdin" ;
	      CartoonVector[1] = "Jasmine" ;
	      CartoonVector[2] = "Mickey" ;
	      CartoonVector[3] = "Minnie" ;
	      CartoonVector[4] = "Goofy" ;
	
	      start1 = CartoonVector.begin() ;  // location of first
	                                        // element of CartoonVector
	
	      end1 = CartoonVector.end() ;  // one past the location last
	                                    // element of CartoonVector
	
	      //Initialize list CartoonDeque
	      CartoonDeque.push_back("Jasmine") ;
	      CartoonDeque.push_back("Aladdin") ;
	      CartoonDeque.push_back("Goofy") ;
	
	      start2 = CartoonDeque.begin() ; // location of first
	                                      // element of CartoonDeque
	
	      end2 = CartoonDeque.end() ; // one past the location last
	                                  // element of CartoonDeque
	
	      //sort CartoonVector and CartoonDeque alphabetically
	      //includes requires the sequences
	      //to be sorted.
	      sort(start1, end1) ;
	      sort(start2, end2) ;
	
	      // print contents of CartoonVector and CartoonDeque
	      cout << "CartoonVector { " ;
	      for(it1 = start1; it1 != end1; it1++)
	          cout << *it1 << ", " ;
	      cout << " }\n" << endl ;
	      cout << "CartoonDeque { " ;
	      for(it2 = start2; it2 != end2; it2++)
	          cout << *it2 << ", " ;
	      cout << " }\n" << endl ;
	
	      //Is CartoonDeque a subset of CartoonVector?
	      if(includes(start1, end1, start2, end2) )
	          cout << "CartoonVector includes CartoonDeque"
	          << endl ;
	      else
	          cout << "CartoonVector does not include CartoonDeque"
	          << endl ;
	
	  }
	
	Program Output is:
	
	CartoonVector { Aladdin, Goofy, Jasmine, Mickey, Minnie,  }
	
	CartoonDeque { Aladdin, Goofy, Jasmine,  }
	
	CartoonVector includes CartoonDeque
	
	REFERENCES
	==========
	
	Visual C++ Books On Line: Visual C++ Books:C/C++:Standard C++ Library Reference.
	
	Additional query words: STL includes
	
	======================================================================
	Keywords          : _IK 
	Technology        : kbVCsearch kbAudDeveloper kbVCLibrary
	Version           : winnt:
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
