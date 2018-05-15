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

Telerik Report Server supports localization of the Standalone Report Designer when used with ClickOnce deployment.

To add support for languages with the Report Server, copy the required Report Designer resources in 

[Telerik Report Server Installation Directory]**\Telerik.ReportServer.Web\Report Designer\Languages\**[culture name]

For example: 

**C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web\Report Designer\Languages\de-DE**

To start the designer in specific language set the **Report Server -> Configuration -> Designer -> Preferred Language** setting. The drop down lists all languages available in the report server languages directory specified above.

The preferred language setting will be applied after connecting to the report server and if the user hasn't had specified language from the **Report Designer -> Options -> Language**.
