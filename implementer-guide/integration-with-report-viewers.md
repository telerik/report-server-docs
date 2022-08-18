---
title: Integration With Telerik Report Viewers
page_title: Integration With Telerik Report Viewers
description: The article elaborates on connecting and using Telerik Report Server from a Telerik Report Viewer
slug: integration-with-report-viewers
tags: integration,report viewer
published: True
position: 810
---

# Integration With Report Viewers

Report Server can preview its stored reports through the integrated web report preview, but this can be insufficient for users that want to show server reports in their desktop or web application without redirecting to the Report Server manager. This is addressed by exposing the necessary APIs to the report viewers, so they can authenticate against the report server and gain access to its reports. 

## Configuration ##
Usually a client application uses a report viewer with a pre-defined connection to a reporting engine (*Embedded (local)*, *REST Service* or *Report Server*). Scenarios where the same report viewer will switch dynamically from local to server reports or back are not so common, so the best way to set up the report viewer’s report engine connection is through the Item Template Wizard. This is especially recommended for desktop viewers (WinForms and WPF), because in these cases a specific NuGet packages must be referenced to establish the connection with the Report Server engine and the Item Template Wizard will do it automatically. The following links to the Telerik Reporting documentation explain the process in details:
* [How To: Use Windows Forms Report Viewer With Report Server](https://docs.telerik.com/reporting/winforms-viewer-howto-use-it-with-reportserver)
* [How To: Use WPF Report Viewer With Report Server](https://docs.telerik.com/reporting/wpf-report-viewer-howto-use-it-with-reportserver)
* [How To: Use HTML5 Report Viewer with Report Server](https://docs.telerik.com/reporting/html5-report-viewer-howto-use-it-with-reportserver)

## Security ##
Since the user credentials will be sent to the Report Server instance in plain text, it is recommended to use a secure transport protocol (https) between the client and server. This will provide protection against reading or altering the information sent back and forth. 
The user credentials, however, can be seen when inspecting the page code in HTML5-based report viewers. This should not be considered as a security issue, because the report viewer must be used by the person that provides the credentials of its associated CAL user to access the Report Server. If the report viewer needs to be utilized by many users, then the [Guest]({%slug guest-user%}) user must be used which does not have credentials.
