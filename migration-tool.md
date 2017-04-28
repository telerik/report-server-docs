---
title: Telerik Report Server Storage Migration Tool
page_title: Telerik Report Server Storage Migration Tool
description: Telerik Report Server Storage Migration Tool
slug: migration-tool
tags: migration,export
published: True
position: 720
---

# Telerik Report Server Storage Migration Tool



The **Telerik Report Server Storage Migration Tool** is a standalone module shipped with the Telerik Report Server installation and its purpose is to provide easy out-of-the box solution for migrating the Report Server storage. It can be used from a command line or a graphical (Windows Forms) user interface. 

Command-Line Interface
----------------------

The executable must be started with two arguments - **source** and **destination**, followed by a connection information for every storage type. An example usage of the tool with command-line arguments would look like this:

*migrate.exe source=file,connection="C:\Report Server\Data" destination=redis,connection=localhost:6981,defaultDatabase=1*

Available values for **source/destination** parameter (case-insensitive): 
-	**file** - indicates that a file storage will be used.
-	**redis** - indicates that a Redis storage will be used.
-	**mssql** - indicates that a MSSQL server storage will be used.


File Storage Connection Parameters
----------------------------------

When using **file** as a storage type, the **connection** parameter must contain the path to the Telerik Report Server storage directory. By default it is named **Data** and is placed under **Telerik.ReportServer.Web** folder. When the path consists of directory names containing spaces, the argument must be enclosed in quotes. When used for destination parameter, make sure the current user has proper rights for creating files in the specified folder.


Redis Storage Connection Parameters
-----------------------------------

The migration tool uses *StackExchange.Redis.StrongName v.1.0.479* library as a client that accepts the value of the connection argument in order to create a connection to the database. Make sure the Redis storage instance is active and is accepting connections before commencing a migration. Examples for initializing the connection options can be found [here](https://github.com/StackExchange/StackExchange.Redis/blob/c6d8aec280722d83ed78b11e7b70d6d43b16ec98/Docs/Configuration.md).


MSSQL Storage Connection Parameters
-----------------------------------

Similar to the **redis** option, when  **mssql** type is used, the value of the connection parameter is passed as a connection string to the MSSQL client. Make sure the MSSQL server is active and accepts connections before commencing a migration. Examples for constructing the connection string can be found here. Note that if you do not specify a table name the data will be stored using the *master* schema.

Graphical User Interface
------------------------

The migration tool can be used via Windows Forms application that provides a convenient UI and an option to log the migration process output. The form requires setting type and connection information for **source** and **destination** storages - the same way it is done with the CLI tool. An events log text box will display the results of the migration process and its content can be copied to clipboard via a context menu. If needed, the same log can be saved to a file for further examination - in this case make sure your user has the necessary privileges for writing a file into log directory.
