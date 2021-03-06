---
layout: page
title: "Q65480: BASIC PDS 7.00 and 7.10 Cannot Use IOCTL and Far Strings"
permalink: /kb/065/Q65480/
---

## Q65480: BASIC PDS 7.00 and 7.10 Cannot Use IOCTL and Far Strings

{% raw %}

	Article: Q65480
	Product(s): See article
	Version(s): m7.00 7.10
	Operating System(s): MS-DOS
	Keyword(s): ENDUSER | SR# S900904-34 | mspl13_basic
	Last Modified: 6-SEP-1990
	
	Some customers have reported that the IOCTL$ function and IOCTL
	statement do not work with far strings (BC /Fs) in Microsoft BASIC
	Professional Development System (PDS) versions 7.00 and 7.10.
	Microsoft has not confirmed this to be a problem.
	
	This information applies to Microsoft BASIC Professional Development
	System (PDS) versions 7.00 and 7.10 for MS-DOS.
	
	The IOCTL$ function and IOCTL statement allow BASIC programs to
	interact with MS-DOS character device drivers that can give and
	receive control data strings. Not all character device drivers support
	IOCTL control data strings. For instance, ANSI.SYS, which replaces the
	standard CON device driver in DOS, is a character device driver, but
	it cannot receive or send control data strings.
	
	For more information on MS-DOS device drivers, device driver classes,
	character device drivers, and how IOCTL works, see "Advanced MS-DOS
	Programming" by Ray Duncan (published by Microsoft Press).
	
	Note that the IOCTL$ function and IOCTL statement cannot be used under
	MS OS/2. You can, however, make equivalent OS/2 API function calls to
	interact with OS/2 character device drivers.

{% endraw %}
