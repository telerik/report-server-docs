---
title: Configure the Report Rendering Engine
page_title: Configure the Report Rendering Engine
description: Configure the Report Rendering Engine
slug: configure-the-report-engine
tags: configuration,settings,config,rest,rendering
published: True
position: 800
---

# Configure the Report Rendering Engine

## Configuration File

The reports rendering engine gets exercised From the Report Server instance in the following contexts:
- When generating live report preview and export from the Report Server manager or thru URL
- When exporting a report using the 'documents' Report Server WebApi endpoint
- When the report scheduling service executes a Scheduled Task or Data Alert

The rendering engine can be fine-tuned using a dedicated configuration file, called **TelerikReporting.config**.
This file gets automatically created on the server when it is started for the first time.

For the first two usages of the engine the default location of this file is
*C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web\TelerikReporting.config*. The Report Server web application needs to be restarted manually in order to apply the changes.

For the report scheduling service usage the default location of the configuration file is
*c:\Program Files (x86)\Progress\Telerik Report Server\Services\TelerikReporting.config*. The **Telerik.ReportServer.ServiceAgent** windows service needs to be restarted manually in order to apply the changes.

Both files' content does not get affected from eventual Report Server upgrade installation.

## Telerik.Reporting configuration section

To become effective, open the **TelerikReporting.config** file and uncomment the TelerikReporting configuration section registration:

```XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <section name="Telerik.Reporting" type="{0}" allowLocation="true" allowDefinition="Everywhere" />
  </configSections>
  <Telerik.Reporting>
    <restReportService workerCount="3" clientSessionTimeout="15" reportSharingTimeout="0" />
  </Telerik.Reporting>
</configuration>
```
## Applicable settings

The applicable report generation engine settings can be found in the chapter [Telerik Reporting Configuration Section](https://docs.telerik.com/reporting/configuring-telerik-reporting). 

## restReportService element settings

This specific element controls the online report preview and export functionality of the Report Server and is not applicable for the report scheduling service. The respective attributes are:

### workerCount 
Optional integer attribute. Specifies the combined count of report rendering worker threads that render report documents 
for the live report preview and export and for the 'documents' WebApi endpoint.
The default value is equal to the logical processors available on the server machine. 

### clientSessionTimeout 
Optional integer attribute. Specifies the value in minutes indicating how long a client report preview session 
will be preserved in the service storage after the last interaction with the report content from this client.
The value must be greater than zero. The default value is 15 minutes. 

### reportSharingTimeout
Optional integer attribute. Specifies the value in minutes indicating how long a rendered report document
from a client will be eligible for reuse for another clients' request.
The value must be greater than or equal to zero. A zero value will prevent rendered report document reuse.
The default value is zero. Changing this is highly recommended for a user-intensive Report Server deployment.
