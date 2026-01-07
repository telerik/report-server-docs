---
title: Storage Backup
page_title: Storage Backup
description: Telerik Report Server Storage Backup
slug: storage-backup
tags: backup,export
published: True
position: 730
---

# Storage Backup

The Report Server storage contains all user assets. Making a regular backup of the Report Server storage is a good practice to avoid eventual data loss. There are several ways to perform a backup.

## Automatic Backup

During product upgrade, the `.msi` installer performs an _automatic storage backup_ if the current product version supports this. It is a good practice not to skip this installation step.

## Backup Script

Along with the [storage migration tools](migration-tool), the installer deploys a PowerShell script called **rs-backup.ps1** located in the same _Tools\\_ subfolder of the installation directory.

The script is a convenient wrapper of the **migrate.exe** tool for the sole purpose of creating a storage backup.

This same script is carried with the product installer when performing the automatic backup and has two optional parameters:

- _first_ - being the product installation folder (defaults to _C:\Program Files (x86)\Progress\Telerik Report Server\\_)
- _second_ - being the destination folder of the produced .zip archive (defaults to a _Backup\\_ subfolder of the given installation folder).

  The second parameter can point to a _folder_ in which case the name of the generated archive in it will correspond to the current date.

  The other option for the second parameter is to be a _file path_ to a specific `.zip` file to be created.

The zip functionality requires _[PowerShell 5](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_windows_powershell_5.1?view=powershell-5.1) or later_, so if an older PS is used, the resulting backup will be a directory containing the migrated storage in the form of a file storage, which you might archive by other means.

The script generates a complete log file called **rs-backup.log** located in the target backup folder in order to account for the job done.

## Manual Backup

If the installed version of Report Server does not have the necessary tools for guided backup, you can still perform manual backup. Based on the currently configured storage, you need to take appropriate actions:

- MS SQL Server storage – Back up the respective database
- Redis storage – Back up the respective database
- File storage – Copy/Archive the respective folder

The preconfigured storage type and its parameters like connection string or destination folder can be discovered using the Configuration page of the Report Server management application or examining the _Telerik.ReportServer.Web\ReportServerAdmin.config_ configuration file located in the product installation folder.
