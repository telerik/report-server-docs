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

1. Download the archive `Telerik_ReportServer_Net_NonWindows_{Report Server version}.zip` from [your Telerik account](https://www.telerik.com/account/downloads/product-download?product=REPSERVER) and unzip it.

1. Unzip the archive. The content gets deployed in two folders `ReportServer` and `ReportServiceAgent`.

1. Open the `powershell` and navigate to the subfolder `ReportServer`.

1. Run the command `docker build -t telerik-report-server:local .` in powershell to build the Report Server Manager image.

1. Navigate to the subfolder `ReportServiceAgent`.

1. Run the command `docker build -t telerik-report-server-agent:local .` in powershell to build the Report Server ServiceAgent image.

1. Navigate to the subfolder `ReportServer\docker-configs`.

1. Open the file `docker-compose.yml` in a text editor like _Notepad++_ and edit its content. Delete everything between the lines `services:` and `  storage:`. Before the line `    environments` include the next lines:

	````yaml
	ports:
	..- "1433:1433"
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

1. Run the command `docker-compose up` in powershell to execute the above script and create the MsSqlServer container we are going to use as Report Server Storage.

1. Open `MSSQL Management Studio` and _Login_ with the following parameters:

	* _Server_  : `localhost`
	* _User_    : `sa`
	* _Password_: `place_your_sa_password_here` (this is the argument _SA_PASSWORD_ from the above script file. You may change it as required.)

1. Add the database named `reportserver`. After successfully creating the database, you may close the management studio.

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

1. Go back to powershell environment and execute the above yaml

mssql_storage.env

    ports:
      - "1433:1433"


storage: localhost
login: sa
passwd: place_your_sa_password_here
