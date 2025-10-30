---
title: Optimize MsSqlServer Storage
description: "Learn how to investigate what assets take most space in your MSSQL Server Storage and how to delete the unnecessary ones."
type: troubleshoot
page_title: Investigate and Optimize Report Server MsSqlServer Storage
meta_title: Investigate and Optimize Report Server MsSqlServer Storage
slug: optimize-report-server-mssql-server-storage
tags: report-server, mssql, server, storage, troubleshoot
res_type: kb
ticketid: 1699496
---

## Environment

<table>
   <tbody>
      <tr>
         <td>Product</td>
         <td>Report Server</td>
      </tr>
   </tbody>
</table>

## Problem

The MSSQL Server Database that I use as Storage for my Report Server became very large. Apart from taking a lot of space on the server machine, this seems to significantly decrease the performance of my Report Server.

## Description

The [Report Server Storage]({%slug storage-settings%}) contains two major parts:

* The __TRS__ part, short for 'Telerik Report Server'. It stores the actual Report Server assets like _report definitions_; _users_; _data connections_, etc.
* The __{GUID}\{Telerik Reporting Version}__, for example __d4b7948f\19.2.25.1001__ part. This is the [embedded Telerik Reporting REST Service Storage](https://docs.telerik.com/reporting/embedding-reports/host-the-report-engine-remotely/rest-service-storage/overview) assets that keep the state of the clients/viewers that connect to the Report Server and use it as a service for delivering report documents.

The REST Service part keeps temporary assets that are needed only when communicating with the corresponding client/viewer. When the client expires, for example, when a user of a Report Viewer closes the browser tab with the viewer, the corresponding assets expire and the REST Service schedules them for removal - see the blog [Telerik Reporting REST Service Storage Revealed](https://www.telerik.com/blogs/telerik-reporting-rest-service-storage-revealed) for details.

In some scenarios, the REST Service Storage may not be cleaned, with its expired assets piling up, taking up unnecessary space. The most popular scenarios are:

* Stop/Restart of the Report Server. In such cases, the REST Service may not have yet deleted the expired assets.
* Upgrade of the Report Server. In this scenario, the part of the storage responsible for the REST Service assets obtains a new identifier corresponding to the new Reporting version. The old part remains, although unnecessary.

## Troubleshooting

When using MSSQL Database Server Storage, you may use the following SQL script to figure out the amount of space taken by the different Report Server assets. You may execute it in the MSSQL Management Studio against your database used as Report Server Storage:

````SQL
select 'AppLock' as TableName, 'RS' as Application, count(*) as RowsCount 
from tr_AppLock where left(Id, 3) = 'TRS'
union all
select 'AppLock' as TableName, 'Cache' as Application, count(*) as RowsCount 
from tr_AppLock where left(Id, 3) <> 'TRS' 
union
select 'tr_Object', 'RS' as Application, count(*) 
from tr_Object where left(Id, 3) = 'TRS'
union all
select 'tr_Object', 'Cache' as Application, count(*) 
from tr_Object where left(Id, 3) <> 'TRS' 
union
select 'tr_Set', 'RS' as Application, count(*) 
from tr_Set where left(Id, 3) = 'TRS'
union all
select 'tr_Set', 'Cache' as Application, count(*) 
from tr_Set where left(Id, 3) <> 'TRS' 
union
select 'tr_String', 'RS' as Application, count(*) 
from tr_String where left(Id, 3) = 'TRS'
union all
select 'tr_String', 'Cache' as Application, count(*) 
from tr_String where left(Id, 3) <> 'TRS'
order by 1,2
````

The result returns the number of the _TRS_ (required) assets as 'RS', and the number of Reporting REST Service (unnecessary) assets as 'Cache'.

## Solution

* Track down the {GUID} and {Telerik Reporting Version} and use code like the following to delete the temporary REST Service assets. For example, if we use the above values 'd4b7948f' for the GUID and '19.2.25.1001' for the Reporting version, here is a sample SQL code:

	````SQL
delete from tr_object where left([Id], 21) = 'd4b7948f\19.2.25.1001'
	delete from tr_string where left([Id], 21) = 'd4b7948f\19.2.25.1001'
	delete from tr_set where left([Id], 21) = 'd4b7948f\19.2.25.1001'
````

	> There may be leftovers from previous Report Server versions. Ensure you also delete the old assets with identifiers corresponding to the old Report Server and Reporting version.

* Upon upgrade of the Report Server, use the following SQL script to remove the REST Service tables that don't need to be migrated:

	````SQL
truncate table tr_AppLock;
	truncate table tr_Object;
	truncate table tr_Set;
	truncate table tr_String;
````


* When upgrading the Report Server, you may also consider [Migrating its Storage with the tool we provide]({%slug migration-tool%}). The tool migrates only assets from the _TRS_ part of the storage and ignores the REST Service part. After a successful migration, you may delete the whole previous Report Server Storage.

## See Also

* [Welcome to Telerik® Report Server!]({%slug introduction%})
* [Report Server Storage]({%slug storage-settings%})
* [Storage Migration Tool]({%slug migration-tool%})
* [Reporting REST Service Storage](https://docs.telerik.com/reporting/embedding-reports/host-the-report-engine-remotely/rest-service-storage/overview)
* [Telerik Reporting REST Service Storage Revealed](https://www.telerik.com/blogs/telerik-reporting-rest-service-storage-revealed)
