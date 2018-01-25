---
title: Upgrading Report Server
page_title: Upgrading Report Server
description: Upgrading Report Server
slug: upgrade
tags: upgrade
published: true
position: 205
---

# Upgrading Report Server

To upgrade an existing Report Server installation, you can run the [Telerik Report Server Installer]({%slug installation%}).
Telerik Report Server installer replaces existing files in the selected installation folder. 
The installer will preserve existing data storage and configuration files - _ReportServerAdmin.config_ and _ServiceAgent.config_.
The installer will not preserve any other config files such as _Web.config_ and _Telerik.ReportServer.ServiceAgent.exe.config_. Thus, it is recommended to perform a file backup before upgrading.

On first launch of the Report Server you can select to re-use the same data storage folder from the previous installation.

> The Report Server installer will not run if it detects an already installed Report Server of the same or greater version.
