---
title: Configure the Report Rendering Engine
page_title: Configure the Report Rendering Engine
description: Configure the Report Rendering Engine
slug: configure-the-report-engine
tags: configuration,settings,config,rest,rendering
published: True
position: 800
---

# Configure the Report Rendering Engine

## Configuration File

The reports rendering engine is exercised from the Report Server instance in the following contexts:

- When generating live report preview and export from the Report Server manager or through a URL
- When exporting a report using the 'documents' Report Server WebApi endpoint
- When the report scheduling service executes a Scheduled Task or Data Alert

### Report Server for .NET Framework

The rendering engine can be fine-tuned using a dedicated configuration file, called **TelerikReporting.config**.
This file is automatically created on the server when it is started for the first time.

For the first two usages of the engine, the default location of this file is
_C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web\TelerikReporting.config_. The Report Server web application needs to be restarted manually in order to apply the changes.

For the report scheduling service usage the default location of the configuration file is
_c:\Program Files (x86)\Progress\Telerik Report Server\Services\TelerikReporting.config_. The **Telerik.ReportServer.ServiceAgent** windows service needs to be restarted manually in order to apply the changes.

Both files' content is not affected by Report Server upgrade installations.

#### XML Configuration Section

To become effective, open the **TelerikReporting.config** file and uncomment the TelerikReporting configuration section registration:

```XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <section name="Telerik.Reporting" type="{0}" allowLocation="true" allowDefinition="Everywhere" />
  </configSections>
  <Telerik.Reporting>
    <restReportService workerCount="3" clientSessionTimeout="15" reportSharingTimeout="0" />
  </Telerik.Reporting>
</configuration>
```

### Report Server for .NET

In the newer [Report Server for .NET](slug:report-server-net-overview), the rendering engine can be fine-tuned using a JSON-based configuration file called **TelerikReporting.json**, located at `C:\Program Files (x86)\Progress\Telerik Report Server .NET\Telerik.ReportServer.Web\config`(_default location_).

