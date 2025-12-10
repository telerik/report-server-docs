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

This document describes how to configure the Report Server and Report Designer so you can add an OLAP Data Source (Cube Data Source).

## Prerequisites

The suggested solution requires the following:

- Telerik Report Server
- Telerik Reporting
- `Telerik.ReportDesigner.exe` and `Telerik.ReportDesigner.exe.config` (located in `_InstallationPath_\Progress\Telerik Reporting {Version}\Report Designer`)

## Solution

The following steps describe how to implement the required configuration:

1. Locate the `Telerik.ReportDesigner.exe` file in the Telerik Reporting installation folder and open the exe file.
1. Create a new report or open an existing one in Telerik Report Designer. For more information on how to create or open a report, see [Working with Report Server Reports](https://docs.telerik.com/reporting/designing-reports/report-designer-tools/desktop-designers/standalone-report-designer/working-with-report-server-reports).
1. Perform _step 1_ described in [Configuring your project for using Microsoft Analysis Services](https://docs.telerik.com/reporting/designing-reports/connecting-to-data/data-source-components/cubedatasource-component/configuring-your-project-for-using-microsoft-analysis-services).
1. Apply _step 2_ and _step 3_ described in [Configuring your project for using Microsoft Analysis Services](https://docs.telerik.com/reporting/designing-reports/connecting-to-data/data-source-components/cubedatasource-component/configuring-your-project-for-using-microsoft-analysis-services) to the `Telerik.ReportDesigner.exe.config` file. The article [Extending Report Designer](https://docs.telerik.com/reporting/designing-reports/report-designer-tools/desktop-designers/standalone-report-designer/configuration/extending-report-designer) explains how to add the required assembly references to the designer's config file.

   > Telerik Reporting is built with **ADOMD.NET for SQL Server 2008 R2**, which means that the engine will expect to work with `Microsoft.AnalysisServices.AdomdClient` assembly version `10.0.0.0`. When you use a more recent SQL Server version, you also have a more recent version of the `Microsoft.AnalysisServices.AdomdClient` assembly. That's why you need to add the binding redirect for this assembly as demonstrated in [step 3](https://docs.telerik.com/reporting/designing-reports/connecting-to-data/data-source-components/cubedatasource-component/configuring-your-project-for-using-microsoft-analysis-services).

1. Verify that the Microsoft ADOMD.NET client data provider is installed on both Dev and Server machines.
1. Once the report is published, apply the same settings in the `_TelerikReportServerInstallationFolder_\Telerik.ReportServer.Web\TelerikReporting.config` file.
1. Copy `Microsoft.AnalysisServices.AdomdClient.dll` and `Telerik.Reporting.Adomd.dll` into the `Telerik.ReportServer.Web\bin` and `Telerik Reporting {Version}\Report Designer` folders.

   > The `Telerik.Reporting.Adomd.dll` assembly is distributed with the Telerik Reporting installation. It is located by default in `_InstallationPath_\Progress\Telerik Reporting {Version}\Bin)`.
