---
title: Integration with Report Viewers
page_title: Integration With Telerik Report Viewers
description: The article elaborates on connecting and using Telerik Report Server from a Telerik Report Viewer
slug: integration-with-report-viewers
tags: integration,report viewer
published: True
position: 9
---

# Integration With Report Viewers

The Report Server can preview its stored reports through the integrated web report preview, but this can be insufficient for users that want to show server reports in their desktop or web application without redirecting to the Report Server manager.

This is addressed by exposing the necessary APIs to the report viewers, so they can authenticate against the report server and gain access to its reports.

## Configuration

Often, a client application uses a report viewer with a pre-defined connection to a reporting engine (_Embedded (local)_, _REST Service_ or _Report Server_). Scenarios where the same report viewer will switch dynamically from local to server reports or back are not so common, so the best way to set up the report viewer’s report engine connection is through the Item Template Wizard.

This is especially recommended for desktop viewers (WinForms and WPF), because in these cases a specific NuGet packages must be referenced to establish the connection with the Report Server engine and the Item Template Wizard will do it automatically.

The following links to the Telerik Reporting documentation explain the process in details:

- [How to Use HTML5 Report Viewer with Report Server](https://docs.telerik.com/reporting/embedding-reports/display-reports-in-applications/web-application/html5-report-viewer/how-to-use-html5-report-viewer-with-report-server "Embed HTML5 Report Viewer connected to the Report Server").
- [How to Use HTML5 ASP.NET MVC Report Viewer With Report Server](https://docs.telerik.com/reporting/embedding-reports/display-reports-in-applications/web-application/html5-asp.net-mvc-report-viewer/how-to-use-html5-asp.net-mvc-report-viewer-with-report-server "Embed HTML5 ASP.NET MVC Report Viewer connected to the Report Server")
- [How to Use HTML5 ASP.NET Web Forms Report Viewer with Report Server](https://docs.telerik.com/reporting/embedding-reports/display-reports-in-applications/web-application/html5-asp.net-web-forms-report-viewer/use-html5-web-forms-viewer-with-report-server "Embed HTML5 ASP.NET Web Forms Report Viewer connected to the Report Server")
- [How to Use React Report Viewer with Report Server](https://docs.telerik.com/reporting/embedding-reports/display-reports-in-applications/web-application/react-report-viewer/how-to-use-react-report-viewer-with-report-server "Embed React Report Viewer connected to the Report Server")
- [How To: Use Windows Forms Report Viewer With Report Server](https://docs.telerik.com/reporting/embedding-reports/display-reports-in-applications/windows-forms-application/how-to-use-windows-forms-report-viewer-with-report-server "Embed Windows Forms Report Viewer connected to the Report Server")
- [How To: Use WPF Report Viewer With Report Server](https://docs.telerik.com/reporting/embedding-reports/display-reports-in-applications/wpf-application/how-to-use-wpf-report-viewer-with-report-server "Embed WPF Report Viewer connected to the Report Server")

## Security

Since the user credentials will be sent to the Report Server instance in plain text, it is recommended to use a secure transport protocol (https) between the client and server. This will provide protection against reading or altering the information sent back and forth.

The user credentials, however, can be seen when inspecting the page code in HTML5-based report viewers. This should not be considered as a security issue, because the report viewer must be used by the person that provides the credentials of its associated CAL user to access the Report Server.

If the report viewer needs to be utilized by many users, then the [Guest]({%slug guest-user%}) user must be used which does not have credentials.
