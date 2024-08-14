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

The Report Server for .NET (`RS.NET`) is ready for deployment on Docker Containers. The assets for non-Windows platforms are available as separate resources downloadable from [your Telerik account](https://www.telerik.com/account/downloads/product-download?product=REPSERVER).

This article is a step-by-step tutorial on deploying Telerik Report Server for .NET on a Linux Docker Container with a [Microsoft SQL Server (MsSqlServer) Storage]({%slug storage-settings%}#microsoft-sql-server-mssqlserver) deployed on its own Docker Container based on the image `mcr.microsoft.com/mssql/server:2019-latest` exposed publicly on port `1433`.

## Installation Process

1. Download the archive `Telerik_ReportServer_Net_NonWindows_{Report Server version}.zip` from [your Telerik account](https://www.telerik.com/account/downloads/product-download?product=REPSERVER).
1. Unzip the archive. The content gets deployed in two folders `ReportServer` and `ReportServiceAgent`.
1. Open the `Powershell` and navigate to the subfolder `ReportServer`.
1. Run the command `docker build -t telerik-report-server:local .` in _Powershell_ to build the Report Server Manager image.
1. Navigate to the subfolder `ReportServiceAgent`.
1. Run the command `docker build -t telerik-report-server-agent:local .` in _Powershell_ to build the Report Server ServiceAgent image.
1. Navigate to the subfolder `ReportServer\docker-configs`.
1. Open the file `docker-compose.yml` in a text editor like _Notepad++_ and edit its content. Delete everything between the lines `services:` and `  storage:`. Before the line `    environments` include the next lines:

	````yaml
	ports:
	  - "1433:1433"
````

	The tabulation is essential and should be preserved. Here is the final content of the `docker-compose.yml` file:

	````yaml
services:

	storage:
	  image: "mcr.microsoft.com/mssql/server:2019-latest"
	  restart: always
	  ports:
	    - "1433:1433"
	  environment:
	    - SA_PASSWORD=place_your_sa_password_here
	    - ACCEPT_EULA=Y
	  volumes: 
	    - mssql-storage:/var/opt/mssql

	volumes:
	mssql-storage:
````


	Save the modified file.

1. Run the command `docker-compose up` in _Powershell_ to execute the above script to create and run the MsSqlServer Docker container we are going to use as Report Server Storage.
1. Open `MSSQL Management Studio` and _Login_ with the following parameters:

	* _Server_  : `localhost`
	* _User_    : `sa`
	* _Password_: `place_your_sa_password_here` (this is the argument _SA_PASSWORD_ from the above script file. You may change it as required.)

1. Add the database named `reportserver`. After successfully creating the database, you may close the management studio.
1. Stop the current process in _Powershell_, for example, with the key combination `Ctrl+C`.
1. Go back to the text editor with the opened file `docker-compose.yml` and restore its original content:

	````yaml
services:

	# template configuration of Report Server.
	# Includes sample config for /app/Data File Storage.
	telerik-report-server:
	  env_file:
	    - mssql_storage.env
	  image: telerik-report-server:local
	  restart: always
	  ports:
	    - "82:80"
	  depends_on: 
	    - storage

	# template configuration of Report Server Agent.
	# Includes sample config for /app/Data File Storage.
	telerik-report-server-agent:
	  environment:
	    - Agent__Name=FirstAgent,
	    - Agent__Address=http://telerik-report-server-agent:80
	  env_file:
	    - mssql_storage.env
	  image: telerik-report-server-agent:local
	  restart: always
	  depends_on:
	    - storage

	storage:
	  image: "mcr.microsoft.com/mssql/server:2019-latest"
	  restart: always
	  environment:
	    - SA_PASSWORD=place_your_sa_password_here
	    - ACCEPT_EULA=Y
	  volumes: 
	    - mssql-storage:/var/opt/mssql

	volumes:
	mssql-storage:
````

	Save the file.

1. Go back to the _Powershell_ environment and execute the above _yaml_ file with the same command `docker-compose up`. This should run the Report Server Manager and ReportServer.ServiceAgent for .NET.
1. Navigate to `localhost:82` in the browser to open the Report Server Manager for .NET.

The first time you open the Report Server you need to configure it as explained in the article [Application Startup]({%slug application-startup%}).

You may download and watch the whole process from our `reporting-samples` GitHub repository: [SetupRS.NET-Docker.mp4](https://github.com/telerik/reporting-samples/blob/master/VideosRS/SetupRS.NET-Docker.mp4).

The above approach for starting the RS.NET from the container will stop it each time you restart the machine. To avoid this, execute the following commands in _Powershell_ from the folder _.\ReportServer\docker-configs\_ to start/stop the Report Server instead of using the commands `docker-compose up` and `docker-compose down`:

1. (_optional_, use it only if it was not used before) Initialize a swarm to make the Docker Engine hosting the RS.NET a manager in the newly created single-node swarm:`docker swarm init`
1. Start the RS.NET with `.\start-docker-server.bat`
1. (_optional_) Stop the RS.NET with `.\stop-docker-server.bat`

## See Also

* [Telerik Report Server Introduction]({%slug introduction%})
* [Report Server for .NET Introduction]({%slug coming-soon%})
* [SetupRS.NET-Docker.mp4](https://github.com/telerik/reporting-samples/blob/master/VideosRS/SetupRS.NET-Docker.mp4)
