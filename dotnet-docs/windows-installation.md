---
title: Installation on Windows
page_title: Installing ReportServer.NET on Windows
description: "Learn about the specifics, recommendations, and available approaches for installing the Telerik Report Server for .NET on Windows."
slug: dotnet-installation-on-windows
tags: installation,dotnet,windows
published: True
position: 200
---

# Report Server for .NET Installation

The Report Server for .NET (`RS.NET`) is currently distributed along with the Report Server for the installer for the .NET Framework 4.6.2. By default, the installer does not install RS.NET. Users must click `Customize` to install RS.NET.

### Installation Process

The RS.NET is an ASP.NET Core web application and its installation on the IIS requires the `ASP.NET Core Hosting Bundle` as explained in the Microsoft article [Host ASP.NET Core on Windows with IIS](https://learn.microsoft.com/en-us/aspnet/core/host-and-deploy/iis/?view=aspnetcore-8.0). The installation wizard will show a warning if the module is not installed. The user can continue the installation although the module was not found.

>warning Known issue: the detection returns false negative results on machines having `Windows 11`, `Windows Server 2016` and `Windows Server 2022`. This is fixed and will be included in our next release.

The installer will configure the ports for installing the RS.NET and RS.NET Service Agent, taking the available ports from 80 upwards [screenshot]

### Installed Assets

The __RS.NET__ is installed in `{Installation Folder}\Telerik Report Server\Telerik.ReportServer.Web\.NET`. The cross-platform distribution of RS.NET is in the `_non-windows` subfolder.

The __RS.NET Service Agent__ is installed in `{Installation Folder}\Telerik Report Server\Services\.NET`. The cross-platform distribution of RS.NET Service Agent is in the '_non-windows' subfolder.

### Automatic Configuration

The installation wizard will do the initial configuration of RS.NET and RS.NET Service Agent on Windows, making them ready-to-run. 

For configuring RS.NET and RS.NET Service Agent on non-windows platforms, please, check [this article](link to other article with linux/docker docs).

