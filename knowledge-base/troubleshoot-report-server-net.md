---
title: Troubleshooting Report Server for .NET
description: "Learn how to diagnose problems with the Telerik Report Server for .NET web application using logging."
type: troubleshooting
page_title: Debugging Report Server Manager
slug: troubleshoot-report-server-net
res_type: kb
---

## Environment
<table>
	<tr>
		<td>Product</td>
		<td>Progress® Telerik® Report Server for .NET</td>
	</tr>
</table>

## Description

The Report Server for .NET application can stop working for a variety of reasons such as installation failures, user permissions, IIS bindings, corrupted storage, etc. 

By enabling logging, the internal exceptions that are not shown on the browser page can be seen and used to resolve the issue. 

## Solution

1. Ensure that the [ASP.NET Core Module (ANCM)](https://dotnet.microsoft.com/permalink/dotnetcore-current-windows-runtime-bundle-installer) is installed on the machine with the Telerik Report Server for .NET - [Install ASP.NET Core Module (ANCM)](https://learn.microsoft.com/en-us/aspnet/core/host-and-deploy/aspnet-core-module?view=aspnetcore-8.0#install-aspnet-core-module-ancm).
1. Check for any errors in the `Browser Console` or failing requests in the `Network` tab.
1. Use [Fiddler ](https://www.telerik.com/download/fiddler) to see the exact requests from the Report Viewer of the Report Server Manager to the Report Server REST Service, and the corresponding responses - they may indicate what has failed.
1. Enable [ASP.NET Core Module](https://learn.microsoft.com/en-us/aspnet/core/host-and-deploy/aspnet-core-module?view=aspnetcore-8.0) logging in the Report Server for .NET application by editing the `web.config` file in the root directory of the application, e.g. - `C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web.NET`. 

	````XML
<?xml version="1.0" encoding="utf-8"?>
<configuration>
<location path="." inheritInChildApplications="false">
	<system.webServer>
	<handlers>
		<add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
	</handlers>
	<aspNetCore processPath="dotnet" arguments=".\Telerik.ReportServer.Web.Core.dll" stdoutLogEnabled="true" stdoutLogFile=".\logs\stdout" hostingModel="inprocess" >
			<handlerSettings>
			<handlerSetting name="debugFile" value=".\logs\aspnetcore-debug.log" />
			<handlerSetting name="debugLevel" value="FILE,TRACE" />
			</handlerSettings>
	</aspNetCore>
	</system.webServer>
</location>
</configuration>
````


1. Use the [Event Viewer](https://learn.microsoft.com/en-us/shows/inside/event-viewer) to inspect `Application Event Logs` of the Telerik Report Server for .NET application - [Application Event Log (IIS)](https://learn.microsoft.com/en-us/aspnet/core/test/troubleshoot-azure-iis?view=aspnetcore-8.0#application-event-log-iis). The events can be saved into `evtx` files by right-clicking on the events in the Event Viewer -> `Save Selected Events...`.
1 [Run the app at a command prompt](https://learn.microsoft.com/en-us/aspnet/core/test/troubleshoot-azure-iis?view=aspnetcore-8.0#run-the-app-at-a-command-prompt) to catch start-up errors that may not be part of the Application Event log by executing `dotnet Telerik.ReportServer.Web.Core.dll` in the root directory of the Telerik Report Server for .NET - `C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web.NET`. 


>note If the problem persists, you may open a support ticket and send us in an archive (ZIP/RAR file) the [SAZ file](https://docs.telerik.com/fiddler/Save-And-Load-Traffic/Tasks/CreateSAZ) recorded by `Fiddler`, as well as the `.log` and `.evtx` files  Including the steps which have to be followed in order to reproduce the issue may also speed up the diagnostic process.
