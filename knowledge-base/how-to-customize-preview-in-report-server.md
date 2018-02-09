---
title: How to customize preview in Report Server
description: How to customize preview and apply styling when previewing reports in Report Server
type: how-to
page_title: How to customize preview in Report Server
slug: how-to-customize-preview-in-report-server
position: 
tags: preview
ticketid: 1151103
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
The layout of Reports Preview in Telerik Report Server is currently fixed, based on default CSS styling and Html template.

## Solution
The look of reports Preview in the Report Server is customizable in the same way the Html5 Report Viewer is.
To achieve the desired appearance you could use a local/custom template for the ReportViewer, where to refer a custom/modified CSS file with appropriate ReportViewer styles.  
The template should be assigned to the 'templateUrl' property of the HTML5ReportViewer, as explained in [this collection of help articles](https://docs.telerik.com/reporting/html5-report-viewer-styling-and-appearance).
  
Here is a sample step-by-step guide:  
  
1\. Create folder **styles** in (_**Telerik Report Server** installation folder_)\\Telerik.ReportServer.Web\\ReportViewer and add file **telerikReportViewer.css** with the viewer styles.
If you have Telerik Reporting installed on the machine, you could copy the file **telerikReportViewer.css** file from (_**Telerik Reporting** installation folder_)\Html5\ReportViewer (for example *C:\Program Files (x86)\Progress\Telerik Reporting R1 2018\Html5\ReportViewer\styles*).

Otherwise, you could download the content of file **telerikReportViewer.css** from the Report Server, and save it in the local folder. The exact URL is **(Report Server host)/api/reports/resources/styles/telerikReportViewer-css**.

After creating (copying/downloading) the file, you could modify the appropriate styles to achieve the desired report appearance in the viewer.

2\. Create folder **templates** in (_**Telerik Report Server** installation folder_)\\Telerik.ReportServer.Web\\ReportViewer and add file **telerikReportViewerTemplate.html** - the report viewer template.
If you have Telerik Reporting installed on the machine, you could copy the file **telerikReportViewerTemplate.html** file from (_**Telerik Reporting** installation folder_)\Html5\ReportViewer (for example *C:\Program Files (x86)\Progress\Telerik Reporting R1 2018\Html5\ReportViewer\templates*).

Otherwise, you could copy the code for file **telerikReportViewerTemplate.html** from the Report Server. The exact URL is **(Report Server host)/api/reports/resources/templates/telerikReportViewerTemplate-html**. Note that it would be necessary to display the actual code from the above URL with *View Page Source*, and copy and paste the code in the file.

Change the reference to CSS styles for the Report Viewer in **telerikReportViewerTemplate.html** file by substituting thе default code:
```HTML
<link href="{service}resources/styles/telerikReportViewer-css" rel="stylesheet" />
```
with thе code
```HTML
<link href="/ReportViewer/styles/telerikReportViewer.css" rel="stylesheet" />
```

3\. The viewer is configured in the _Preview.cshtml_ View file that could be found in the folder (_Telerik Report Server installation folder_)\\Telerik.ReportServer.Web\\Views\\Report (for example _C:\\Program Files (x86)\\Progress\\Telerik Report Server\\Telerik.ReportServer.Web\\Views\\Report_). Modify **Preview.cshtm** by setting **templateUrl** property of the ReportViewer:
```C#
.telerik_ReportViewer({
serviceUrl: '@Url.Content("~/api/reports/")',
// ADD THE FOLLOWING LINE TO REFER THE JUST CREATED CUSTOM TEMPLATE
templateUrl: '/ReportViewer/templates/telerikReportViewerTemplate.html',
reportSource: {
report: '@Model.ReportSource',
parameters: @Html.Raw(Json.Encode(Model.Parameters))
},
...........
});
```
4\. Restart the Report Server.
