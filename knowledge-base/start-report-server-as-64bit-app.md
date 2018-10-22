---
title: Start Telerik Report Server as 64-bit application
description: Describes how to start Telerik Report Server as a 64-bit application
page_title: How to start Telerik Report Server as a 64-bit application
slug: start-report-server-as-64bit-app
tags: iis,bitness,64bit,32bit
res_type: kb
---

## Environment

<table>
 <tr>
  <td>Product</td>
  <td>Progress® Telerik® Report Server</td>
 </tr>
 <tr>
  <td>Operating System</td>
  <td>Windows</td>
 </tr>
 <tr>
  <td>.Net framework</td>
  <td>Version 4.6</td>
 </tr>
</table>


## Description

The Report Server application is installed and configured to run in 32-bit mode by default (see [Installation](https://docs.telerik.com/report-server/implementer-guide/setup/installation) article) for compatibility reasons. To allow addressing more memory or using specific version of database drivers, the mode in which the Report Server is started may need to be changed.

## Solution

The mode in which the Report Server instance runs is determined by its application pool settings, which define it as a 32-bit application by default. 
To change it, navigate to the Report Server's application pool, open its *Advanced Settings* form and look for a *Enable 32-bit Applications* property. Change it to **False** to run the Report Server instance in 64-bit mode and recycle the pool.
