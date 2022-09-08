---
title: Report Designer
page_title: Report Designer
description: Report Designer
slug: report-designer
tags: report,designer
published: true
position: 300
---

# Report Designer

The Report Designer is a report authoring tool. When you design a report, you specify where to get the data, which data to get, and how to display the data. When you run the report, the report generation engine takes all the information you have specified, retrieves the data, and combines it with the report layout to generate the final report document. You can preview these documents in Report Designer, or you can publish your report to Report Server, where others can run it.

### Access

The Report Designer tool can be accessed from the Report Server web management application upon new report or edit report action. If the web browser agent supports the ClickOnce deployment technology (built-in for IE and extension for other browsers), the tool gets installed on the client machine. Otherwise, the web application will provide a link to download and run the tool manually.
In the first case the user will get the subsequent tool updates handled by the ClickOnce technology, and in the latter this should be handled by the user (re-download a fresh version of the tool).

### Schema compatibility

The supported report definitions format eventually changes with the new versions of the Report Server product. The version of the report definition is referred as [Schema version](https://docs.telerik.com/reporting/upgrading-xml-report-definition-versioning#xml-schema-versioning). The definition schema version of a particular report stored on the server gets updated upon editing with a newer Report Designer. However, no Report Designer can be used having newer schema version than the one supported from the Report Server. This rule gets enforced from the Server and Designer negotiation logic so that the Server can actually render the uploaded report definition. The best practice is to always use the Report Designer coming with the current version of the Report Server product.

### Report Designer Localization with ClickOnce Deployment

Telerik Report Server supports localization of the Standalone Report Designer when used with ClickOnce deployment.

The **Report Designer -> Options -> Language** drop down lists all available languages (resources) located locally and on the connected Report Servers. If no language is explicitly defined, the Standalone Report Designer will use the language set in the Report Server administration.

### Data Connectivity

Report Server supports [WebService](https://docs.telerik.com/reporting/webservicedatasource-component), [SQL]({%slug data-connections-management%}), [Object]({%slug business-objects-management%}), and inline [CSV](https://docs.telerik.com/reporting/csvdatasource-component) data sources.

### Related Articles

- [Report Designer Overview](https://docs.telerik.com/reporting/designing-reports/report-designer-tools/desktop-designers/standalone-report-designer/overview "Standalone Report Designer Overview")
- [Create, Open, Edit, Save and Publish Reports](https://docs.telerik.com/reporting/designing-reports/report-designer-tools/desktop-designers/standalone-report-designer/working-with-report-server-reports "Working with server reports")
- [SqlDataSource Component](https://docs.telerik.com/reporting/designing-reports/connecting-to-data/data-source-components/sqldatasource-component/overview "SqlDataSource Component")
- [SqlDataSource Wizard](https://docs.telerik.com/reporting/designing-reports/report-designer-tools/desktop-designers/tools/data-source-wizards/sqldatasource-wizard/overview "SqlDataSource Wizard Overview")
- [CsvDataSource Component](https://docs.telerik.com/reporting/designing-reports/connecting-to-data/data-source-components/csvdatasource-component/overview "CsvDataSource Component")
- [CsvDataDource Wizard](https://docs.telerik.com/reporting/designing-reports/report-designer-tools/desktop-designers/tools/data-source-wizards/csvdatasource-wizard "CsvDataDource Wizard Overview")
- [Connecting to Business Objects]({%slug business-objects-management%})
