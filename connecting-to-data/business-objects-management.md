---
title: Business Objects Management
page_title: Business Objects Management
description: Business Objects Management
slug: business-objects-management
tags: business,objects,management
published: True
position: 700
---

# Business Objects Management



A common application design practice is to separate the presentation layer from business logic and encapsulate the business logic inside business objects. The Report Server can be integrated into such applications and/or use their business objects to provide data for reports. Custom .NET assemblies containing dedicated classes and data-retrieval methods can be added to the Report Server and the business objects data will be available during the design-time of reports via the [ObjectDataSource Component](https://docs.telerik.com/reporting/objectdatasource).

## How to Bind to a Business Object

1. Create an assembly containing custom business objects. The objects should conform to the [Supported Object Types](https://docs.telerik.com/reporting/objectdatasource#supported-object-types).

2. Copy the assembly to the **_bin_** folder of the Report Server Web Application. The default path is _C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web\bin_.

3. To enable access to the custom assembly when executing a scheduled task, copy the assembly to the folder containing the Report Server Windows Service. The default path is _C:\Program Files (x86)\Progress\Telerik Report Server\Services_.

4. Declare the assembly in the configuration files of the Web Application (_\Telerik Report Server\Telerik.ReportServer.Web\Web.config_) and Windows Service (_\Telerik Report Server\Services\Telerik.ReportServer.ServiceAgent.exe.config_) according to the instructions in the [Configuration](https://docs.telerik.com/reporting/objectdatasource#configuration) section.

5. Create [New Report]({%slug new-report%}).

6. Create new [ObjectDataSource Component](https://docs.telerik.com/reporting/objectdatasource) and follow the [ObjectDataSource Wizard](https://docs.telerik.com/reporting/objectdatasource-wizard) to select a .NET class and data-retrieval method from that class, and configure any data source parameters. Only simple type parameters are supported (Boolean, DateTime, Integer, Float, String, and arrays of them).

>The custom .NET class will show in the [ObjectDataSource Wizard](https://docs.telerik.com/reporting/objectdatasource-wizard) only when the currently logged-in user has Create/Edit permissions.
