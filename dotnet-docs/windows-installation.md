---
title: Installation on Windows
page_title: Installing ReportServer.NET on Windows
description: "Learn about the specifics, recommendations, and available approaches for installing the Telerik Report Server for .NET on Windows."
slug: dotnet-installation-on-windows
tags: installation,dotnet,windows
published: True
position: 2
---

# Report Server for .NET: Installation on Windows

Starting from **2025 Q4**, a dedicated Report Server for .NET (RS.NET) installer is introduced. This article explains the installation steps and the differences from the Report Server for .NET Framework installer.

## Prerequisites

RS.NET is an ASP.NET Core web application that requires the [ASP.NET Core Hosting Bundle](https://learn.microsoft.com/en-us/aspnet/core/host-and-deploy/iis/?view=aspnetcore-8.0) for IIS deployment. Install this module following the [Install the ASP.NET Core Module/Hosting Bundle](https://learn.microsoft.com/en-us/aspnet/core/host-and-deploy/iis/?view=aspnetcore-8.0#install-the-aspnet-core-modulehosting-bundle) instructions before proceeding. The installation wizard will display a warning if this module is not available.

## Installation Process

TODO: mention what the msi is called and guide the user through the installation steps (go to downloads, etc.). while guiding, mention that currently there is no examples/migration tool (possibly in a note)

The installer automatically assigns available ports for RS.NET and RS.NET Service Agent. By default, these are ports 81 and 84 respectively, but it can assign the next available ones if these are already in use.

![Use the button Customize to allow installing the Report Server for .NET](../images/rs-net-images/rs-customize.png)

## Installed Assets

The __RS.NET__ is installed in `{Installation Folder}\Telerik Report Server\Telerik.ReportServer.Web.NET`. The cross-platform distribution of RS.NET is in the `_non-windows` subfolder.

The __RS.NET Service Agent__ is installed in `{Installation Folder}\Telerik Report Server\Services\.NET`. The cross-platform distribution of RS.NET Service Agent is in the `_non-windows` subfolder.

TODO: explain this further? what is the purpose of the cross-platform distribution now that RS.NET can be installed on Linux through the dedicated installer? there doesn't seem to be such a folder anymore. maybe move this whole section at the end of the article to keep the correct flow of actions (installation > configuration > additional details)

## Configuration

### Automatic Configuration on Windows

The installer is supposed to initially configure both RS.NET and RS.NET Service Agent on Windows, making them ready-to-run. If the automatic configuration fails, check the [instructions for manual configuration](#manual-configuration-on-windows).

TODO: what a fail could mean here? a crash in the installer (likely not since no assets would be installed to be checked) or that there is an error once RS.NET is opened in the browser? maybe move this sentence at the end of the installation process and move installed assets at the end of the article to keep the correct flow of actions

### Initialization process

TODO: maybe explain 2 and 3 in the installed assets section? make 1 longer

1. When the Report Server is started for the first time, the user is supposed to pass the _Configure Storage_ and _Register Administrator_ pages. The settings from these pages are stored in a file named `ReportServerAdmin.json`.
1. Next, the RS.NET checks its `appsettings.json` configuration file for the key __InitialAgentUrl__. If the installation has passed successfully, the key must exist and must have a valid value like __http://localhost:84__. This is where the MSI installation file for Windows has registered the __RS.NET Service Agent__.
1. The RS.NET calls the above URL and passes the storage settings to its Service Agent. They are saved in the file `ServiceAgent.json` in the RS.NET Service Agent's directory. If such a file does not exist, the agent was not initialized or registered in the IIS.

### Manual Configuration on Windows

1. Delete the file `\Services\.NET\ServiceAgent.json` from RS.NET Service Agent's folder if it exists.
1. Test whether the RS.NET Service Agent responds by calling the RS.NET Service Agent endpoint `/api/system/isalive` from the browser. By default, this would be the URL `http://localhost:84/api/system/isalive`.

	If the agent is working, the result must be __HTTP ERROR 401 - Unauthorized__.

	If the agent is not working, the result should be __404 - Not Found__.

1. Open RS.NET's `appsettings.json` configuration file and add/edit the key `"InitialAgentUrl": "http://localhost:84"`. The value in the example assumes the RS.NET Service Agent is running on port _84_. Change the URL based on your settings.
1. Restart the RS.NET and RS.NET Service Agent.
1. Check the RS.NET's _Configuration_ -> _ServiceAgent_ page. The entry `"DefaultServiceAgent" : "http://localhost:84"` should now be present. The URL may differ, depending on your settings.
1. To use the RS.NET Service Agent, ensure the _Mail Server_ settings in _Configuration_ page are valid.

TODO: what restart means in step 4? iisreset/recycling the app pool for rs.net and restarting the service agent through services.msc > rsnet service agent > restart? maybe change the section title to "debugging" to let know users are supposed to do this as last resort when the automatic configuration fails. explain that the pages that are mentioned have to be opened in the browser

TODO: Upgrade from old version of RS.NET (the one distributed with the combined MSI)/Downgrade from new RS.NET MSI to combined MSI - ask Hristov what these mean from the gh issue - whether users should be doing something to upgrade/downgrade or is it supposed to happen automatically and what does this upgrade/downgrade mean after all