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

The reports rendering engine is exercised from the Report Server instance in the following contexts:

- When generating live report preview and export from the Report Server manager or through a URL
- When exporting a report using the 'documents' Report Server WebApi endpoint
- When the report scheduling service executes a Scheduled Task or Data Alert

### Report Server for .NET Framework

The rendering engine can be fine-tuned using a dedicated configuration file, called **TelerikReporting.config**.
This file is automatically created on the server when it is started for the first time.

For the first two usages of the engine, the default location of this file is
_C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web\TelerikReporting.config_. The Report Server web application needs to be restarted manually in order to apply the changes.

For the report scheduling service usage the default location of the configuration file is
_c:\Program Files (x86)\Progress\Telerik Report Server\Services\TelerikReporting.config_. The **Telerik.ReportServer.ServiceAgent** windows service needs to be restarted manually in order to apply the changes.

Both files' content is not affected by Report Server upgrade installations.

#### XML Configuration Section

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

### Report Server for .NET

In the newer [Report Server for .NET](slug:report-server-net-overview), the rendering engine can be fine-tuned using a JSON-based configuration file called **TelerikReporting.json**, located at `C:\Program Files (x86)\Progress\Telerik Report Server .NET\Telerik.ReportServer.Web\config`(_default location_).

The **Telerik Report Server .NET** site needs to be manually restarted from the [IIS Manager](https://learn.microsoft.com/en-us/iis/get-started/getting-started-with-iis/getting-started-with-the-iis-manager-in-iis-7-and-iis-8) in order to apply the changes.

#### JSON Configuration Section

To become effective, open the **TelerikReporting.json** file and edit the `telerikReporting` section. Additional configuration options can be seen in the [Report Engine Configuration](https://docs.telerik.com/reporting/doc-output/configure-the-report-engine/overview) article.

```JSON
{
  "telerikReporting": {
    "restReportService": {
      "hostAppId": "TRS",
      "workerCount": 3,
      "reportSharingTimeout": 0,
      "clientSessionTimeout": 15
    }
  }
}
```

## Applicable settings

The applicable report generation engine settings can be found in the chapter [Telerik Reporting Configuration Section](https://docs.telerik.com/reporting/configuring-telerik-reporting).

## restReportService element settings

This specific element controls the online report preview and export functionality of the Report Server and is not applicable to the report scheduling service. The respective attributes are:

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
from a client will be eligible for reuse for another client's request.

The value must be greater than or equal to zero. A zero value will prevent rendered report document reuse.
The default value is zero.

Changing this is _highly recommended_ for a user-intensive Report Server deployment.
