---
title: Generating Logs
page_title: Recording runtime logs in the Report Server for .NET
description: "Learn how to enable SeriLog logging in the Telerik Report Server for .NET application and service."
slug: logging-rs-net
tags: SeriLog,Logging,Troubleshooting,Error,RS.NET
published: True
position: 10
---

# Creating Logs in the Report Server for .NET

The Report Server for .NET uses [Serilog](https://serilog.net/) to allow writing diagnostic logging information from the server onto a file for easier troubleshooting.

## Setup

The configuration options for Serilog that would usually be set up through the C# API - [Serilog Configuration Basics](https://github.com/serilog/serilog/wiki/Configuration-Basics), can be configured in two ways:

1. [Environment Variables](#using-environment-variables) - Set system-wide environment variables.
2. [Configuration Files](#using-configuration-files) - Modify the `appsettings.json` files directly.

### Using Environment Variables

You can enable logging for both the Report Server Manager and Service Agent at the same time by setting the following environment variables:

- `Serilog__MinimumLevel=Verbose`
- `Serilog__WriteTo__1__Name=File`
- `Serilog__WriteTo__1__Args__path=Logs/rsnetlogs.txt`

This requires the default Serilog configuration to exist in the `appsettings.json` files for both the manager and service components, as environment variables are intended to override these base settings as needed.

> note When the Report Server is installed using the MSI installer, it runs under a dedicated Windows user account (ReportServerUser) or a system account (e.g., LocalSystem), depending on your installation choice.
>
> These accounts do not have access to user-level environment variables. To ensure environment variable overrides work correctly, you must define them at the **system level**.

### Using Configuration Files

Alternatively, you can define the configuration in the `appsettings.json` configuration files of the Report Server for .NET.

#### Report Server Manager

The `appsettings.json` file of the Report Server Manager for .NET resides in its installation directory, for example, `C:\Program Files (x86)\Progress\Telerik Report Server .NET\Telerik.ReportServer.Web\`.

The following configuration settings can be added to that file, at the top level:

```JSON
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
```

#### Service Agent

The Report Server for .NET ServiceAgent's `appsettings.json` file can be found in its installation directory, by default - `C:\Program Files (x86)\Progress\Telerik Report Server .NET\Services\`.

The following configuration settings can be added to that file, at the top level:

```JSON
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
```

> For more configuration settings, refer to [Serilog Configuration Basics](https://github.com/serilog/serilog/wiki/Configuration-Basics).

## See Also

- [Report Server for .NET Introduction]({%slug report-server-net-overview%})
- [Report Server for .NET: Installation on Windows]({%slug dotnet-installation-on-windows%})
- [Report Server for .NET: Installation on Docker Container]({%slug dotnet-installation-on-docker-container%})
