---
title: Attempt to load Oracle client libraries threw BadImageFormatException
description: BadImageFormatException after Telerik Report Server upgrade
type: troubleshooting
page_title: BadImageFormatException error message
slug: BadImageFormatException-error
position: 
tags: 
ticketid: 1488667
res_type: kb
---

## Environment

<table>
	<tbody>
		<tr>
			<td>Product Version</td>
			<td>6.2.20.916</td>
		</tr>
		<tr>
			<td>Product</td>
			<td>Progress® Telerik® Report Server</td>
		</tr>
	</tbody>
</table>

## Description

A Report runs fine from the web interface of the Report Server. The same report throws the following error when being run on a schedule from the Report Server:

`Attempt to load Oracle client libraries threw BadImageFormatException. This problem will occur when running in 64-bit mode with the 32-bit Oracle client components installed.`

The error occurs after an upgrade to the latest version of the Telerik Report Server software.

## Error Message

`Attempt to load Oracle client libraries threw BadImageFormatException. This problem will occur when running in 64-bit mode with the 32-bit Oracle client components installed.`

## Possible Cause

The Oracle client utilized to connect to the database is 32-bit, whereas the Report Server Service Agent is running in 64-bit mode.

Starting with the [R2 2019 SP1 (5.1.19.618)](https://www.telerik.com/support/whats-new/report-server/release-history/progress-telerik-report-server-r2-2019-sp1-5-1-19-618) release, the Service Agent is indeed running as a 64-bit service by default. We did this change to avoid issues related to insufficient memory. For more information, see [Memory Limits for Windows and Windows Server](https://docs.microsoft.com/en-us/windows/win32/memory/memory-limits-for-windows-releases#physical-memory-limits-windows-10).

## Solution

Configure the Service Agent to run in 32-bit mode. See the [Forcing a .Net Windows service to run as 32-bit on a 64-bit machine](https://stackoverflow.com/questions/1079066/forcing-a-net-windows-service-to-run-as-32-bit-on-a-64-bit-machine) Stackoverflow thread for details.

## See Also

* [BadImageFormatException or Architecture Mismatch message when using ODBC connection]({%slug badimageformatrxception-or-architecture-mismatch-message-when-using-odbc-connection%})