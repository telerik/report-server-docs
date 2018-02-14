---
title: Telerik Report Server Service Agent is not running error when managing reports/tasks/alerts
description: Cannot create/update report/task/alert due to Telerik Report Server Service Agent is not running error
type: troubleshooting
page_title: Telerik Report Server Service Agent is not running error after creating/updating report/task/alert
slug: report-server-service-agent-is-not-running
position: 
tags: tasks,alerts
ticketid: 1142785
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

To perform certain operations, Report Server requires a running instance of Telerik.ReportServer.ServiceAgent service which is a local Windows service.
Such operations can include creating or updating tasks and alerts, updating reports that have tasks and alerts linked to them. 

## Error Message
Telerik Report Server Service Agent is not running. Please check the Windows service.

## Cause\Possible Cause(s)

1\. The service is not running.

2\. The server application cannot communicate with the service at the configured port.

## Solution

To make sure that the service is running and that the Report Server application can find the service using the configured address check the following:  
  
1\. Open Windows Task manager and look for Telerik.ReportServer.ServiceAgent service - it should be running.

2\. Open Telerik.ReportServer.ServiceAgent.exe.config located at [installation folder]\\Progress\\Telerik Report Server\\Services and look for the address of the service (baseAddress element). Paste this address in the browser to check if the service is functioning.

3\. Open server's Web.config located at [installation folder]\\Progress\\Telerik Report Server\\Telerik.ReportServer.Web and check if the address of the service matches the address provided in Telerik.ReportServer.ServiceAgent.exe.config.  
  

