---
layout: page
title: "Q67783: C1001: Internal Compiler Error: regMD.c, Lines 4634 and 4688"
permalink: /kb/067/Q67783/
---

## Q67783: C1001: Internal Compiler Error: regMD.c, Lines 4634 and 4688

{% raw %}

	Article: Q67783
	Product(s): See article
	Version(s): 6.00 6.00a | 6.00 6.00a
	Operating System(s): MS-DOS | OS/2
	Keyword(s): ENDUSER | buglist6.00 buglist6.00a | mspl13_c
	Last Modified: 6-FEB-1991
	
	When compiled with /Oe and /MD, the sample code generates an internal
	compiler error for Microsoft C Compiler versions 6.00 and C 6.00a. The
	errors are different for each version.
	
	Under C 6.00
	------------
	
	   fatal error c1001: Internal Compiler Error
	   (compiler file '@(#)regMD.c:1.110',line 4634)
	
	Under C 6.00a
	-------------
	
	   fatal error c1001: Internal Compiler Error
	   (compiler file '@(#)regMD.c:1.110',line 4688)
	
	Sample Code
	-----------
	
	char wi_lines(char);
	
	int w_hline(char *pnt)
	{
	   int x;
	   for (x=0;x<=10;x++)
	   pnt[x]=wi_lines(pnt[x]);
	}

{% endraw %}
