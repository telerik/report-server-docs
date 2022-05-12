---
title: Add More Formatting Options to the Mail Templates
description: How to add more formatting options to the mail templates
type: how-to
page_title: Add More Formatting Options like FontName to the Mail Templates Toolbars
slug: add-more-formatting-options-to-mail-templates
position: 
tags: 
ticketid: 1539934
res_type: kb
---

## Environment
<table>
	<tbody>
		<tr>
			<td>Product</td>
			<td>Progress® Telerik® Report Server</td>
		</tr>
	</tbody>
</table>


## Description 

The Report Server has limited formatting options in its Mail Templates. This article elaborates on how you may add more of them. 

The Mail Templates are [Kendo Editors](https://demos.telerik.com/kendo-ui/editor/index). They are set up in the CSHTML templates that get deployed with the Report Server.

## Solution 

The CSHTML templates can be found in the installation folder of the Report Server product, for example, `C:\Program Files (x86)\Progress\Telerik Report Server\Telerik.ReportServer.Web\Views\Shared`. 
The files are `_LocalUsersMailTemplate.cshtml` and `_ExternalUsersMailTemplate.cshtml`. The setup of the Kendo Editors in these files includes a limited number of options 
that can be increased to enlarge the available formatting functionality when needed. For example, if you would like to be able to select 'FontName', you need to add 
the `fontName` option as it is absent by default. Here is the relevant part of the CSHTML script for the `_ExternalUsersMailTemplate.cshtml` file: 

````HTML
<script id="externalUsersMailTemplateEditorTemplate" type="text/x-kendo-template">
    <textarea id='externalUsersMailTemplateBodyInput'
              data-role='editor'
              data-messages='{ insertHtml: "variables" }'
              data-tools="[
                'bold',
                'italic',
                'underline',
                'justifyLeft',
                'justifyCenter',
                'justifyRight',
                'viewHtml',
                'fontSize',
                'fontName',
                 {
                    name  : 'insertHtml',
                     items : [
                        #params# ]
                 },
              ]"
              data-bind='value: ExternalUsersMailTemplate.Body'></textarea>
</script>
````

