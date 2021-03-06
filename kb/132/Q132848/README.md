---
layout: page
title: "Q132848: Dec Venturis PCI or ISAPNP Adapter Problems in Windows 95"
permalink: /kb/132/Q132848/
---

## Q132848: Dec Venturis PCI or ISAPNP Adapter Problems in Windows 95

{% raw %}

	Article: Q132848
	Product(s): Microsoft Windows 95.x Retail Product
	Version(s): 
	Operating System(s): 
	Keyword(s): 
	Last Modified: 17-DEC-2000
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Windows 95 
	-------------------------------------------------------------------------------
	
	SYMPTOMS
	========
	
	After you install Windows 95 on a DEC Venturis computer, you may see the
	following symptoms:
	
	- Device Manager shows a Standard VGA node with a yellow exclamation point (!)
	  indicator.
	
	- Windows 95 does not automatically detect or install any PCI or ISAPNP
	  adapters.
	
	RESOLUTION
	==========
	
	In this case, the Standard VGA node with a yellow exclamation point (!)
	indicator in Device Manager does not cause any Windows problems and can be
	safely ignored.
	
	For the PCI or ISAPNP adapters resolution, contact DEC for an updated Plug and
	Play BIOS that is Windows 95 compatible. Although the exact date and version of
	the corrected Plug and Play BIOS is not known, a BIOS date later than 6/1/95
	should correct the problem.
	
	As an alternate workaround, have Windows 95 recognize and configure PCI and
	ISAPNP devices correctly by manually adding a PCI bus to the system. To do so,
	follow these steps:
	
	1. Click the Start button, point to Settings, and then click Control Panel on
	  the menu that appears.
	
	2. Double-click the Add New Hardware icon.
	
	3. In the Add New Hardware Wizard dialog box, click Next.
	
	4. Under "Do you want Windows to search for your new hardware?" click No, and
	  then click Next.
	
	5. Under Hardware types, click System devices, and then click Next.
	
	6. Under Models, click PCI bus, click Next, and then continue through the Add
	  New Hardware Wizard.
	
	MORE INFORMATION
	================
	
	The DEC Venturis computer is manufactured by Digital Equipment Corporation, a
	vendor independent of Microsoft; we make no warranty, implied or otherwise,
	regarding this product's performance or reliability.
	
	Additional query words: display
	
	======================================================================
	Keywords          :  
	Technology        : kbWin95search kbZNotKeyword3
	
	=============================================================================
	

{% endraw %}
