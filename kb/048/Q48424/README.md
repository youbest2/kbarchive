---
layout: page
title: "Q48424: Mixed-Language Examples for Calling Fortran Are Incorrect"
permalink: /kb/048/Q48424/
---

## Q48424: Mixed-Language Examples for Calling Fortran Are Incorrect

{% raw %}

	Article: Q48424
	Product(s): See article
	Version(s): 5.00 5.10 | 5.10
	Operating System(s): MS-DOS | OS/2
	Keyword(s): ENDUSER | docerr H_MASM S_PasCal | mspl13_c
	Last Modified: 16-JAN-1990
	
	In the "Microsoft Mixed-Language Programmer's Guide" provided with C
	Versions 5.00 and 5.10, MASM Versions 5.00 and 5.10, and Pascal
	Version 4.00, the C and Pascal sample programs for calling a FORTRAN
	subroutine are incorrect. The documentation error appears in two
	different sections of the manual. The documentation error may be found
	in the following locations:
	
	1. Page 40, Section 3.4.1, "Calling FORTRAN from C -- Subroutine Call"
	
	2. Page 67, Section 5.5.1, "Calling FORTRAN from Pascal -- Subroutine
	   Call"
	
	The source code in the manual compiles, but when linked with the
	FORTRAN subroutine, the following error occurs:
	
	   LINK : error L2029: Unresolved externals:
	
	   MAXPAR in file(s):
	    FACT.OBJ(fact.c)
	
	   There was 1 error detected
	
	This error occurs because the FORTRAN subroutine has a different name
	than is used by the calling programs (maxparam instead of maxpar). To
	get the two modules to link correctly, the following changes must be
	made:
	
	In C (Page 40), change
	
	   extern void fortran maxpar (int near *, int near *);
	                .
	                .
	   maxpar (&a, &b);
	
	to the following:
	
	   extern void fortran maxparam (int near *, int near *);
	                .
	                .
	   maxparam (&a, &b);
	
	In Pascal (Page 67), change
	
	   procedure Maxpar (var i,j : integer) ; extern;
	                .
	                .
	   Maxpar (a,b);
	
	to the following:
	
	   procedure Maxparam (var i,j : integer) ; extern;
	                .
	                .
	   Maxparam (a,b);

{% endraw %}
