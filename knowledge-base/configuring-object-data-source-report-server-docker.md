---
title: Setting Object Data Source in Report Server.NET
description: "Learn how to correctly add and configure an object data source for local Windows IIS installation of the Report Server for .NET, and also when the server is hosted in a Docker container."
type: how-to
page_title: Configuring ObjectDataSource in Report Server.NET on Docker Linux or Local Windows Installation
meta_title: Configuring ObjectDataSource in Report Server.NET on Docker Linux or Local Windows Installation
slug: configuring-object-data-source-report-server-docker
tags: report-server,docker,object-datasource,assembly,configuration
res_type: kb
ticketid: 1709828
---

## Environment

<table>
 <tbody>
  <tr>
   <td>Product</td>
   <td>Report Server</td>
  </tr>
  <tr>
   <td>Version</td>
   <td>11.3.26.121+</td>
  </tr>
 </tbody>
</table>

## Description

I need to configure an [ObjectDataSource component](https://www.telerik.com/products/reporting/documentation/designing-reports/connecting-to-data/data-source-components/objectdatasource-component/overview) in the [Report Server for .NET](slug:report-server-net-overview) hosted in a Docker container.

I added the `.dll` file to the container's `app` directory, but the data source does not appear in the [ObjectDataSource Wizard](https://www.telerik.com/products/reporting/documentation/designing-reports/report-designer-tools/desktop-designers/tools/data-source-wizards/objectdatasource-wizard) after restarting the container.

This knowledge base article also answers the following questions:

- How to add an external assembly in the Telerik [Report Server for .NET](slug:report-server-net-overview) in Docker?
- Why don't my types appear in the [Telerik Report Server for .NET](slug:report-server-net-overview)?

## Solution

### Case 1 - Docker Container

1. Add the `.dll` file to the container's `app` directory. For example, `/app/DataFunctions.dll`.
2. Update the `appsettings.json` file in the same directory to explicitly allow the assembly. Use the following Reporting configuration:

   ```json
   {
     "telerikReporting": {
       "assemblyReferences": [
         {
           "name": "DataFunctions"
         }
       ]
     }
   }
   ```

3. Ensure the `docker-compose.yml` file includes a storage service and mounts the necessary files. Use the following configuration:

   ```yaml
   services:
     telerik-report-server:
       image: progressofficial/telerik-reportserver-app:latest
       restart: always
       environment:
         - RSNET_AMO=True
         - RSNET_Platform=AMO
         - reportServer__storage__provider=MsSqlServer
         - reportServer__storage__parameters__0__name=ConnectionString
         - reportServer__storage__parameters__0__value=Server=tcp:<host>,1433;Initial Catalog=TelerikReportServer;Persist Security Info=False;User ID=sa;Password=<password>;Encrypt=False
       volumes:
         - ./DataFunctions.dll:/app/DataFunctions.dll
         - ./appsettings.json:/app/appsettings.json
       ports:
         - "80:80"
       depends_on:
         - storage
     storage:
       image: "mcr.microsoft.com/mssql/server:2022-latest"
       restart: always
       environment:
         - MSSQL_SA_PASSWORD=<password>
         - ACCEPT_EULA=Y
       volumes:
         - mssql-storage:/var/opt/mssql

   volumes:
     mssql-storage:
   ```

4. Restart the container to apply changes using the `docker compose up` command.
5. Verify the assembly and updated `appsettings.json` file are present in the container using the [Docker Desktop GUI](https://www.docker.com/products/docker-desktop/) or command-line tools.

After performing the above steps, the custom assemblies should appear when you open the [ObjectDataSource Wizard](https://www.telerik.com/products/reporting/documentation/designing-reports/report-designer-tools/web-report-designer/tools/objectdatasource-wizard) in the [Web Report Designer](slug:web-report-designer).

> If you encounter issues with the container creating new instances on each restart, ensure the storage configuration is correctly set up in the `docker-compose.yml` file.

### Case 2 - Local Windows Installation

1. Paste the custom assembly - `DataFunctions.dll`, in the installation folder of the Report Server for .NET web application - **C:\Program Files (x86)\Progress\Telerik Report Server .NET\Telerik.ReportServer.Web**.
2. Update the `appsettings.json` file in the same directory to explicitly allow the assembly. Use the following Reporting configuration:

   ```json
   {
     "telerikReporting": {
       "assemblyReferences": [
         {
           "name": "DataFunctions"
         }
       ]
     }
   }
   ```

3. Recycle the application pool of the Report Server for .NET, and restart the site from the `IIS Manager` for the changes to take effect.

## See Also

- [Getting Started with the IIS Manager in IIS](https://learn.microsoft.com/en-us/iis/get-started/getting-started-with-iis/getting-started-with-the-iis-manager-in-iis-7-and-iis-8)
- [AssemblyReferences Element](https://www.telerik.com/products/reporting/documentation/doc-output/configure-the-report-engine/assemblyreferences-element)
- [Docker Compose Documentation](https://docs.docker.com/compose/)
