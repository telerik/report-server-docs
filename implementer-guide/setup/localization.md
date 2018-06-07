---
title: Localization
page_title: Localization
description: Localization
slug: localization
tags: localization
published: true
position: 455
---

# Localization

## Localiza Standalone Report Designer

Telerik Report Server supports localization of the Standalone Report Designer when used with ClickOnce deployment.

To add support for languages with the Report Server, copy the required Report Designer resources in 

[Telerik Report Server Installation Directory]**\Telerik.ReportServer.Web\Report Designer\Languages\**[culture name]

For example: 

**C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web\Report Designer\Languages\de-DE**

To start the designer in specific language set the **Report Server -> Configuration -> Designer -> Preferred Language** setting. The drop down lists all languages available in the report server languages directory specified above.

The preferred language setting will be applied after connecting to the report server and if the user hasn't had specified language from the **Report Designer -> Options -> Language**.

## Localiza Telerik Report Server Web Application 
 
Telerik Report Server Web Application now support localization for its UI. To do that, there are a few steps that has to be done:

First, check Kendo UI for jQuery, if supports the language you want to translate. As the Report Server uses Progress Kendo UI framework for UI representation, read and make all needed changes, to localize the Kendo UI widgets, found in [Kendo UI for jQuery Documentation](https://docs.telerik.com/kendo-ui/framework/localization/overview).

Second, open the source code of the Telerik Report Server Web Application. Navigate to Scripts > ReportServer folder and find the sr.js and sr.user.js files. In sr.js you can find all texts used in the Report Server Web Application. Copy all of them, that you want to translate, into “sr” object in sr.user.js file. 

Finally, translate the texts, coped in the sr.user.js, for the specified culture.
