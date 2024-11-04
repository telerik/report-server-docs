---
title: Storage
page_title: Storage
description: Storage Settings
slug: storage-settings
tags: storage,settings
published: True
position: 400
---

# Storage

The storage settings view allows you to specify where the reports and their metadata will be stored on the server. By default the application is using a **File** storage with relative to the web application path: "_~/Data"_

## Storage Types

### Microsoft SQL Server (MsSqlServer)

> Consider rebuilding the indexing of the MsSqlServer storage tables if the Report Server starts responding slower. You may use the approach from the article [Automate rebuilding SQL Database indexes using Maintenance Plans](https://www.sqlshack.com/automate-rebuild-indexes-of-sql-database-using-maintenance-plans/) to avoid the issue in the future.

This storage type uses the Microsoft SQL Server database and can also be used when the Report Server is deployed on a web farm.
To use this storage you should specify a connection string to the desired database.  

> When saving the configuration settings, the tables and the stored procedures that are needed will be created automatically. However, the database should be created in advance and the user under which the web application is running should have the necessary permissions to modify the database schema.

### Redis

This storage type uses the [Redis](http://redis.io/) key-value cache and store. The **Redis** storage is configured through a [configuration](https://stackexchange.github.io/StackExchange.Redis/Configuration.html) string.
Examples: 
````
localhost:6375
localhost:6379, defaultdatabase=3
````

### File

Тhe file storage uses the file system of the operating system to store the reports and other data. To configure this storage specify the location of the storage by using the **BasePath** parameter. 
It can be also a relative path to the report server's web application. For example: "_~/Data/ReportServer_".
