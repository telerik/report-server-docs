---
title: High CPU Processing and High Memory Consumption in Report Server
description: If experiencing High CPU usage or High Memory Consumption use the use these troubleshooting steps to help alleviate it.
type: troubleshooting
page_title: Troubleshooting High CPU Usage and Memory Consumption
slug: troubleshooting-high-cpu-usage-and-memory-consumption
position: 
tags: 
ticketid: 1474172
res_type: kb
---

## Environment

<table>
	<tbody>
		<tr>
			<td>Product Version</td>
			<td>6.1.20.618</td>
		</tr>
		<tr>
			<td>Product</td>
			<td>Progress® Telerik® Report Server</td>
		</tr>
	</tbody>
</table>

## Description

If Report Server crashes due to extreme loads when using the Reporting REST Service with multiple Report Viewer clients. This will cause high cpu usage and memory consumption and happens for a couple of reasons.

The main reason is when report server is processing several consecutive workloads this will increase memory consumption. By default, Report Server runs as a 32-bit application and is limited to using only 2GB of RAM.

Consequentially, once the maximum memory capacity has been reached this will off-load work to the CPU causing the CPU to reach abnormally high usage levels.

## Solution

There are a couple of solutions for these scenarios which are listed below.

1. Confirm the amount of memory assigned to the machine.
   1. If memory consumption has not reached the available memory threshold then the [Report Server application can be changed to a 64-bit process](https://docs.telerik.com/report-server/knowledge-base/start-report-server-as-64bit-app) which will enable Report Server to allocate more than 2GB of memory.
2. If after switching to 64-bit processing the CPU is still too high, then add more report processing workers.
   1. This is the same as adding workers to the [Reporting REST Service](https://docs.telerik.com/reporting/configuring-telerik-reporting-restreportservice).
   2. Use the [Report Engine Configuration](https://docs.telerik.com/report-server/implementer-guide/setup/configure-the-report-engine) included with Report Server.

## Notes

These troubleshooting steps should only be used when a report normally takes a few seconds to process starts processing in a much longer time.

This should not be used in a situation for large reports that have always taken a long time to process. 

For consistent long-running report processing, see the [Performance Considerations](https://docs.telerik.com/reporting/designing-performance).

## See Also

* [Report Server application can be changed to a 64-bit process](https://docs.telerik.com/report-server/knowledge-base/start-report-server-as-64bit-app)
* [Reporting REST Service](https://docs.telerik.com/reporting/configuring-telerik-reporting-restreportservice)
* [Report Engine Configuration](https://docs.telerik.com/report-server/implementer-guide/setup/configure-the-report-engine)
* [Performance Considerations](https://docs.telerik.com/reporting/designing-performance)