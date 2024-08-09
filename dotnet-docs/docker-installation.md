---
title: Installation on Docker Container
page_title: Installing ReportServer.NET on Docker Container
description: "Learn about the specifics, recommendations, and available approaches for installing the Telerik Report Server for .NET on Docker Container."
slug: dotnet-installation-on-docker-container
tags: installation,dotnet,docker,container
published: True
position: 300
---

# Report Server for .NET: Installation on Docker Container

The Report Server for .NET (`RS.NET`) is ready for deployment on Docker Containers. We distribute separete assets for non-Windows platforms.

## Installation Process


1. Download the archive `Telerik_ReportServer_Net_NonWindows_{Report Server version}.zip` from your [Telerik account](https://www.telerik.com/account/downloads/product-download?product=REPSERVER) and unzip it.

1. Unzip the archive. The content gets deployed in two folders `ReportServer` and `ReportServiceAgent`.

1. Open the `powershell` and navigate to the subfolder `ReportServer`

1. Run the command `docker build -t telerik-report-server:local .` to build the Report Server Manager image

1. Navigate to the subfolder `ReportServiceAgent`

1. Run the command `docker build -t telerik-report-server-agent:local .` to build the Report Server ServiceAgent image






mssql_storage.env

    ports:
      - "1433:1433"


storage: localhost
login: sa
passwd: place_your_sa_password_here