The **Telerik Report Server .NET** site needs to be manually restarted from the [IIS Manager](https://learn.microsoft.com/en-us/iis/get-started/getting-started-with-iis/getting-started-with-the-iis-manager-in-iis-7-and-iis-8) in order to apply the changes.

For scheduled tasks and data alerts, configure the service agent's `TelerikReporting.json`. Its default location is `C:\Program Files (x86)\Progress\Telerik Report Server .NET\Services\config\TelerikReporting.json`. Restart the corresponding .NET service agent after configuration changes. For a separately deployed agent, use its own application directory.

#### JSON Configuration Section

To become effective, open the **TelerikReporting.json** file and edit the `telerikReporting` section. Additional configuration options can be seen in the [Report Engine Configuration](https://docs.telerik.com/reporting/doc-output/configure-the-report-engine/overview) article.

```JSON
{
  "telerikReporting": {
    "restReportService": {
      "hostAppId": "TRS",
      "workerCount": 3,
      "reportSharingTimeout": 0,
      "clientSessionTimeout": 15
    }
  }
}
```

## Restricting Access to External Resources

Telerik Reporting introduced `IStrictResourceResolver` in the [2026 Q4 (20.3.26.1111)](https://www.telerik.com/support/whats-new/reporting/release-history/progress-telerik-reporting-2026-q4-(20-3-26-1111)) release. Both Report Server for .NET Framework and Report Server for .NET support configuration of this interface.

Implement `Telerik.Reporting.Interfaces.IStrictResourceResolver` to apply your application's rules to external report resources. Telerik does not provide a ready-to-use public implementation. The interface extends `IResourceResolver` without additional members; implement `Resolve(string resourceUri)`.

The existing interface handles selected references, including relative image paths. Absolute image locations and resources such as map tiles do not all pass through it. The strict interface covers external images, CSV/JSON sources, shapefiles, external stylesheets, and map resources across relative paths, absolute paths, UNC paths, and URLs.

Return resource bytes or an approved location to allow access. Return `null` to deny access without fallback to the original location. Report-source selection and data-provider connections remain separate responsibilities. Inline or embedded content does not necessarily require an external-resource lookup.

### Deploying the Resolver Assembly

Build your resolver against a Telerik Reporting version compatible with the installed Report Server. A .NET Standard 2.0 library can serve both editions when its dependencies support each host. Do not replace the host's Reporting assemblies with assemblies from a different runtime or release.

Copy the DLL and its required dependencies to each application that must use the policy. The following table lists the paths relative to the corresponding Report Server installation folder:

| Host | DLL destination | Engine configuration file |
| --- | --- | --- |
| .NET Framework web application | `Telerik.ReportServer.Web\bin` | `Telerik.ReportServer.Web\TelerikReporting.config` |
| .NET Framework service agent | `Services` | `Services\TelerikReporting.config` |
| .NET web application | `Telerik.ReportServer.Web` | `Telerik.ReportServer.Web\config\TelerikReporting.json` |
| .NET service agent | `Services` | `Services\config\TelerikReporting.json` |

The default installation roots are `C:\Program Files (x86)\Progress\Telerik Report Server` for .NET Framework and `C:\Program Files (x86)\Progress\Telerik Report Server .NET` for .NET. For separately deployed agents, use the equivalent paths in each agent's application directory.

Configure both the web application and every relevant service agent. The web application handles live previews and exports; service agents handle scheduled tasks and data alerts. Grant their process identities read access to the approved resource directory and deployed assemblies.

### Registering Through XML

In each Framework host's `TelerikReporting.config`, enable the `Telerik.Reporting` section registration and the section itself if they are commented out. Keep `configSections` as the first child of `configuration`. Merge the following settings without removing existing configuration:

```XML
<configuration>
  <configSections>
    <section name="Telerik.Reporting"
             type="Telerik.Reporting.Configuration.ReportingConfigurationSection, Telerik.Reporting"
             allowLocation="true" allowDefinition="Everywhere" />
  </configSections>
  <Telerik.Reporting>
    <typeReferences>
      <add typeName="StrictResourceResolver.TrustedResourceResolver"
           assemblyName="StrictResourceResolver" />
    </typeReferences>
    <processing validateReportPaths="true">
      <resourceResolver provider="custom">
        <parameters>
          <parameter name="typeName"
                     value="StrictResourceResolver.TrustedResourceResolver, StrictResourceResolver" />
          <parameter name="directory" value="C:\ReportingResources" />
          <parameter name="trustedImageUrl"
                     value="https://raw.githubusercontent.com/telerik/reporting-docs/master/report-items/images/" />
        </parameters>
      </resourceResolver>
    </processing>
  </Telerik.Reporting>
</configuration>
```

The example trusts the individual resolver type through `typeReferences`. Alternatively, trust the assembly by replacing that element with the following `assemblyReferences` element:

```XML
<assemblyReferences>
  <add name="StrictResourceResolver" />
</assemblyReferences>
```

### Registering Through JSON

In each .NET host's `config\TelerikReporting.json`, merge the following settings into the existing `telerikReporting` section:

```JSON
{
  "telerikReporting": {
    "typeReferences": [
      {
        "typeName": "StrictResourceResolver.TrustedResourceResolver",
        "assemblyName": "StrictResourceResolver"
      }
    ],
    "processing": {
      "validateReportPaths": true,
      "resourceResolver": {
        "provider": "custom",
        "parameters": [
          {
            "name": "typeName",
            "value": "StrictResourceResolver.TrustedResourceResolver, StrictResourceResolver"
          },
          { "name": "directory", "value": "C:\\ReportingResources" },
          {
            "name": "trustedImageUrl",
            "value": "https://raw.githubusercontent.com/telerik/reporting-docs/master/report-items/images/"
          }
        ]
      }
    }
  }
}
```

Alternatively, replace `typeReferences` with `assemblyReferences` inside the same `telerikReporting` section. The alternative trust registration is:

```JSON
{
  "assemblyReferences": [
    { "name": "StrictResourceResolver" }
  ]
}
```

### Applying the Resource Policy

Trust registration and resolver selection serve different purposes. `typeReferences` or `assemblyReferences` permits the custom code to load. The `processing.resourceResolver` element selects it through the `custom` provider and its assembly-qualified `typeName`. Trust registration alone does not activate the resolver. Keep type validation enabled.

The examples use the illustrative [Strict Resource Resolver sample](https://github.com/telerik/reporting-samples/tree/master/StrictResourceResolver). Its constructor accepts `directory` and `trustedImageUrl`. The custom provider excludes `typeName`, sorts remaining parameter names, and passes their values as positional string arguments.

Replace `C:\ReportingResources` with an existing absolute directory that both host identities can read, or configure an appropriate directory for each host. The sample permits local files beneath that directory and PNG images directly in the configured HTTPS folder. Subfolders and other URL locations remain denied by this sample policy.

These constructor parameters and rules belong to the sample, not the interface. Adapt your implementation to the resources your reports require. For the implementation and its behavior, refer to [Restricting Access to Report Resources](https://docs.telerik.com/reporting/knowledge-base/implementing-strict-resource-resolver).

Keep `validateReportPaths` enabled for report definitions. The strict interface does not supply a resource policy or automatically apply `validateReportPaths` and `externalReportPaths` to custom results.

Restart the web application and corresponding service agents after deployment and configuration changes. Verify approved and denied resources in both live reports and scheduled report execution. Existing `IResourceResolver` implementations remain supported; strict resolution is opt-in.

## Applicable settings

The applicable report generation engine settings can be found in the chapter [Telerik Reporting Configuration Section](https://docs.telerik.com/reporting/configuring-telerik-reporting).

## restReportService element settings

This specific element controls the online report preview and export functionality of the Report Server and is not applicable to the report scheduling service. The respective attributes are:

### workerCount

Optional integer attribute. Specifies the combined count of report rendering worker threads that render report documents
for the live report preview and export and for the 'documents' WebApi endpoint.

The default value is equal to the logical processors available on the server machine.

### clientSessionTimeout

Optional integer attribute. Specifies the value in minutes indicating how long a client report preview session
will be preserved in the service storage after the last interaction with the report content from this client.

The value must be greater than zero. The default value is 15 minutes.

### reportSharingTimeout

Optional integer attribute. Specifies the value in minutes indicating how long a rendered report document
from a client will be eligible for reuse for another client's request.

The value must be greater than or equal to zero. A zero value will prevent rendered report document reuse.
The default value is zero.

Changing this is _highly recommended_ for a user-intensive Report Server deployment.

## See Also

For related configuration guidance, refer to these resources:

* [Security Best Practices]({%slug rs-security-best-practices%})
* [Report Engine Configuration](https://docs.telerik.com/reporting/doc-output/configure-the-report-engine/overview)
* [Type References](https://docs.telerik.com/reporting/doc-output/configure-the-report-engine/typereferences-element)
* [Assembly References](https://docs.telerik.com/reporting/doc-output/configure-the-report-engine/assemblyreferences-element)
