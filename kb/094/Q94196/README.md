---
layout: page
title: "Q94196: Reinstalling Windows Without Losing Settings"
permalink: /kb/094/Q94196/
---

## Q94196: Reinstalling Windows Without Losing Settings

{% raw %}

	Article: Q94196
	Product(s): Microsoft Windows 3.x Retail Product
	Version(s): WINDOWS:3.1,3.11
	Operating System(s): 
	Keyword(s): 
	Last Modified: 29-OCT-1999
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows versions 3.1, 3.11 
	-------------------------------------------------------------------------------
	
	
	SUMMARY
	=======
	
	There may be situations in which you need to reinstall Microsoft Windows to
	troubleshoot a problem possibly related to file corruption or accidental
	deletion of files from the Windows directory or the Windows SYSTEM subdirectory.
	In most cases, it is not advisable to simply reinstall over an existing Windows
	installation because with that procedure, some files may not be properly
	updated.
	
	Installing Windows to a new directory ensures a "clean" installation; however,
	any modifications to Windows initialization (.INI) files or the registration
	database (REG.DAT) are lost with such an installation. Also, programs that
	install files into the Windows directory, such as Microsoft Word for Windows and
	Microsoft Excel, cannot run from the new copy of Windows. Any Windows-based
	applications must be reinstalled under the new installation of Windows.
	Furthermore, any customization of Program Manager groups, desktop colors and
	wallpaper, screen-saver settings, and other user-defined environment settings
	must be re-created.
	
	MORE INFORMATION
	================
	
	Use the following steps to reinstall Windows 3.1 without losing current
	settings, such as .INI and REG.DAT file modifications, customized Program
	Manager groups (.GRPs), and other desktop settings.
	
	1. Install Windows into a new directory, such as C:\WIN. Verify that Windows
	  runs from this new directory.
	
	  If Windows ran during installation but does not run from this new directory,
	  something has changed on the computer, or file corruption has occurred since
	  Windows was installed. The following causes should be considered:
	
	   - Changes to the path
	
	   - Deletion of files from the Windows directory
	
	   - Low conventional memory
	
	   - File corruption
	
	   - Hardware failures
	
	2. In this new installation, rename the .GRP files using .GRN, the .INI files
	  using .INN, and the .FOT files (located in the Windows SYSTEM subdirectory)
	  using .FOZ. Rename the REG.DAT file using REG.DAN. To do this, quit Windows
	  and type the following commands at an MS-DOS command prompt:
	
	  rename c:\win\*.grp *.grn
	  rename c:\win\*.ini *.inn
	  rename c:\win\reg.dat reg.dan
	  rename c:\win\system\*.fot *.foz
	
	  NOTE: The *.FOT files have an internal direct path to the *.TTF files, which
	  if copied to the old C:\WINDOWS\SYSTEM subdirectory, can create problems with
	  the fonts after the C:\WIN directory is removed.
	
	3. Remove the Read-Only attribute from any files in the C:\WINDOWS and
	  C:\WINDOWS\SYSTEM directories. Copy all the files from the new installation
	  into the original Windows directory (C:\WINDOWS) by typing the following at
	  an MS-DOS command prompt:
	
	  attrib -s -h c:\windows\*.* /s
	  attrib -r c:\windows\*.* /s
	  xcopy c:\win c:\windows /s
	
	  If Windows now runs from the C:\WINDOWS directory, the reinstallation has been
	  successful, and no settings were lost. To save disk space, delete the C:\WIN
	  directory from File Manager or from MS-DOS version 6.0 or later using the
	  DELTREE command. Also, delete files with the extensions .INN, .GRN, and the
	  file REG.DAN in the C:\WINDOWS directory, and the files ending with .FOZ in
	  the C:WINDOWS\SYSTEM subdirectory.
	
	  If Windows does not run, continue with the following steps.
	
	4. Rename the original .INI files using .INO, and rename the .INN files using
	  .INI as follows:
	
	  rename c:\windows\*.ini *.ino
	  rename c:\windows\*.inn *.ini
	
	  Edit the PROGMAN.INI file and replace all occurrences of C:\WIN with
	  C:\WINDOWS.
	
	  If Windows runs now, the problem is being caused by a corruption or improper
	  setting in one of the original .INI files. The best solution is to back up
	  all data files from Windows-based applications and then reinstall the
	  applications. This ensures the correct WIN.INI, SYSTEM.INI, and directory
	  settings for each application. Note that you must re-create any customization
	  of Program Manager groups and desktop settings.
	
	  To free up disk space, delete excess files as shown in step 3 above.
	
	5. If Windows does not run now, back up all application data files and reinstall
	  the applications under the new Windows installation after renaming the .INN,
	  .GRN, .FOZ, and REG.DAN files as follows:
	
	  rename c:\win\*.inn *.ini
	  rename c:\win\*.grn *.grp
	  rename c:\win\reg.dan reg.dat
	  rename c:\win\system\*.foz *.fot
	
	REFERENCES
	==========
	
	"Microsoft Windows Resource Kit," version 3.1, Chart 1.6, "Reinstalling Windows
	Without Losing Settings," page 15
	
	"Getting Started With Microsoft Windows," version 3.1, Chapter 1, "Setting Up
	Windows," pages 1-15
	
	Additional query words: tshoot how to preserve 3.10 restore recover reinstall re-install save setup install rebuild
	
	======================================================================
	Keywords          :  
	Technology        : kbWin3xSearch kbZNotKeyword3 kbWin310 kbWin311
	Version           : WINDOWS:3.1,3.11
	
	=============================================================================
	

{% endraw %}
