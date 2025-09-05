---
title: Whitelabeling
page_title: Whitelabeling in the Report Server for .NET
description: "Learn about the specifics of what is supported in the new Whitelabeling functionality in the Report Server for .NET, and how each setting is applied to the Report Server Manager and Web Report Designer."
slug: dotnet-server-whitelabeling
tags: whitelabeling,report,server,.net,color,logo,favicon
published: True
position: 6
---

<style>
	li img {
      width: 75% !important;
	}
</style>

# Overview

Our product supports white-labeling, allowing customers to personalize the visual identity of their instance. This feature enables organizations to align the product's appearance with their brand guidelines.
Whitelabeling enables the **Report Server for .NET's** customers to remove branding elements in the Report Server Manager web application and its internal Web Report Designer.

By replacing the default colors, logo, and favicon with branding from the customer's enterprise, you can personalize the visual identity of each Report Server. This feature enables organizations to align the product's appearance with their brand guidelines.

### Customizable Elements

The following elements can be rebranded:

* Colors - Accent Color, Selected Color, and Link Color.

	![The Report Server Manager and Web Report Designer color settings that are configurable](../images/rs-net-images/rs-net-whitelabeling-colors.png)

* Logo - The logo image should be in PNG, GIF, or JPG file format and have a height of 45 pixels or less.

	![The Report Server Manager Logo](../images/rs-net-images/rs-net-whitelabeling-logo.png)

* Favicon - The favicon should be in ICO, PNG, GIF, or JPG file format.

	![The Report Server Manager Favicon](../images/rs-net-images/rs-net-whitelabeling-favicon.png)

#### Report Server Manager

![Overiew of the Report Server for .NET with changed colors](../images/rs-net-images/rs-net-whitelabeling-manager-applied.png)

####  Web Report Designer

![Overview of the internal Web Report Designer with changed colors](../images/rs-net-images/rs-net-whitelabeling-web-designer-applied.png)

### Configuration

The whitelabeling feature can be found under **Configuration > Whitelabeling**. 
Administrator rights are required to access the Report Server Configuration page.

![All of the available Whitelabeling settings in the Report Server for .NET Configuration](../images/rs-net-images/rs-net-whitelabeling-all-settings.png)

## See Also

* [Report Server for .NET Overview]({%slug coming-soon%})
* [Whitelabeling in the Report Server for .NET Framework]({%slug whitelabeling%})
