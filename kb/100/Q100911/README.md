---
layout: page
title: "Q100911: MS-DOS Err Msg with DoubleSpace: Insufficient Disk Space"
permalink: /kb/100/Q100911/
---

## Q100911: MS-DOS Err Msg with DoubleSpace: Insufficient Disk Space

{% raw %}

	Article: Q100911
	Product(s): Microsoft Disk Operating System
	Version(s): MS-DOS:6.0,6.2,6.21,6.22
	Operating System(s): 
	Keyword(s): msdos
	Last Modified: 02-JUN-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft MS-DOS operating system versions 6.0, 6.2, 6.21, 6.22 
	-------------------------------------------------------------------------------
	
	
	
	This information applies to both Microsoft DoubleSpace and Microsoft
	DriveSpace. For MS-DOS 6.22, use DRVSPACE in place of DBLSPACE for
	commands and filenames.
	
	SUMMARY
	=======
	
	When you copy or create files on a DoubleSpace-compressed drive, it is possible
	to receive an "Insufficient Disk Space" error message when MS-DOS reports
	sufficient space to perform the operation. This article discusses potential
	causes of this problem and workarounds.
	
	MORE INFORMATION
	================
	
	There are several instances, including those listed below, in which MS-DOS may
	report insufficient disk space when copying files to a compressed drive.
	
	- The estimated compression ratio (ECR) is lower than the actual compression
	  ratio (ACR) for the files to be copied. In this case, MS-DOS underestimates
	  the space available. To correct this problem, set the ECR equal to the ACR
	  for the drive as follows:
	
	  1. Start DoubleSpace by typing "dblspace" (without the quotation marks) at
	     the MS-DOS command prompt.
	
	  2. Select the compressed drive you want to change and then choose the Change
	     Ratio command from the Drive menu.
	
	     The Change Compression Ratio dialog box appears.
	
	  3. The default ratio is the ACR. Choose OK.
	
	     You can also change the ECR from the MS-DOS command prompt. For more
	     information, type "help dblspace /ratio" (without the quotation marks) at
	     the MS-DOS command prompt.
	
	     NOTE: The above procedure causes MS-DOS to estimate free disk space more
	     accurately and may also increase the number of FAT entries available. If
	     the files to be copied are highly compressible, then you may need to make
	     the ECR higher than the current ACR.
	
	- The ECR is higher than the ACR for the files to be copied. In this case,
	  MS-DOS overestimates the space available, and you must either delete files or
	  enlarge the drive to free space. To enlarge the compressed drive, use the
	  following steps:
	
	  1. Start DoubleSpace by typing "dblspace" (without the quotation marks) at
	     the MS-DOS command prompt.
	
	  2. Select the compressed drive you want to enlarge, then choose the Change
	     Size command from the Drive menu.
	
	     The Change Size dialog box appears. The New Free Space line shows how much
	     free space the compressed and uncompressed drives will have if you choose
	     OK.
	
	  3. Specify a smaller number for New Free Space on the uncompressed drive. As
	     you change this number, DoubleSpace adjusts the New Free Space amount for
	     the compressed drive. When the New Free Space amount for both drives is
	     what you want, choose OK.
	
	     DoubleSpace enlarges the compressed drive.
	
	     NOTE: The above procedure decreases the free space on the uncompressed
	     (host) drive.
	
	- The DoubleSpace drive is too fragmented. To correct this problem, use the
	  commands DBLSPACE /DEFRAG /F and DBLSPACE /DEFRAG on the compressed drive as
	  follows:
	
	  NOTE: You may want to perform this procedure overnight. Defragmenting a large
	  or badly fragmented drive can take a long time. (To defragment overnight, put
	  both commands into a batch file.)
	
	  1. Make the compressed drive your current drive.
	
	  2. Type "dblspace /defrag /f" (without the quotation marks) at the MS-DOS
	     command prompt.
	
	     DoubleSpace defragments the drive.
	
	  3. When DoubleSpace finishes, type "dblspace /defrag" (without the quotation
	     marks) at the MS-DOS command prompt.
	
	  DoubleSpace consolidates free space on the drive to leave as much free space
	  as possible.
	
	- No more FAT entries are available. To correct this problem, split the host
	  drive into more compressed drives as follows:
	
	  If the data on a compressed drive is reaching the 512-megabyte limit, reduce
	  the size of the drive and then use the Create New command on the Compress
	  menu to create a new drive from free space on the drive.
	
	
	- Finally, certain programs or files may cause the "Insufficient Disk Space"
	  message or may fail when they are installed on a DoubleSpace- compressed
	  drive because their ACR is close to 1:1. These include the following:
	
	   - Many games by Sierra On-Line (also marketed as Dynamix or Coktel)
	
	   - Microsoft Mail Format (.MMF) files
	
	   - Encrypted data files
	
	   - Precompressed files (such as .ARC, .ZIP, .PCX, and .GIF files)
	
	  Move highly compressible files to the compressed drives and leave files that
	  compress poorly on uncompressed drives.
	
	
	For more information on the ECR, ACR, and the space available on a
	DoubleSpace-compressed drive, see page 125 in the "User's Guide."
	
	The products included here are manufactured by vendors independent of Microsoft;
	we make no warranty, implied or otherwise, regarding these products' performance
	or reliability.
	
	REFERENCES
	==========
	
	"Microsoft MS-DOS User's Guide" for version 6 and 6.2, pages 125-126
	
	README.TXT, Section 7.3
	
	
	Additional query words: tshoot 6.00 6.20 6.21 6.22 dblspace
	
	======================================================================
	Keywords          : msdos 
	Technology        : kbMSDOSSearch kbMSDOS621 kbMSDOS622 kbMSDOS620 kbMSDOS600
	Version           : MS-DOS:6.0,6.2,6.21,6.22
	
	=============================================================================
	

{% endraw %}
