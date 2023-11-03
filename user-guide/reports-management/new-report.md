---
title: New Report
page_title: Adding New Report
description: "Learn how to create a new Telerik Reporting Report in the Report Server and the specifics when opening the Report Designer."
slug: new-report
tags: new,report
published: True
position: 110
---

# Creating New Reports

Invoke the desktop [Report Designer]({%slug report-designer%}) in order to create a new report on the server.

![new report](../../images/report-server-images/reports-management/new-report.png)

> The Report Designer will be started using the [ClickOnce deployment technology](https://learn.microsoft.com/en-us/previous-versions/visualstudio/visual-studio-2015/deployment/clickonce-security-and-deployment "ClickOnce Security and Deployment"). You can use a browser extension which adds support for the ClickOnce deployment technology. In case ClickOnce is not supported in your browser, clicking the New Report button will bring up a notification containing the Report Designer download link. Use the link to download and start the designer manually. In case you are experiencing issues with the ClickOnce deployment, you can try to clear the online application cache with the [Mage.exe (Manifest Generation and Editing Tool)](https://learn.microsoft.com/en-us/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool) or use `rundll32 dfshim CleanOnlineAppCache` command.

> If you add a [ReportBook](https://docs.telerik.com/reporting/designing-reports/report-book/overview) to the Report Server or use [SubReport item](https://docs.telerik.com/reporting/report-items/subreport) or [NavigateToReport action](https://docs.telerik.com/reporting/interactivity/actions/drillthrough-report-action) in your reports stored in the Report Server, ensure the [ReportSources](https://docs.telerik.com/reporting/embedding-reports/report-sources) are properly referenced, with their [CategoryName]/[ReportName] as explained in the article [Working with Report Server Reports](https://docs.telerik.com/reporting/standalone-report-designer-working-with-server-reports "Working with Report Server Reports").

## Telerik Report Server Learning Resources

* [Telerik Report Server Homepage](https://www.telerik.com/report-server)
* [Telerik Report Server Installation]({%slug installation%})
* [Telerik Report Server User Management]({%slug user-management%})
* [Connecting to Data with Telerik Report Server]({%slug connecting-to-data%})
* [Telerik Report Server License Agreement](https://www.telerik.com/purchase/license-agreement/report-server)

## See Also

* [Working with Report Server Reports](https://docs.telerik.com/reporting/standalone-report-designer-working-with-server-reports "Working with Report Server Reports")
