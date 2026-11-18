---
title: Standalone Report Designer
page_title: Standalone Report Designer
description: Standalone Report Designer in Telerik Report Server
slug: report-designer
tags: report,designer
published: true
position: 3
---

# Standalone Report Designer

The Standalone Report Designer is a report authoring tool. When you design a report, you specify where to get the data, which data to get, and how to display the data.

When you run the report, the report generation engine takes all the information you have specified, retrieves the data, and combines it with the report layout to generate the final report document.

You can preview these documents in Standalone Report Designer, or you can publish your report to Report Server, where others can run it.

## Server and Designer Compatibility

Use the Standalone Report Designer that matches your Report Server's framework. The following table lists the corresponding variants:

| Report Server | Standalone Report Designer |
| --- | --- |
| Report Server for .NET Framework 4.6.2 | Standalone Report Designer for .NET Framework: `Telerik.ReportDesigner.exe` or `Telerik.ReportDesigner.x86.exe` |
| Report Server for .NET | Standalone Report Designer for .NET: `Telerik.ReportDesigner.Net.exe` or `Telerik.ReportDesigner.Net.x86.exe` |

Use the designer distributed with the target Report Server to match both the framework and the associated designer release.

>important Do not mix the .NET Framework and .NET variants for direct server connections. Different serialization behavior can cause errors, including errors when you create a blank report on the server.

A successful connection or matching report-definition schema does not establish compatibility between the two variants. The [schema requirement](#schema-compatibility) applies in addition to the framework requirement.

The framework requirement applies to direct communication, not all transfers of report files. Before you transfer a report between frameworks, verify its schema and format, supported features, and runtime dependencies, such as custom assemblies. Preview and validate the report in the destination environment. For format and schema details, see [Declarative Report Definition](https://docs.telerik.com/reporting/designing-reports/report-designer-tools/desktop-designers/standalone-report-designer/xml-report-definition).

## Access

Use the new-report or edit action in the Report Server web management application to access the corresponding designer.

### Report Server for .NET Framework 4.6.2

Report Server for .NET Framework uses ClickOnce to deploy and start the .NET Framework designer when the browser supports ClickOnce. Otherwise, use the download link to download and run `Telerik.ReportDesigner.exe` manually.

ClickOnce handles subsequent designer updates. For a manually downloaded designer, download a fresh copy from the target server after a server upgrade.

### Report Server for .NET

Use the designer download link in Report Server for .NET to download and run `Telerik.ReportDesigner.Net.exe` on Windows. Do not use the .NET Framework designer from another installation.

Download a fresh copy from the target server after a server upgrade.

## Schema Compatibility

Report Server releases can introduce a new [report-definition schema version](https://docs.telerik.com/reporting/designing-reports/report-designer-tools/desktop-designers/standalone-report-designer/xml-report-definition#xml-schema-versioning).

When you edit and save a report with a newer designer, its definition can use a newer schema. The designer must not use a newer schema than the server supports.

The connection negotiation checks this schema requirement. It does not verify that the server and designer target the same framework. Use the designer distributed with the target Report Server to meet both requirements.

## Standalone Report Designer Localization with ClickOnce Deployment

Telerik Report Server supports localization of the Standalone Report Designer when used with **ClickOnce** deployment.

The `Report Designer` -> `Options` -> `Language` drop-down lists all available languages (resources) located locally and on the connected Report Servers. If no language is explicitly defined, the Standalone Report Designer will use the language set in the Report Server administration.

## Data Connectivity

Report Server supports [WebService](https://docs.telerik.com/reporting/designing-reports/connecting-to-data/data-source-components/webservicedatasource-component/overview), [SQL](slug:data-connections-management), [Object](slug:business-objects-management), and inline [JSON DataSource](https://docs.telerik.com/reporting/designing-reports/connecting-to-data/data-source-components/jsondatasource-component) and [CSV](https://docs.telerik.com/reporting/designing-reports/connecting-to-data/data-source-components/csvdatasource-component/overview) data sources.

## Telerik Report Server Learning Resources

- [Telerik Report Server Homepage](https://www.telerik.com/report-server)
- [Telerik Report Server Installation](slug:installation)
- [Telerik Report Server User Management](slug:user-management)
- [Connecting to Data with Telerik Report Server](slug:connecting-to-data)
- [Telerik Report Server License Agreement](https://www.telerik.com/purchase/license-agreement/report-server)

## See Also

- [Report Designer Overview](https://docs.telerik.com/reporting/designing-reports/report-designer-tools/desktop-designers/standalone-report-designer/overview "Standalone Report Designer Overview")
- [Create, Open, Edit, Save, and Publish Reports](https://docs.telerik.com/reporting/designing-reports/report-designer-tools/desktop-designers/standalone-report-designer/working-with-report-server-reports "Working with server reports")
- [SqlDataSource Component](https://docs.telerik.com/reporting/designing-reports/connecting-to-data/data-source-components/sqldatasource-component/overview "SqlDataSource Component")
- [SqlDataSource Wizard](https://docs.telerik.com/reporting/designing-reports/report-designer-tools/desktop-designers/tools/data-source-wizards/sqldatasource-wizard/overview "SqlDataSource Wizard Overview")
- [JSON DataSource Component](https://docs.telerik.com/reporting/designing-reports/connecting-to-data/data-source-components/jsondatasource-component)
- [JsonDataSource Wizard](https://docs.telerik.com/reporting/designing-reports/report-designer-tools/desktop-designers/tools/data-source-wizards/jsondatasource-wizard)
- [CsvDataSource Component](https://docs.telerik.com/reporting/designing-reports/connecting-to-data/data-source-components/csvdatasource-component/overview "CsvDataSource Component")
- [CsvDataDource Wizard](https://docs.telerik.com/reporting/designing-reports/report-designer-tools/desktop-designers/tools/data-source-wizards/csvdatasource-wizard "CsvDataDource Wizard Overview")
- [Connecting to Business Objects](slug:business-objects-management)
