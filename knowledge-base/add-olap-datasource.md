---
title: How to add an OLAP DataSource
description: How to add an OLAP DataSource to Report Server
type: how-to
page_title: Add an OLAP DataSource
slug: add-olap-datasource
position: 
tags: 
ticketid: 1487188
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
This doucment describes how to configure Report Server and Report Designer so you can add an OLAP Data Source (Cube Data Source).

## Prerequisites
The suggested solution requires the following:

* Telerik Report Server
* Telerik Reporting
* __Telerik.ReportDesigner.exe__ and __Telerik.ReportDesigner.exe.config__ (located in ```[installation path]\Progress\Telerik Reporting {Version}\Report Designer```)

## Solution
The following steps describe how to implement the required configuration:

1. Locate the __Telerik.ReportDesigner.exe__ file in the Telerik Reporting installation folder and open the exe file.

1. Create a new report or open an existing one in Telerik Report Designer. For more information on how to create or open a report, see
[Working with Report Server Reports](../standalone-report-designer-working-with-server-reports#create-a-report-to-the-server).

1. Perform *step 1* described in [Configuring your project for using Microsoft Analysis Services](../cubedatasource-configuring-project).

1. Apply *step 2* and *step 3* described in [Configuring your project for using Microsoft Analysis Services](../cubedatasource-configuring-project) to the
__Telerik.ReportDesigner.exe.config__ file. [This example](../standalone-report-designer-extending-configuration) shows how to add the required 
assembly references to the designer's config file.

    >__Note__
    >
    >Telerik Reporting is built with ADOMD.NET for SQL Server 2008 R2, which means that the engine will expect to work with ```Microsoft.AnalysisServices.AdomdClient``` assembly version 10.0.0.0.
    >When you use a more recent SQL Server version, you also have a more recent version of the ```Microsoft.AnalysisServices.AdomdClient``` assembly.
    >That's why you need to add the binding redirect for this assembly as demonstrated in [step 3](../cubedatasource-configuring-project).

1. Verify that the Microsoft ADOMD.NET client data provider is installed on both Dev and Server machines. 

1. Once the report is published, apply the same settings in the ```[Telerik Report Server installation path]\Telerik.ReportServer.Web\TelerikReporting.config``` file.

1. Copy ```Microsoft.AnalysisServices.AdomdClient.dll``` and ```Telerik.Reporting.Adomd.dll``` into the ```Telerik.ReportServer.Web\bin``` and 
```Telerik Reporting {Version}\Report Designer``` folders. 

    >__Note__
    >
    >The ```Telerik.Reporting.Adomd.dll``` assembly is distributed with the Telerik Reporting 
    installation (located in ```[installation path]\Progress\Telerik Reporting {Version}\Bin)```.
