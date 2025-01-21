---
title: Best Practices
page_title: Best Security Practices when Installing and Using Telerik Report Server
description: "Check the recommended security practices when installing the Telerik Report Server and working with its reports, users, and services."
slug: rs-security-best-practices
tags: telerik, reporting, report, server, security, best, practices
published: True
position: 4
---

# Security Best Practices

This article covers security practices that are generally applicable to web applications, as well as those specific to Telerik Report Server. The recommendations below should be regarded as a security guidance that ensures your information stored in Telerik Report Server is protected and safe. We recommend consulting with a specialist to provide further assistance on web application safety.

## Configuration Settings

Following the recommendations in this section is a responsibility of the implementer who deploys and configures the Telerik Report Server. These recommendations pertain to general security settings for web applications deployed on Windows IIS Servers. Following the principle "safe-by-default", the product installer and the initial setup workflow will configure Telerik Report Server using the safest options where possible. All of the items listed below can be configured through the web application's registration in IIS, or through the product's Configuration page:

* Configure your Report Server instance to run under [HTTPS protocol](https://developer.mozilla.org/en-US/docs/Glossary/HTTPS). Consider the advice in the article [Configuring IIS Website to Work Over HTTPS]({%slug configuring-iis-website-to-work-over-https%}).
* Let the user with lowered permissions in IIS and Report Server ServiceAgent be your preferred choice. By default, the MSI installer suggests applying the [principle of least privilege](https://learn.microsoft.com/en-us/entra/identity-platform/secure-least-privileged-access) and creating a dedicated Windows user named __ReportServerUser__ whose identity will be used by both applications. The user is granted the minimum necessary permissions to operate within the installation folder of Telerik Report Server as explained in [Report Server Installation]({%slug installation%}). 
* Disable the [CORS]({%slug cors%}) if possible; or enable CORS only for trusted hosts.
* Use the [Encryption]({%slug security%}#encryption) functionality of the Report Server to keep your assets safer.
* Consider the [Rate Limiting]({%slug security%}#rate-limiter) in your Report Server to restrict the network traffic and prevent bad agents from exhausting system resources.

## Working with Report Server Assets

After successfully installing and configuring the Telerik Report Server, the user with sufficient rights, for example, the admin user and those with granted permissions for the corresponding resources, may further enhance its security through the administration policy options provided by the server. Check the article section [Manage Permissions]({%slug users%}#manage-permissions) for the available access modes, scopes, and targets you may provide to Report Server Users. The built-in user roles are listed in the article [User Roles]({%slug user-roles%}).

The admin user and the users with sufficient permissions may control access to all or part of the following Report Server resources:

* [Manage User Permissions]({%slug users%}#manage-user-permissions)
  Each Report Server User is responsible for the Resources in his/her control. 
* [Reports Management]({%slug reports-management%})
  Grant users access only to the Reports/Categories they need. Ensure they are entitled to access the corresponding data sources.
* [Data Connections Management]({%slug data-connections-management%})
  Ensure the Data Connections do not contain credentials. The identity used to connect to the database or web service should be with limited permissions.
* [Scheduled Tasks Management]({%slug tasks-management%})
* [Data Alerts Management]({%slug alerts-management%})

## Extending the Reporting Engine

Telerik Report Server lets you extend its built-in Reporting functionality with custom code, for example by introducing [Custom User Functions](https://docs.telerik.com/reporting/designing-reports/connecting-to-data/expressions/extending-expressions/user-functions), [Custom Aggregate Functions](https://docs.telerik.com/reporting/designing-reports/connecting-to-data/expressions/extending-expressions/user-aggregate-functions), [Event Handlers](https://docs.telerik.com/reporting/designing-reports/report-designer-tools/desktop-designers/standalone-report-designer/using-event-handlers-in-srd#add-event-handlers-to-reports-created-with-the-standalone-report-designer) and [ObjectDataSources](https://docs.telerik.com/reporting/designing-reports/connecting-to-data/data-source-components/objectdatasource-component/overview). The Reporting Engine invokes the custom functionality with reflection. The allowed assemblies should be whitelisted in the configuration file _TelerikReporting.config_ of the Report Server application as explained in the articles [assemblyReferences Element](https://docs.telerik.com/reporting/doc-output/configure-the-report-engine/assemblyreferences-element), [TypeReferences](https://docs.telerik.com/reporting/doc-output/configure-the-report-engine/typereferences-element), and [typeValidation](https://docs.telerik.com/reporting/doc-output/configure-the-report-engine/typevalidation-element). The entire responsibility for registering the custom assemblies and the security of their code is delegated to the developer.

Avoid the [Unsafe Code](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/unsafe-code) in your ObjectDataSource/User Function/Event Handlers' projects and their references.

>tip Use only trusted assemblies that are signed with a public key token (see [Assembly (CLI)](https://en.wikipedia.org/wiki/Assembly_(CLI))) and cannot be replaced when extending the Reporting functionality in your projects, avoiding remote code execution and other malicious actions.

Use the advice in the article [Telerik Reporting Security Best Practices](https://docs.telerik.com/reporting/security/security-best-practices) to keep your reports and data safer.

## See Also

* [Security Overview]({%slug security-overview%})
* [Security FAQ]({%slug security-faq%})
* [Introduction to Telerik Report Server]({%slug introduction%})
* [System Requirements]({%slug system-requirements%})
* [Telerik Reporting Security Best Practices](https://docs.telerik.com/reporting/security/security-best-practices)
