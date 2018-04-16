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

The reports rendering engine can be fine-tuned using a dedicated configuration file, called TelerikReporting.config .
This file gets automatically created on the server when it is stated for first time. The default location of this file is
C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web\TelerikReporting.config and affects the
live report preview generation and the WebApi 'documents' endpoint.

## Telerik.Reporting configuration section

To become effective, open the TelerikReporting.config file and uncomment the TelerikReporting configuration section registration:

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

## restReportService element settings

The following are the attribute settings applicable to the Report Server:

### workerCount 
Optional integer attribute. Specifies the combined count of worker report rendering threads that render report documents 
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
The default value is zero. Changing this is highly recommended for intensively user Report Server deployment.
