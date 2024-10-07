---
title: Logging in the Report Server for .NET 
page_title: Enabling logging in the Report Server for .NET
description: "Learn how to enable SeriLog logging in the Telerik Report Server for .NET application and service."
slug: logging-rs-net
tags: SeriLog,Logging,Troubleshooting,Error,RS.NET
published: True
position: 302
---

# Overview

The Report Server for .NET uses [Serilog](https://serilog.net/) to allow  writing diagnostic logging information from the server onto a file for easier troubleshooting.

## Setup

The configuration options for Serilog that would usually be set up through the C# API - [Serilog Configuration Basics](https://github.com/serilog/serilog/wiki/Configuration-Basics), can instead be
defined in the `appsettings.json` configuration files of the Report Server for .NET.

### Setup for the Server

The `appsettings.json` file for the Report Server for .NET can be found in its installation directory e.g. - `C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web.NET`.
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
        "Args": { "path": "Logs/logserverAll.txt" }
      }
    ]
  }
````

> For more configuration settings, refer to [Serilog Configuration Basics](https://github.com/serilog/serilog/wiki/Configuration-Basics).

### Setup for the Service Agent

The `appsettings.json` file for the Report Server for .NET can be found in its installation directory e.g. - `C:\Program Files (x86)\Progress\Telerik Report Server\Services\.NET`.
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
        "Args": { "path": "Logs/logserverAll.txt" }
      }
    ]
  }
````

> For more configuration settings, refer to [Serilog Configuration Basics](https://github.com/serilog/serilog/wiki/Configuration-Basics).
