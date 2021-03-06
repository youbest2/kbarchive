---
layout: page
title: "Q117682: Returning a Float from Assembly to C"
permalink: /kb/117/Q117682/
---

## Q117682: Returning a Float from Assembly to C

{% raw %}

	Article: Q117682
	Product(s): Microsoft Macro Assembler
	Version(s): 6.0,6.0a,6.1,6.11,6.1a
	Operating System(s): 
	Keyword(s): 
	Last Modified: 06-MAY-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Macro Assembler (MASM), versions 6.0, 6.0a, 6.1, 6.1a, 6.11 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	Returning floating-point values from an assembly module to a C module presents
	certain problems: Small- or medium-model C code expects AX to contain the
	address of a memory location that contains the return value, while compact- or
	large-model C code expects DX:AX to contain the address of this memory location.
	This is explained very briefly in the chapter on mixed-language programming in
	the "MASM Programming Guide," but no examples are provided there. In the "MORE
	INFORMATION" section, below, is sample code that illustrates how to pass and
	return a floating-point value from assembly code to C code.
	
	MORE INFORMATION
	================
	
	The following sample code shows two methods to return a floating-point value
	from assembly code to C code. The first method (function Add1), returns the
	address of a storage location set up by the assembly module. This method is
	fairly straightforward. The sample uses large-model code, so far pointers are
	used. If small- or medium-model code is selected, the segment values are not
	needed.
	
	There is a problem with this technique if the assembly module is contained in a
	Windows DLL. The data segment in the DLL is not accessible by the calling
	program, so returning the address as shown in Add1 does not work. An alternative
	technique (function Add1Again) is also illustrated in the sample code. In this
	method, the calling program passes an address of a floating-point variable, and
	the function places the return data at that address. The sample is intended to
	be built as an MS-DOS program (or a QuickWin), but Add1Again can be used in a
	DLL.
	
	Sample Build
	------------
	
	        rem MAKEFTST.BAT
	        rem Batch program to build the test files
	     cl /c /AL /Od /Zi floatstc.c
	     ml /c /FPi /Zi floatsta.asm
	        rem /FPi allows the MASM module to use the C floating point emulator
	     link /CO floatstc + floatsta;
	        rem Resulting program is FLOATSTC.EXE and can be test in CodeView
	        rem if desired
	
	Sample Code
	-----------
	
	     ;assembly language routines
	     .MODEL LARGE,C
	     .8087
	
	     PUBLIC Add1
	     PUBLIC Add1Again
	
	     .FARDATA
	     temp REAL4 ?    ; temporary storage for return value
	
	     .CODE
	
	         ; procedure to return a float
	     Add1 PROC USES es, y:REAL4
	         ; y is the float passed from C
	     ASSUME ES:SEG temp
	         mov ax, SEG temp
	         mov es, ax          ; load the far data segment
	         fld DWORD PTR y     ; load the coprocessor
	         fld1
	         faddp ST(1),ST      ; add 1 to the value passed in
	         fstp DWORD PTR es:temp  ; store the value to temporary storage
	         mov dx, SEG temp        ; load DX:AX with the address of temp
	         mov ax, OFFSET temp
	             ; this is what the C module expects as a return value
	         ret
	     Add1 ENDP
	
	         ; procedure to do the same things
	         ; but return a value at the passed address
	     Add1Again PROC USES es bx, y:REAL4, z:DWORD
	         ; y is the float passed from C
	         ;z is the address of a float in the C module
	     ASSUME ES:NOTHING
	         les bx, z       ; load ES:BX with the address of the return location
	         fld DWORD PTR y
	         fld1
	         faddp st(1),st
	         fstp DWORD PTR es:[bx]
	             ; store the final value to the C modules data area
	         ret
	     Add1Again ENDP
	
	     END
	
	  /****************************************
	   * C module to test the assembly routines
	   ****************************************/ 
	
	     #include <stdio.h>
	
	     float Add1(float i);
	     void Add1Again(float i, float *j);
	
	     float p = 10;
	     float y = 0;
	     float z = 0;
	
	     void main()
	     {
	         y = Add1(p);
	         printf("p = %f\t\ty = %f\n",p,y);
	         Add1Again(p, &z);
	         printf("p = %f\t\tz = %f\n",p,z);
	     }
	
	REFERENCES
	==========
	
	For additional information on returning floating-point values from a DLL, please
	see the following article in the Microsoft Knowledge Base:
	
	  Q86081 PRB: DLL Function Returns Float or Double Value Incorrectly
	
	Additional query words: kbinf 6.00 6.00a 6.10 6.10a s_c
	
	======================================================================
	Keywords          :  
	Technology        : kbMASMsearch kbAudDeveloper kbMASM600 kbMASM610 kbMASM611 kbMASM610a kbMASM600a
	Version           : :6.0,6.0a,6.1,6.11,6.1a
	
	=============================================================================
	

{% endraw %}
