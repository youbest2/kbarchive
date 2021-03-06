---
layout: page
title: "Q224967: How to Create File Shares on a Cluster"
permalink: /kb/224/Q224967/
---

## Q224967: How to Create File Shares on a Cluster

{% raw %}

	Article: Q224967
	Product(s): Microsoft Windows NT
	Version(s): 2000,4.0
	Operating System(s): 
	Keyword(s): kbenv diskmem kbDiskMemory
	Last Modified: 22-AUG-2001
	
	-------------------------------------------------------------------------------
	The information in this article applies to:
	
	- Microsoft Cluster Server, included with:
	   - Microsoft Windows NT Server, Enterprise Edition version 4.0 
	- Microsoft Windows 2000 Advanced Server 
	- Microsoft Windows 2000 Datacenter Server 
	-------------------------------------------------------------------------------
	
	SUMMARY
	=======
	
	To create highly available file shares on a cluster, you should create them
	using either Cluster Administrator (CluAdmin.exe) or the cluster API set. When
	the share is placed in a group with other related resources (IP Address, Network
	Name, and a storage device), the share is available from whichever node in the
	cluster owns the group of resources. This article lists basic steps for creating
	a basic File Share resource.
	
	MORE INFORMATION
	================
	
	To create a file share on a server cluster, follow these steps:
	
	1. Open Windows Explorer and create a folder on a shared disk that you want to
	  share out for users.
	
	2. Assign the appropriate NTFS file level permissions on the folder. Make sure
	  that the account used to start the Cluster Service has at least READ rights
	  to the folder.
	
	  NOTE: Do not share the folder in Windows Explorer as you normally would for a
	  file share. If you do not grant the Cluster account the appropriate
	  permissions or share the folder through Windows Explorer, it may cause the
	  cluster file share to fail. This also includes any administrative shares that
	  already exist, you do not want to create shares for the root of the drive
	  (Q$) for example.
	
	3. Start Cluster Administrator (CluAdmin.exe).
	
	4. Select a group that has an existing IP Address and Network Name resources. If
	  you do not have these resources created, you will need to complete this
	  before continuing. Please reference this article for additional information:
	
	  Q257932 Using Microsoft Cluster Server to Create a Virtual Server
	
	5. Right-click, and select New, then Resource.
	
	6. Fill in an administrative name and description for the resource. From the
	  Resource Type pull down, select "File Share", click Next.
	
	  NOTE: This is the name that will be displayed in Cluster Administrator and is
	  only used for administrative purposes. This is not the share name that users
	  will connect to, give the resource a name that will be easy to identify and
	  manage.
	
	7. Select the nodes that you want to be possible owners of the resource. Click
	  Next to leave all nodes as possible owners.
	
	  NOTE: Possible Owners defines whether a resource is ever able to failover to a
	  specific node. Use extreme caution in defining Possible Owners because
	  defining a possible owner for a single resource will effect the failover for
	  the entire group.
	
	8. Select a Network Name and Physical Disk resource that the file share will be
	  dependent on.
	
	  NOTE: Dependencies serve two functions.
	
	  a. They define the bindings for a resource. You want the file share to be
	  dependent on the Network Name resource that clients are going to use when
	  connecting to the file share. The IP Address resource that the Network Name
	  resource is dependent upon is the IP Address that will be used when
	  connecting to this share. You never want a file share resource to be
	  dependent on the "Cluster Name" resource.
	
	  b. They define the start order for a resource. You want to make sure that the
	  network name that the share is going to be created under and the physical
	  disk where the folder resides that is going to be shared are online and
	  available before attempting to bring the File Share online.
	
	  When creating a dependency 'Tree' it is best to keep it as simple as possible.
	  A file share resource should always be dependent on a Network Name that the
	  clients will use to connect to this share and Physical disk resource where
	  the folder is located. The Physical Disk resource should never be dependent
	  on anything. The Network Name resource should be dependent on a IP Address
	  resource which the virtual server will be associated with. The IP Address
	  resource should not be dependent on anything. See the following article for
	  additional information:
	
	  
	
	  Q171791 Creating Dependencies in Microsoft Cluster Server
	
	9. On the File Share Parameters screen fill in the following information and
	  click Finish:
	
	  a. The "Share Name" is the name of the share that will be created for the UNC
	  when clients connect. This needs to be a valid NetBIOS name, and is
	  recommended to be a valid URL name as well.
	
	  b. The "Path" is the full path on the local node to the shared disk where the
	  folder is located. For example: T:\Users.
	
	  c. The "Comment" is the information about the share that will appear when a
	  client browses the share.
	
	1. The 'User Limit' dialog can be used to limit the number of simultaneous
	  users.
	
	2. Click the "Permissions" button to set share level permissions. Only domain
	  level groups should be used in defining share level permissions because local
	  groups and user accounts do not reside on the other node, and the permissions
	  will not take effect when the file share is failed over. The only exception
	  to this is if all nodes in the cluster are domain controllers. It is
	  recommended to use NTFS permissions instead of share level permissions on a
	  server cluster.
	
	3. The 'Advanced' dialog can be used to create a Dynamic file share or a DFS
	  Root, see the following articles for more information:
	
	  
	
	  Q256926 Implementing Home Folders on a Server Cluster
	
	  Q220819 How to Configure Dfs Root on a Windows 2000 Server Cluster
	
	  NOTE: The advanced button was a new feature added in Windows NT 4.0 service
	  pack 4. If you are running NT4 and the advanced button is not present,
	  reapply SP4 or higher.
	
	
	When browsing the file share, file shares for other virtual servers on the same
	cluster may be visible. Reference the following article for additional
	information.
	
	  Q170762 Cluster Shares Appear in Browse List under Other Names
	
	If you are going to create a large number of file share resources, it may be
	easier to script the creation using Cluster.exe. See the following article for
	additional information:
	
	  Q284838 How to Create a Server Cluster File Share with Cluster.exe
	
	Additional query words: mscs
	
	======================================================================
	Keywords          : kbenv diskmem kbDiskMemory 
	Technology        : kbAudDeveloper kbClustServSearch
	Version           : :2000,4.0
	Issue type        : kbhowto
	
	=============================================================================
	

{% endraw %}
