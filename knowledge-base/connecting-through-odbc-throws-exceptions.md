---
title: Connecting through ODBC throws BadImageFormatException or shows "Architecture Mismatch" error message
description: Rendering a report that uses ODBC connection, throws BadImageFormatException or shows "The specified DSN contains an architecture mismatch between the driver and the application" error message.
type: troubleshooting
page_title: BadImageFormatException or "Architecture Mismatch" message when using ODBC connection
slug: 
position: 
tags: oracle,odbc
ticketid:
res_type: kb
---

## Environment
<table>
 <tr>
  <td>Product</td>
  <td>Progress® Telerik® Report Server </td>
 </tr>
 <tr>
  <td>Operating System</td>
  <td>Windows</td>
 </tr>
  <td>.Net framework</td>
  <td>Version 4.6</td>
 </tr>
</table>


## Description
When the Report Server application is running in 32-bit application pool and opens an ODBC connection that uses a 64-bit driver, ODBC Driver Manager throws either a BadImageFormatException (reproduced with Oracle driver) or shows "The specified DSN contains an architecture mismatch between the driver and the application" error message (reproduced with Progress® OpenEdge® driver). The same is valid also if the Report Server is running in 64-bit application pool and ODBC uses a 32-bit driver.

## Solution
If the correct version of database drivers is installed, then the Report Server's application pool should be set to run in different mode (32 or 64-bit). Report Server's application pool settings define it as a 32-bit application by default. To change it, navigate to the Report Server's application pool, open its *Advanced Settings* form and look for a *Enable 32-bit Applications* property. Change it to **False** to run the Report Server instance in 64-bit mode and recycle the pool.
