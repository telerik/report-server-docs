---
title: Installation on Docker Container
page_title: Installing ReportServer.NET on Docker Container
description: "Learn about the specifics, recommendations, and available approaches for installing the Telerik Report Server for .NET on Docker Container."
slug: dotnet-installation-on-docker-container
tags: installation,dotnet,docker,linux,container
published: True
position: 300
---

# Report Server for .NET: Installation on Docker Container

The Report Server for .NET (`RS.NET`) is ready for deployment on Docker Containers. The assets for non-Windows platforms are available as separate resources downloadable from [your Telerik account](https://www.telerik.com/account/downloads/product-download?product=REPSERVER).

This article is a step-by-step tutorial on deploying Telerik Report Server for .NET on a Linux Docker Container with a [Microsoft SQL Server (MsSqlServer) Storage]({%slug storage-settings%}#microsoft-sql-server-mssqlserver) deployed on its own Docker Container based on the image `mcr.microsoft.com/mssql/server:2019-latest` exposed publicly on port `1433`.

## Installation Process

1. Download the archive `Telerik_ReportServer_Net_NonWindows_{Report Server version}.zip` from [your Telerik account](https://www.telerik.com/account/downloads/product-download?product=REPSERVER).
1. Unzip the archive. The content gets deployed in two folders `ReportServer` and `ReportServiceAgent`.
1. Open the `Powershell` and navigate to the subfolder `ReportServer`.
1. Run the command `docker build -t telerik-report-server:local .` in _Powershell_ to build the Report Server Manager image. Mind the dot `.` at the end of the command.
1. Navigate to the subfolder `ReportServiceAgent`.
1. Run the command `docker build -t telerik-report-server-agent:local .` in _Powershell_ to build the Report Server ServiceAgent image. Mind the dot `.` at the end of the command.
1. Navigate to the subfolder `ReportServer\docker-configs`.
1. (_optional, recommended_) Change the password `P1@ceStr0ngP@ssw0rdH3r3` for the SA database user with your own strong password in the files `docker-compose.yml` and `mssql_storage.env`:

	* Open the file `docker-compose.yml` in a text editor like Notepad++ and change the password on line 31. The tabulation is essential and should be preserved:

	`      - SA_PASSWORD=P1@ceStr0ngP@ssw0rdH3r3`

	* Open the file `mssql_storage.env` in a text editor like Notepad++ and change the password with your own password you used above:

	`reportServer__storage__parameters__0__value=Data Source=storage;Initial Catalog=reportserver;Password=P1@ceStr0ngP@ssw0rdH3r3;User Id=sa;Encrypt=false`

1. Run the command `docker image pull mcr.microsoft.com/mssql/server:2019-latest`.
1. Run the command `docker stack deploy -c docker-compose.yml report-server`.
1. Navigate to `localhost:82` in the browser to open the Report Server Manager for .NET.

The first time you open the Report Server you need to configure it as explained in the article [Application Startup]({%slug application-startup%}).

## Additional Resources

You may download and watch the whole process from our `reporting-samples` GitHub repository: [SetupRS.NET-Docker.zip](https://github.com/telerik/reporting-samples/blob/master/VideosRS/SetupRS.NET-Docker.zip).

## Notes

The above approach for starting the RS.NET from the container will stop it *each* time you restart the machine. To avoid this, execute the following commands in _Powershell_ from the folder _.\ReportServer\docker-configs\_ to start/stop the Report Server instead of using the commands `docker-compose up` and `docker-compose down`:

1. (_optional_, use it only if it was not used before) Initialize a swarm to make the Docker Engine hosting the RS.NET a manager in the newly created single-node swarm:`docker swarm init`
1. Start the RS.NET with `.\start-docker-server.bat`
1. (_optional_) Stop the RS.NET with `.\stop-docker-server.bat`

## See Also

* [Telerik Report Server Introduction]({%slug introduction%})
* [Report Server for .NET Introduction]({%slug coming-soon%})
