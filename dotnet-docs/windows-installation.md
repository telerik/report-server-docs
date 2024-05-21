---
title: Installation on Windows
page_title: Installing ReportServer.NET on Windows
description: "Learn about the specifics, recommendations, and available approaches for installing the Telerik Report Server for .NET on Windows."
slug: dotnet-installation-on-windows
tags: installation,dotnet,windows
published: True
position: 200
---

# Report Server for .NET Installation on Windows

The Report Server for .NET (`RS.NET`) is currently distributed along with the Report Server for the installer for the .NET Framework 4.6.2. By default, the installer does not install RS.NET. Users must click `Customize` to install RS.NET.

### Installation Process

The RS.NET is an ASP.NET Core web application and its installation on the IIS requires the `ASP.NET Core Hosting Bundle` as explained in the Microsoft article [Host ASP.NET Core on Windows with IIS](https://learn.microsoft.com/en-us/aspnet/core/host-and-deploy/iis/?view=aspnetcore-8.0). The installation wizard will show a warning if the module is not installed. The user can continue the installation although the module was not found.

>warning Known issue: the detection returns false negative results on machines having `Windows 11`, `Windows Server 2016` and `Windows Server 2022`. This is fixed and will be included in our next release.

The installer will configure the ports for installing the RS.NET and RS.NET Service Agent, taking the available ports from 80 upwards [screenshot]

### Installed Assets

The __RS.NET__ is installed in `{Installation Folder}\Telerik Report Server\Telerik.ReportServer.Web\.NET`. The cross-platform distribution of RS.NET is in the `_non-windows` subfolder.

The __RS.NET Service Agent__ is installed in `{Installation Folder}\Telerik Report Server\Services\.NET`. The cross-platform distribution of RS.NET Service Agent is in the '_non-windows' subfolder.

### Automatic Configuration

The installation wizard will do the initial configuration of _RS.NET_ and _RS.NET Service Agent_ on Windows, making them ready-to-run.

###  Initialization process

1. When the Report Server is started for the first time, the user is supposed to pass the _Configure Storage_ and _Register Administrator_ pages. The settings from these pages are stored in a file named `ReportServerAdmin.json`.
1. Next, the RS.NET checks its `appsettings.json` configuration file for the key __InitialAgentUrl__. If the installation has passed successfully, the key must exist and must have a valid value like `http://localhost:84`. This is where the MSI has registered the __RS.NET Service Agent__.
1. The RS.NET calls the above URL and passes the storage settings to the service agent. They are saved in a file in the RS.NET Service Agent's directory, named `\Services\.NET\ServiceAgent.json`. If such a file does not exist, the agent was not initialized or registered in the IIS.
