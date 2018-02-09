---
title: Error Cannot read a document with the specified schema
description: Error Cannot read a document with the specified schema when previewing report in Report Server
type: troubleshooting
page_title: Error Cannot read a document with the specified schema
slug: cannot-read-document-with-the-specified-schema
position: 
tags: version
ticketid: 1148469
res_type: kb
---

## Environment
<table>
	<tr>
		<td>Product</td>
		<td>Progress® Telerik® Report Server</td>
	</tr>
</table>


## Description

After publishing a report to Report Server and previewing it, there is an error displayed in the viewer: "Cannot read a document with the specified schema"

## Error Message
Cannot read a document with the specified schema

## Solution
This error is caused by the mismatch in Telerik Reporting versions, report that is created or modified with a newer version cannot be processed by the older version. When you modify the report in Standalone designer of the newer version, the [XML schema of the report](https://docs.telerik.com/reporting/upgrading-xml-report-definition-versioning) will be updated. Reporting engine of the older version is not able to read the updated schema and will show the mentioned error.  
  
To avoid issues caused by the version mismatch when using both Telerik Reporting and Report Server products it is recommended: 
  
1\. To have Telerik Reporting and Report Server of the same version on the machine. If you have upgraded Telerik Reporting to the latest version consider upgrading Report Server as well.  
2\. Create and modify reports with Standalone designer that is shipped with Report Server, this way you can be sure that version of designer and Report Server is the same. The designer can be found in product installation folder: C:\\Program Files (x86)\\Progress\\Telerik Report Server\\Telerik.ReportServer.Web\\Report Designer. 

## See Also

[XML Report Definition](https://docs.telerik.com/reporting/upgrading-xml-report-definition-versioning)

