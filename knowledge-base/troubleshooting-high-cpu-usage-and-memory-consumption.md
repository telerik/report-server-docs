---
title: High CPU Processing and High Memory Consumption in Report Server
description: If experiencing High CPU usage or High Memory Consumption use these troubleshooting steps to help alleviate it.
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

If Report Server crashes due to extreme loads when using the Reporting REST Service with multiple Report Viewer clients. This will cause high CPU usage and Memory consumption and happens for a couple of reasons.

The main reason is when report server is processing several consecutive workloads this will increase Memory consumption. By default, Report Server runs as a 32-bit application and is limited to using only 2GB of RAM.

Consequentially, once the maximum Memory capacity has been reached this will off-load work to the CPU causing the CPU to reach abnormally high usage levels.

## Solution

There are a couple of solutions for this scenario which is listed below.

1. Confirm the amount of Memory available to the machine.

	1. If Memory consumption has not reached the available Memory threshold then the [Report Server application can be changed to a 64-bit process]({%slug start-report-server-as-64bit-app%}) which will enable Report Server to allocate more than 2GB of Memory.

2. If after switching to 64-bit processing the CPU is still too high, then add more report processing workers.

	1. This is the same as adding workers to the [Reporting REST Service](https://docs.telerik.com/reporting/doc-output/configure-the-report-engine/restreportservice-element).
	2. Use the [Report Engine Configuration]({%slug configure-the-report-engine%}) included with Report Server.

## Notes

These troubleshooting steps should only be used when report processing begins to take longer than usual and the CPU and Memory resources are noticeably high.

This should not be used in a situation for large reports that have always taken a long time to process.

For consistent long-running report processing, see these [Performance Considerations](https://docs.telerik.com/reporting/designing-reports/performance-considerations).

## See Also

* [Report Server application can be changed to a 64-bit process]({%slug start-report-server-as-64bit-app%})
* [Reporting REST Service](https://docs.telerik.com/reporting/doc-output/configure-the-report-engine/restreportservice-element)
* [Report Engine Configuration]({%slug configure-the-report-engine%})
* [Performance Considerations](https://docs.telerik.com/reporting/designing-reports/performance-considerations)