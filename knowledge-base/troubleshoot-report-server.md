---
title: Troubleshooting Report Server
description: Diagnose problems with the Telerik Report Server application
type: troubleshooting
page_title: Troubleshoot Report Server Manager
slug: troubleshoot-report-server
position: 
tags: 
ticketid: 1400116
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
Sometimes it is possible to experience problems with the Report Server the reasons for which are not apparent. For example, restricted permission for accessing the File Storage, Internal Server Errors due to inaccessible Storage or missing/corrupted report resources (e.g. invalid image), etc.

## Solution
We recommend using the following basic approaches for troubleshooting :
  
1. Check whether there are any errors in the browser console.  

2. Use [Fiddler ](https://www.telerik.com/download/fiddler) to see the exact requests from the Viewer of the Report Server Manager to the Report Server REST Service, and the corresponding responses - they may indicate what has failed.  

3. Attach a [Trace Listener](https://docs.microsoft.com/en-us/dotnet/framework/debug-trace-profile/how-to-create-and-initialize-trace-listeners) to the Report Server. The generated log should contain the entire Stack Trace of the error causing the failure. This can be done in the _Web.config_ file of the Report Server application. By default, it is in the (_Telerik Report Server installation folder_)\\Telerik.ReportServer.Web (e.g. _C:\\Program Files (x86)\\Progress\\Telerik Report Server\\Telerik.ReportServer.Web_). The code for enabling the _Trace Listener_ may look like :  
  
	````XML
<configuration>
		...
		<system.diagnostics>
			<trace autoflush="true" indentsize="4">
			  <listeners>
				<add name="myListener" type="System.Diagnostics.TextWriterTraceListener" initializeData="c:\temp\ReportServer.LOG" />            
				<remove name="Default" />
			  </listeners>
			</trace>
		</system.diagnostics>
		...
	</configuration>
````


4. For issues related to Scheduled Tasks, it's recommended to set up a Trace Listener in Report Server Service Agent configuration file. Please check [Telerik Report Server Service Agent is not running](./report-server-service-agent-is-not-running) KB article for details.

5. Additional information may also be logged in machine's [Windows Events](https://docs.microsoft.com/en-us/windows/desktop/events/windows-events). You may use the [Event Viewer](https://www.howtogeek.com/123646/htg-explains-what-the-windows-event-viewer-is-and-how-you-can-use-it/) to inspect the events logged from __w3wp__ or __serviceAgent__ processes and see if there is any useful information.

If the problem persists, you may open a support ticket and send us in an archive (ZIP/RAR file) the [SAZ file](https://docs.telerik.com/fiddler/Save-And-Load-Traffic/Tasks/CreateSAZ) recorded by _Fiddler_, the log file generated by the _Trace Listeners_ and _Windows Event Viewer_ while experiencing the issue. Including the steps which have to be followed in order to reproduce the issue may speed up the diagnostic process.
