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

Before migrating the Report Server or Server Agent applications on another operating system, [back up the storage](slug:storage-backup#manual-backup) and make the required [encryption keys](slug:security#encryption) available on the destination. Upgrade all Report Server Manager and Server Agent instances that share the storage to version 2026 Q4 (12.3.26.1125) or later.

Report Server versions earlier than 2026 Q4 (12.3.26.1125) write the storage keys in a format that depends on the operating system. When you move Report Server to another operating system but keep the same database storage, the application cannot read the existing storage entries. As a result, Report Server treats the storage as empty and redirects users to the Register Administrator page. If you complete the registration, Report Server creates a second set of entries in the storage and keeps the original entries. A storage that contains entries created on both Windows and Linux is in an invalid storage state.

In Report Server for .NET 2026 Q4 (12.3.26.1125) and later, every user who signs in to a storage in an invalid state is redirected to the **Invalid Storage State** page:

* Administrators can review the users and reports of the Windows and the Linux storage entries, and select which entries to keep.
* All other users see a message to contact their administrator. Sign-in is disabled until the storage is repaired.

While the storage is invalid, the Server Agent does not run scheduled tasks and data alerts.

For the recovery steps and backup precautions, see [Using Report Server for .NET Database Storage Across Operating Systems](<slug:cross-platform-database-storage-rs-net>).
