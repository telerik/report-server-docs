---
title: Telerik Report Server Service Agent is not running
description: Telerik Report Server Service Agent is not running error
type: troubleshooting
page_title: Telerik Report Server Service Agent is not running
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

Telerik Report Server R2 2018 (4.1.18.516) exhibits this issue. It has been fixed in [R2 2018 SP1 (4.1.18.620)](https://www.telerik.com/support/whats-new/report-server/release-history/progress-telerik-report-server-r2-2018-sp1-4-1-18-620). If you are using a different version than 4.1.18.516 and still experience the issue, please follow the steps below.

To make sure that the service is running and that the Report Server application can find the service using the configured address check the following:  
  
1\. Open Windows Task manager and look for Telerik.ReportServer.ServiceAgent service - it should be running.

2\. Open Telerik.ReportServer.ServiceAgent.exe.config located at [installation folder]\\Progress\\Telerik Report Server\\Services and look for the address of the service (baseAddress element). Paste this address in the browser to check if the service is functioning.

3\. Open server's Web.config located at [installation folder]\\Progress\\Telerik Report Server\\Telerik.ReportServer.Web and check if the address of the service matches the address provided in Telerik.ReportServer.ServiceAgent.exe.config.  
  
4\. Enable tracing in the Telerik.ReportServer.ServiceAgent.exe.config, start the service manually, and check the generated log file for errors.

	<configuration>
		...
		<system.diagnostics>
			<trace autoflush="true" indentsize="4">
			  <listeners>
				<add name="myListener" type="System.Diagnostics.TextWriterTraceListener" initializeData="c:\temp\ServiceAgent.LOG" />              
				<remove name="Default" />
			  </listeners>
			</trace>
		</system.diagnostics>
	</configuration>
