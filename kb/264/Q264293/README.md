---
layout: page
title: "Q264293: How Streets &amp; Trips 2001 Recognizes Geographic Information"
permalink: /kb/264/Q264293/
---

## Q264293: How Streets &amp; Trips 2001 Recognizes Geographic Information

{% raw %}

	Article: Q264293
	Product(s): Microsoft Automap
	Version(s): 1.0
	Operating System(s): 
	Keyword(s): kbtool kbimu
	Last Modified: 12-NOV-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Streets & Trips 2002, version 1.0 
	- Microsoft Streets and Trips 2001 
	- Microsoft MapPoint 2002 
	- Microsoft MapPoint 2001 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	If you use the Import Data Wizard in Microsoft MapPoint 2001 or Microsoft
	Streets and Trips 2001 to import addresses to a map, the program searches the
	imported data to find any geographic information that can be used to match the
	records to locations on the map.
	
	This article discusses how MapPoint 2001 and Streets & Trips 2001 recognize
	geographic information.
	
	MORE INFORMATION
	================
	
	MapPoint 2001 and Streets & Trips 2001 search the imported data for column
	headings that indicate that the field may contain geographic information, such
	as:
	
	- City
	- Province
	- State
	- Street address
	- ZIP or Postal Code
	
	If the program finds column headings that indicate that the field may contain
	geographic information, the program uses the contents of that field to match
	data to the map.
	
	For example, if a column heading named "City" contains United States city names,
	the program uses the data from that field to position the record in the
	corresponding city on the map. The program then displays the following message:
	
	  Matching records to City in the country/region: United States.
	
	If the program does not find column headings that resemble a geographic area, the
	program searches the imported data for five-digit numbers, number/letter
	combinations, and two-letter sequences.
	
	If the program does not find any data that may correspond to geographic
	information, you cannot position your records on the map unless you choose an
	appropriate heading for each column.
	
	For additional information how to use the Import Data Wizard in Microsoft Streets
	and Trips 2001, click the article number below to view the article in the
	Microsoft Knowledge Base:
	
	  Q264294 Streets and Trips 2001: Information That You Need to Use the Import
	  Data Wizard
	
	Additional query words: st2001 mp2001 importing push pin located header
	
	======================================================================
	Keywords          : kbtool kbimu 
	Technology        : kbHomeProdSearch _IKkbbogus kbExpediaSearch kbMapptSearch kbMapPoint2001 kbExpediaStreets2001 kbExpediaStreets2002 kbMapPoint2002
	Version           : :1.0
	Issue type        : kbinfo
	
	=============================================================================
	

{% endraw %}
