---
layout: page
title: "Q77256: SAMPLE: MASMWin.exe Uses MASM 6.0 to Write Windows Application"
permalink: /kb/077/Q77256/
---

## Q77256: SAMPLE: MASMWin.exe Uses MASM 6.0 to Write Windows Application

{% raw %}

	Article: Q77256
	Product(s): Microsoft Macro Assembler
	Version(s): 
	Operating System(s): 
	Keyword(s): kbfile kbsample
	Last Modified: 04-DEC-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows Software Development Kit (SDK) for Windows 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	MASMWin.exe is a sample that demonstrates how to write a complete Windows
	program using MASM 6.0. Using the high-level language features of the Microsoft
	Macro Assembler (MASM) version 6.0, it is now much simpler to write a complete
	Windows program in MASM than with previous versions of the program.
	
	MORE INFORMATION
	================
	
	The following file is available for download from the Microsoft Download
	Center:
	
	  MASMWin.exe
	  (http://download.microsoft.com/download/platformsdk/sample34/1/W31/EN-US/MASMWin.exe)
	
	For additional information about how to download Microsoft Support files, click
	the article number below to view the article in the Microsoft Knowledge Base:
	
	  Q119591 How to Obtain Microsoft Support Files from Online Services
	
	Microsoft used the most current virus detection software available on the date of
	posting to scan this file for viruses. Once posted, the file is housed on secure
	servers that prevent any unauthorized changes to the file.
	
	MASMWIN demonstrates a number of features of MASM 6.0. It demonstrates the use of
	alternate PROLOGUE and EPILOGUE code generation. It also demonstrates function
	prototyping and the use of the INVOKE feature.
	
	While MASM provides a complete programming environment with high-level language
	features, applications written in MASM will be much more difficult to transfer
	to future versions of Windows that run on non- Intel platforms.
	
	Using the OPTION:PROLOGUE and OPTION:EPILOGUE directives in MASM 6.0, an
	application can cause MASM 6.0 to generate any type of prologue or epilogue code
	desired. For this program, it creates the appropriate Windows code. The macros
	to perform this task are contained in the file WINPRO.INC. The two declarations,
	?WINDOWS=1 and ?PMODE=1, affect the generation of the prologue and epilogue
	code.
	
	The ?WINDOWS=1 declaration will cause Windows prologue and epilogue code to be
	generated for all FAR functions. All other functions are declared with the
	normal function stack frame.
	
	The ?PMODE=1 declaration causes the Windows prologue and epilogue code to be
	generated only for FAR functions declared as EXPORT. This code takes advantage
	of the fact that in protected mode, Windows does not walk the stack.
	
	The program includes a WINDOWS.INC file that is different from the one included
	in Windows Software Development Kit (SDK) version 3.0. This WINDOWS.INC file was
	created by running WINDOWS.H through the H2INC utility provided with MASM 6.0.
	This provides prototypes for all of the Windows functions and also translates C
	structures to corresponding MASM structures. This file allows the INVOKE feature
	of MASM 6.0 to be used to call Windows functions. The INVOKE function handles
	all the parameter passing and stack clean up. To use this file, it is necessary
	to include the following line in the source code before the line that includes
	the new WINDOWS.INC:
	
	  OPTION CASEMAP:NONE
	
	This causes the assembler to maintain case sensitivity when dealing with symbols.
	
	Additional query words:
	
	======================================================================
	Keywords          : kbfile kbsample 
	Technology        : kbAudDeveloper kbSDKSearch kbWinSDKSearch
	Version           : :
	
	=============================================================================
	

{% endraw %}
