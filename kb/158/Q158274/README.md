---
layout: page
title: "Q158274: Automap/Expedia Err Msg: Couldn't Find &lt;Program Name&gt; CD-ROM"
permalink: /kb/158/Q158274/
---

## Q158274: Automap/Expedia Err Msg: Couldn't Find &lt;Program Name&gt; CD-ROM

{% raw %}

	Article: Q158274
	Product(s): Microsoft Automap
	Version(s): WINDOWS:5.0
	Operating System(s): 
	Keyword(s): kbenv kberrmsg kbimukbfaq
	Last Modified: 06-AUG-2002
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Automap Streets Plus for Windows, version 5.0 
	- Microsoft Automap Trip Planner for Windows, version 5.0 
	- Microsoft Expedia Streets 98 
	- Microsoft Expedia Trip Planner 98 
	- Microsoft Expedia Streets and Trips 2000 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	When you attempt to start one of the programs listed at the beginning of this
	article, you may receive an error message similar to one of the following:
	
	   - <Program Name>
	
	  Couldn't find the <Program Name> CD-ROM on this machine. Ensure that the
	  CD is correctly inserted in your CD-ROM drive, then click OK (or click Cancel
	  to terminate the program).
	
	   - Microsoft Expedia Streets & Trips 2000
	
	  Couldn't find the Microsoft Expedia Streets & Trips 2000 RUN CD-ROM on
	  this machine. Ensure that the RUN CD (not the SETUP CD) is correctly inserted
	  in your CD-ROM drive, then click OK (or click
	  Cancel to exit the application).
	
	CAUSE
	=====
	
	This behavior can occur if any of the following conditions is true:
	
	- You are using the PowerToys FlexiCD program.
	
	- Your MCI CD Audio device driver is not installed or enabled.
	
	- You are attempting to run the program over a Terminal Server connection.
	
	RESOLUTION
	==========
	
	To resolve this issue, use one of the following methods.
	
	Disable PowerToys FlexiCD
	-------------------------
	
	1. Right-click the FlexiCD icon (a compact disk), located next to the clock on
	  the Windows taskbar.
	
	2. On the FlexiCD menu, click Exit FlexiCD.
	
	3. Restart the program.
	
	Make Sure the MCI CD Audio Device Is Installed and Enabled
	----------------------------------------------------------
	
	To make sure the MCI CD Audio device is installed and enabled, follow these
	steps:
	
	1. Click Start, point to Settings, and then click Control Panel.
	
	2. Double-click Multimedia.
	
	3. Click the Advanced or Devices tab.
	
	4. Click the PLUS SIGN (+) next to Media Control Devices to expand the branch.
	
	5. Click CD Audio Device (Media Control), and then click the Properties.
	
	  NOTE: If CD Audio Device (Media Control) is not listed, skip to the "Install
	  the CD Audio Device" section later in this article.
	
	6. Click Use This Media Control Device, and then click OK.
	
	7. Close Control Panel, and then restart Windows.
	
	If the CD Audio Device is installed and enabled but you still receive the error
	message, you must remove and reinstall the CD Audio Device.
	
	NOTE: If a CD-ROM changer is installed in your computer, the drive you assign to
	play music compact discs (CD Audio), must also be the drive you use for any of
	the programs listed at the beginnng of this article.
	
	Remove the CD Audio Device
	--------------------------
	
	1. Click Start, point to Settings, and then click Control Panel.
	
	2. Double-click Multimedia.
	
	3. Click the Advanced or Devices tab.
	
	4. Click the PLUS SIGN (+) next to Media Control Devices to expand the branch.
	
	5. Click CD Audio Device (Media Control), and then click the Properties.
	
	  NOTE: If CD Audio Device (Media Control) is not listed, skip to the "Install
	  the CD Audio Device" section later in this article.
	
	6. Click Remove, and then click OK.
	
	7. Close Control Panel.
	
	8. Click Start, point to Find, and then click "Files or Folders".
	
	9. In the Named box, type "mcicda.drv" (without the quotation marks).
	
	10. In the "Look in" box, click My Computer, and then click Find Now.
	
	11. In the list of found files, right-click the Mcicda.drv file, and then click
	  Delete.
	
	12. When you are prompted to confirm the file deletion, click Yes.
	
	13. Close the Find: Files Named Mcicda.drv window, and then restart the
	  computer.
	
	Install The CD Audio Device
	---------------------------
	
	1. Click Start, point to Settings, and then click Control Panel.
	
	2. Double-click Add New Hardware.
	
	3. Click Next, click No, and then click Next.
	
	  NOTE: If you are using a Microsoft Windows 98-based computer, click Next.
	
	  If Windows detects new hardware, click "No, the device isn't in the list," and
	  then click Next. If Windows does not detect any devices, click No, and then
	  click Next.
	
	4. Click Sound, Video And Game Controllers, and then click Next.
	
	5. In the Manufacturers list, click Microsoft MCI.
	
	6. In the Models list, click CD Audio Device (Media Control).
	
	7. Click Next, and then click Finish. Follow the instructions on the screen.
	
	8. Restart Windows.
	
	Run the Program Locally
	-----------------------
	
	The MCI CD Audio device is not available across a Terminal Server connection.
	Because of this, you cannot run the programs listed on the beginning of this
	article across a Terminal Server connection. To run one of these programs,
	install and run it locally on your computer.
	
	STATUS
	======
	
	Microsoft has confirmed that this is a problem in the Microsoft products that
	are listed at the beginning of this article.
	
	MORE INFORMATION
	================
	
	The programs listed at the beginning of this article need to obtain exclusive
	control of your CD-ROM drive. If the program cannot obtain exclusive control of
	your CD-ROM drive, you receive an error message similar to the messages
	specified in the "Symptoms" section of this article.
	
	Additional query words: 5.00 multi multi-media media mm auto-map amap mcicda.drv cdplayer
	
	======================================================================
	Keywords          : kbenv kberrmsg kbimu kbfaq
	Technology        : kbHomeProdSearch kbHomeMMsearch kbAutomapSearch kbExpediaSearch kbAutomapStreetsPlus500 kbAutomapTripPlanner500 kbExpediaStreets2000
	Version           : WINDOWS:5.0
	Issue type        : kbbug
	Solution Type     : kbpending
	
	=============================================================================
	

{% endraw %}
