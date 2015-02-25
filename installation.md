---
title: Installation
page_title: Installation
description: Installation
slug: installation
tags: installation
published: True
position: 300
---

# System Requirements



The .zip archive contains the Report Server web application and the Standalone Report Designer executable.

The Report Server is a web application which is hosted on IIS. To setup the Report Server application follow these steps:

1. Unzip the contents of the .zip archive and copy the __Telerik.ReportServer.Web__ folder to a convenient for you location.
2. Open __Internet Information Services (IIS) Manager__. For more information see: [How to: Open IIS Manager](https://msdn.microsoft.com/en-us/library/bb763170%28v=vs.140%29.aspx)
3. In the __Connections__ pane expand the __Sites__ node.
4. Right-click the site in which you want to add the application and click __Add Application__.
5. In the __Alias__ text box type a name for the Report Server application, e.g. _telerikreportserver_. This name is used to access the application in a URL (e.g. _http://localhost/telerikreportserver_)
6. Click __Select… __to check the application pool settings. The application pool properties should read:  
_.Net Framework Version: 4.0._  
_Pipilene mode: Integrated_  
If the properties are different, choose an application pool from the dropdown list which has properties as the required ones.
7. In the __Physical path__ text box, type the full path to the __Telerik.ReportServer.Web__ folder. (e.g. _C:\inetpub\wwwroot\telerik.reportserver.web_) or click the browse (…) button to navigate to that folder.
8. Click __OK__.