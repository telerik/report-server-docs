---
title: How to enable Trace Listener for Standalone Designer that opens reports from the Report Server
description: Trace logs when opening/editing reports from the Report Server
type: how-to
page_title: Configure Trace Listener for Report Server designer
slug: 
position: 
tags: 
ticketid: 1169769
res_type: kb
---

## Environment
<table>
	<tr>
		<td>Product Version</td>
		<td>4.1 18.516</td>
	</tr>
	<tr>
		<td>Product</td>
		<td>Progress® Telerik® Report Server </td>
	</tr>
</table>


## Description
Sometimes it is necessary to get the Trace Listener log for the **Standalone Designer** that opens reports from the Telerik Report Server. There are two options to get such Trace logs, based on which report designer instance will be used.

## Solution
_**First option**_ :  
By default when the report is opened directly from the Report Server Manager we use the **_ClickOnce_** deployment. An instance of the Standalone Designer is deployed in a folder, which is not explicitly specified, and could change when the report is opened with _ClickOnce_ the next time. Due to this inconsistency we _do **NOT** recommend_ to use this designer for the purpose of error tracing. If you prefer this approach though, here are the necessary steps:  
The _ClickOnce_ install directory is hard to find so while trying to open the report from the server (_Design Reports_ button) invoke the _Windows Task Manager_ (key combination _Ctrl+Shift+Esc_) and open the Standalone Designer location from there (right click on _Telerik Report Designer..._ and select _Open file location_). The location folder looks like _C:\\Users\\**currentUserName**\\AppData\\Local\\Apps\\2.0\\RYEGNMR1.X05\\AAAR4WG1.OO0\\tele...app\_0ec16cac1aa370e1\_000c.0001\_5a5ebd3f2e011654_.  
Save the following config file in the opened folder. Note that the name of the config file should match the designer EXE file, with additional ._config_ at the end, i.e. _Telerik.ReportDesigner.exe.config_.

```XML
<?xml version ="1.0"?>
<configuration>
	<configSections>
	    <section
		name="Telerik.Reporting"
		type="Telerik.Reporting.Configuration.ReportingConfigurationSection, Telerik.Reporting"
		allowLocation="true"
		allowDefinition="Everywhere"/>

	    <section
		name="Telerik.ReportDesigner"
		type="Telerik.ReportDesigner.Configuration.ReportDesignerConfigurationSection, Telerik.ReportDesigner.Configuration"
		allowLocation="true"
		allowDefinition="Everywhere"/>    
	</configSections>

	<startup>
		<supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
	</startup>

	<runtime>
	    	<assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
		      <!--
		      <probing privatePath="path-to-the-assemblies"/>
		      -->
		      <dependentAssembly>
			<!-- Required for interoperability with older versions of Telerik Reporting -->
			<assemblyIdentity name="Telerik.Reporting" culture="neutral" publicKeyToken="a9d7983dfcc261be"/>
			<bindingRedirect oldVersion="0.0.0.0-12.1 18.516" newVersion="12.1 18.516"/>
		      </dependentAssembly>
	    	</assemblyBinding>
	</runtime>

	<connectionStrings>
	    <add name="Telerik.Reporting.Examples.CSharp.Properties.Settings.TelerikConnectionString"
		connectionString="Data Source=(local)\SQLEXPRESS;Initial Catalog=AdventureWorks;Integrated Security=SSPI"
		providerName="System.Data.SqlClient" />
	</connectionStrings>

	<Telerik.ReportDesigner DefaultWorkingDir="Examples">
	</Telerik.ReportDesigner>

	<!-- Add assembly references -->
	<!--
	<Telerik.Reporting>
		<AssemblyReferences>
			<add name="MyFunctions" version="1.0.0.0" />
		</AssemblyReferences>
	</Telerik.Reporting>
	-->


	<system.diagnostics>
		<trace autoflush="true" indentsize="4">
			<listeners>
				<add name="myListener" type="System.Diagnostics.TextWriterTraceListener" initializeData="C:\Temp\Telerik.ReportDesigner.log" />
				<remove name="Default" />
			</listeners>
		</trace>
	</system.diagnostics>

</configuration>
```

The Trace Listener should generate and save a Trace Log file in _C:\\Temp\\Telerik.ReportDesigner.log_ (you can change the file name/folder in the config file).  
  
**_Second option_**:  
If you have _Telerik Reporting_ installed, we _recommend to use_ the Standalone Designer from the Telerik Reporting installation folder. Typically, for example for version _R2 2018_ this will be _C:\\Program Files (x86)\\Progress\\Telerik Reporting R2 2018\\Report Designer_. Enable Trace Listener in the _Telerik.ReportDesigner.exe.config_ (or _Telerik.ReportDesigner.x86.exe.config_) in the same folder, as explained in the [Standalone Report Designer Problems](https://docs.telerik.com/reporting/troubleshooting-standalone-report-designer-problems) article. Open this Standalone Designer and choose to open a report from _Reports Servers_-\>the corresponding server (add it with **Add Server** if necessary).
