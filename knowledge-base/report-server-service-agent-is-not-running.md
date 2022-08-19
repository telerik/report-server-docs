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

The Telerik.ReportServer.ServiceAgent is a Windows Service which should be constantly running on the machine where the Report Server is installed. 
It uses WCF to communicate with Report Server and the corresponding settings are configured in its own configuration file *Telerik.ReportServer.ServiceAgent.(x86).exe.config* and Report Server's configuration file *web.config*.
The Report Server maintains the connection with the Service Agent and polls it when a certain event occurs: a Scheduled Task or a Data Alert is added or modified, or the Report Server settings are changed.

## Error Message
When a Scheduled Task or a Data Alert is being added or modified: "**An error occurred while updating the task: Telerik Report Server Service Agent is not running. Please check the Windows service.**".

When the Report Server configuration cannot be saved: "**An error occurred while saving the settings: The changes were not applied!**".


## Cause\Possible Cause(s)

1\. The service is not running.

2\. The server application cannot communicate with the service at the configured port.

## Solution

Telerik Report Server R2 2018 (4.1.18.516) exhibits this issue. It has been fixed in [R2 2018 SP1 (4.1.18.620)](https://www.telerik.com/support/whats-new/report-server/release-history/progress-telerik-report-server-r2-2018-sp1-4-1-18-620). If you are using a different version than 4.1.18.516 and still experience the issue, please follow the steps below.

To make sure that the service is running and that the Report Server application can find the service using the configured address check the following:  
  
1\. Open Windows Task manager and look for Telerik.ReportServer.ServiceAgent service - it should be running.

2\. Open **Telerik.ReportServer.ServiceAgent.exe.config** file located at [installation folder]\\Progress\\Telerik Report Server\\Services and look for the address of the service (baseAddress element). Paste this address in the browser to check if the service is functioning.

3\. Open server's **Web.config** file located at [installation folder]\\Progress\\Telerik Report Server\\Telerik.ReportServer.Web and check if the address of the service matches the address provided in Telerik.ReportServer.ServiceAgent.exe.config.  
  
4\. Enable tracing in the **Telerik.ReportServer.ServiceAgent.exe.config** file, start the service manually, and check the generated log file for errors.

	<configuration>
		...
		<system.diagnostics>
			<trace autoflush="true" indentsize="4">
			  <listeners>
				<add name="myListener" type="System.Diagnostics.TextWriterTraceListener" initializeData="serviceAgent.log" />              
				<remove name="Default" />
			  </listeners>
			</trace>
		</system.diagnostics>
	</configuration>

5\. Enable tracing in the Telerik.ReportServer's **Web.config** file, restart the web application and check the generated log file for errors.

	<configuration>
		...
		<system.diagnostics>
			<trace autoflush="true" indentsize="4">
			  <listeners>
				<add name="myListener" type="System.Diagnostics.TextWriterTraceListener" initializeData="reportServer.log" />              
				<remove name="Default" />
			  </listeners>
			</trace>
		</system.diagnostics>
	</configuration>

6\. The communication layer between the Service Agent and Report Server uses WCF services and by default relies on port 80 for initial client registration. Ensure that the port is currently not used by another application or service. Use the **netstat** command to list the active connections and check if port 80 is available. A common issue is to have a web server (e.g. Apache Tomcat) already using this port. In this case either move the application that occupies port 80 to another port, or change the configuration of the **wsDualHttpBinding** entry in Report Server's web.config file, adding [**clientBaseAddress** attribute](https://docs.microsoft.com/en-us/dotnet/api/system.servicemodel.wsdualhttpbinding.clientbaseaddress?view=netframework-4.8) to the **binding** entry:

````
<system.serviceModel>
    <bindings>
        <wsDualHttpBinding>
            <binding clientBaseAddress="https://reportserver:56436" name="WSDualHttpBinding_IServiceAgentCommService" sendTimeout="00:00:10"/>
        </wsDualHttpBinding>
    </bindings>
	...
</system.serviceModel>	
````
