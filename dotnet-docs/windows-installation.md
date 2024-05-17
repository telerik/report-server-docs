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

The Report Server for .NET is currently distributed along with Report Server for the installer for the .NET Framework 4.6.2. By default the installer does not install Report Server for .NET. Users must click `Customize` to install Report Server for .NET.

### Installation Process

The Report Server for .NET is an ASP.NET Core web applications and its installation on the IIS requires the `ASP.NET Core Hosting Bundle` as explained in the Microsoft article [Host ASP.NET Core on Windows with IIS](https://learn.microsoft.com/en-us/aspnet/core/host-and-deploy/iis/?view=aspnetcore-8.0). The installation wizard will show a warning in case the module is not installed. The user will be able to continue the installation although the module was not found.

>warning Known issue: the detection returns false negative result on machines having `Windows 11`, `Windows Server 2016` and `Windows Server 2022`. This is fixed and will be included in our next release.

The installer will configure the ports for installing the Report Server for .NET and Report Server for .NET Service Agent, taking the available ports from 80 upwards [screenshot]

