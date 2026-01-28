---
title: Error Promise is undefined
description: Error "Promise" is undefined
type: troubleshooting
page_title: Error Promise is undefined
slug: error-promise-is-undefined
tags: promise,viewer
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
</table>

## Description

As of **Telerik Reporting R2 2017**, the Report Server and HTML5 Report Viewer require a browser supporting promises.The error indicates that the used browser does not support promises.

Please follow the [HTML5 Viewer: Important Settings](http://docs.telerik.com/reporting/html5-report-viewer-system-requirements#important-settings) article which contains the requirements for promises.

## Solution

Add a promise polyfill to the page, such as [Polyfill.io](https://polyfill.io/v2/docs/).
