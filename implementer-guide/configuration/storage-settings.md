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

The storage settings view allows you to specify where the reports and their metadata will be stored on the server. By default, the application uses a **File** storage relative to the web application path: "_~/Data"_.

The Report Server Storage assets are serialized and saved as a [key-value store](https://en.wikipedia.org/wiki/Key%E2%80%93value_database).

## Storage Types

### Microsoft SQL Server (MsSqlServer)

> Consider rebuilding the indexing of the MsSqlServer storage tables if the Report Server starts responding more slowly. You may use the approach from the article [Automate rebuilding SQL Database indexes using Maintenance Plans](https://www.sqlshack.com/automate-rebuild-indexes-of-sql-database-using-maintenance-plans/) to avoid the issue in the future.

This storage type uses the Microsoft SQL Server database and can also be used when the Report Server is deployed on a web farm.
To use this storage, you should specify a connection string to the desired database.

> When saving the configuration settings, the tables and the stored procedures that are needed will be created automatically. However, the database should be created in advance and the user under which the web application is running should have the necessary permissions to modify the database schema.

### Redis

This storage type uses the [Redis](http://redis.io/) key-value cache and store. The **Redis** storage is configured through a [configuration](https://stackexchange.github.io/StackExchange.Redis/Configuration.html) string.

Examples:

- `localhost:6375`
- `localhost:6379, defaultdatabase=3`

### File

The file storage uses the file system of the operating system to store the reports and other data. To configure this storage, specify the location of the storage by using the **BasePath** parameter.

It can also be a relative path to the report server's web application. For example: `_~/Data/ReportServer_`.

## Cross-Platform Database Storage

Starting with [Report Server 2026 Q4 (12.3.26.1125)](<https://www.telerik.com/support/whats-new/report-server/release-history/progress-telerik-report-server-2026-q4-(12-3-26-1125)>), Report Server for .NET can use the same Microsoft SQL Server or Redis storage on Windows and Linux. It detects the separator used by the existing storage keys and reuses it without rewriting the keys. File storage is not affected by this change.

Before moving database storage between operating systems, [back up the storage](slug:storage-backup#manual-backup) and make the required [encryption keys](slug:security#encryption) available on the destination. Upgrade all Report Server Manager and Server Agent instances that share the storage to version 2026 Q4 (12.3.26.1125) or later.

If a database contains separate Windows and Linux entries, Report Server for .NET displays an **Invalid Storage State** page after sign-in. An administrator must choose which entries to keep. This operation permanently deletes the other entries and does not merge them. Scheduled tasks and data alerts do not run while the storage is invalid.

For the recovery steps and backup precautions, see [Using Report Server for .NET Database Storage Across Operating Systems](slug:cross-platform-database-storage-rs-net).
