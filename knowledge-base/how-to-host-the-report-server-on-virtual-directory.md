---
title: Hotsting the Report Server on a Virtual Directory
description: Explains how to host the Report Server on a virtual directory in IIS
type: how-to
page_title: How to Host the Report Server on Virtual Directory in IIS
slug: how-to-host-the-report-server-on-virtual-directory
position: 
tags: 
ticketid: 1533027
res_type: kb
---

## Environment
<table>
	<tbody>
		<tr>
			<td>Product</td>
			<td>Progress® Telerik® Report Server</td>
		</tr>
    <tr>
			<td>IIS version</td>
			<td>10</td>
		</tr>
	</tbody>
</table>


## Description
In some scenarios, to make the Report Server resources working, you need to host the Report Server on a virtual directory in the IIS.

## Solution
Below are the required steps:
1. Open the IIS;
2. Under **Connections** -> **Sites** -> right-click over the site ->** Add Virtual Directory**;
3. In **Alias**, type **reporting**;
4. **Phisical path** should point to **Telerik.ReportServer.Web** folder of the Report Server.
5. Right-click over the virtual directory -> **Convert to application**. 


## See Also
You can also [download this video](resources/UploadingReportServerToVirtualDirectory.zip) that demonstrates the steps.
