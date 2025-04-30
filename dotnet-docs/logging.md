---
title: Logging in the Report Server for .NET 
page_title: Enabling logging in the Report Server for .NET
description: "Learn how to enable SeriLog logging in the Telerik Report Server for .NET application and service."
slug: logging-rs-net
tags: SeriLog,Logging,Troubleshooting,Error,RS.NET
published: True
position: 302
---

# Creating Logs in the Report Server for .NET

The Report Server for .NET uses [Serilog](https://serilog.net/) to allow  writing diagnostic logging information from the server onto a file for easier troubleshooting.

## Setup

The configuration options for Serilog that would usually be set up through the C# API - [Serilog Configuration Basics](https://github.com/serilog/serilog/wiki/Configuration-Basics), can instead be
defined in the `appsettings.json` configuration files of the Report Server for .NET.

### Report Server Manager

The `appsettings.json` file of the Report Server Manager for .NET resides in its installation directory, for example, `C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web.NET\`.
The following configuration settings can be added to that file, at the top level:

````JSON
  "Serilog": {
   "MinimumLevel": "Verbose",
    "WriteTo": [
      {
        "Name": "Console"
      },
	  {
        "Name": "File",
        "Args": { "path": "Logs/logServerManagerAll.txt" }
      }
    ]
  }
````

### Service Agent

The Report Server for .NET ServiceAgent's `appsettings.json` file can be found in its installation directory, by default - `C:\Program Files (x86)\Progress\Telerik Report Server\Services\.NET\`.
The following configuration settings can be added to that file, at the top level:

````JSON
  "Serilog": {
   "MinimumLevel": "Verbose",
    "WriteTo": [
      {
        "Name": "Console"
      },
	  {
        "Name": "File",
        "Args": { "path": "Logs/logServiceAgentAll.txt" }
      }
    ]
  }
````

> For more configuration settings, refer to [Serilog Configuration Basics](https://github.com/serilog/serilog/wiki/Configuration-Basics).

## See Also

* [Report Server for .NET Introduction]({%slug coming-soon%})
* [Report Server for .NET: Installation on Windows]({%slug dotnet-installation-on-windows%})
* [Report Server for .NET: Installation on Docker Container]({%slug dotnet-installation-on-docker-container%})
