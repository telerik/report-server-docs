---
title: Embed in Another Application
page_title: Embed in Another Application
description: The article elaborates on embedding Telerik Report Server in another application
slug: embed-in-another-application
tags: embed,report server,iframe,subdomain
published: True
position: 820
---

# Embed in Another Application

The Report Server Manager is an ASP.NET MVC web application. A frequent business requirement in the organization is to access the Report Server Manager as a part of another web application - usually an enterprise web application or company business portal.

## Subdomain and Whitelabeling

One way to satisfy the organization requirements is to host the Report Server Manager on a subdomain. Step two is to style it in a similar manner
with [whitelabeling]({%slug whitelabeling%}). The final touch is to implement single sign-on (SSO) using a [custom login provider]({%slug custom-login-provider%}).

## Inline Frame <iframe>

Some may prefer to access the Report Server Manager application without having to switch browser tabs. For these cases embedding the Report Server in an **<iframe>** element might be a viable solution.
Embedding the Report Server Manager into an inline frame is disabled by default to prevent [clickjacking](https://en.wikipedia.org/wiki/Clickjacking) attacks. When this type of attack is not a concern (e.g. private networks) the setting can be modified using the **ReportServerAdmin.config** configuration file:

`````
<configuration>
  <configSections>
    <section name="reportServer" type="Telerik.ReportServer.Web.Configuration.ReportServerConfigurationSection, Telerik.ReportServer.Web" requirePermission="false" allowLocation="true" />
  </configSections>
  <reportServer>
    ...
    <antiForgery>
      <parameters>
        <parameter name="SuppressXFrameOptionsHeader" value="true" />
      </parameters>
    </antiForgery>
  </reportServer>
</configuration>
`````
