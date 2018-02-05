---
title: How to customize preview in Report Server
description: Customize styling for previewing Reports in Telerik Report Server
type: how-to
page_title: Customize styling for previewing Reports in Telerik Report Server
slug: how-to-customize-preview-in-report-server
position: 
tags: Preview
ticketid: 1151103
res_type: kb
---

## Environment
<table>
	<tr>
		<td>Product</td>
		<td>Progress® Telerik® Report Server</td>
	</tr>
</table>


## Description
The look of reports Preview in Telerik Report Server is customizable in the same way the Html5 Report Viewer is.
To achieve the desired appearance you could use a local/custom template for the ReportViewer, where to refer a custom/modified CSS file with appropriate ReportViewer styles.  
The template should be assigned to the 'templateUrl' property of the HTML5ReportViewer, as explained in [this collection of help articles](https://docs.telerik.com/reporting/html5-report-viewer-styling-and-appearance).
  
Here is a sample step-by-step guide:  
  
1\. Create **styles** folder in (_**Telerik Report Server** installation folder_)\\Telerik.ReportServer.Web\\ReportViewer and add file **telerikReportViewer.css** with the viewer styles. The default styling could be achieved with the following code:
```CSS
/*
* TelerikReporting v11.2.17.1025 (http://www.telerik.com/products/reporting.aspx)
* Copyright 2017 Telerik AD. All rights reserved.
*
* Telerik Reporting commercial licenses may be obtained at
* http://www.telerik.com/purchase/license-agreement/reporting.aspx
* If you do not own a commercial license, this file shall be governed by the trial license terms.
*/
.trv-pages-area .trv-error-pane{left:50%;position:relative;float:left;display:none;max-width:80%}
.trv-pages-area>.trv-error-pane>.centered{position:relative;float:left;left:-50%;padding:1em}
.trv-pages-area .trv-page-overlay{display:none;position:absolute;left:0;right:0;top:0;bottom:0;background-color:#fff;opacity:.6}
.trv-pages-area.loading .trv-page-overlay{display:block}
.trv-pages-area.error .trv-error-pane{display:block}
.trv-pages-area .trv-page-container{position:absolute;left:0;right:0;top:0;bottom:0;overflow:auto}
.trv-pages-area.printpreview .trv-page-container .trv-page-wrapper{margin:20px;text-align:center;position:relative}
.trv-pages-area.printpreview .trv-page-container .trv-page-wrapper .trv-report-page{border:2px solid #ccc;background-color:#fff;margin-left:auto;margin-right:auto;overflow:hidden;position:relative}
.trv-pages-area.printpreview .trv-page-container .trv-page-wrapper.active .trv-report-page{border:2px solid #ccc}
.trv-pages-area.interactive .trv-page-container .trv-page-wrapper{text-align:center;position:relative}
/*.trv-pages-area.interactive .trv-page-container .trv-page-wrapper .trv-report-page{background-color:#fff;overflow:hidden;position:relative;padding:1em}*/
/* THIS STYLE IS MODIFIED TO CENTER THE REPORT IN INTERACTIVE MODE*/
.trv-pages-area.interactive .trv-page-container .trv-page-wrapper .trv-report-page{background-color:#fff;margin-left:auto;margin-right:auto;overflow:hidden;position:relative;padding:1em}
.trv-pages-area.interactive .trv-page-container .trv-page-wrapper.active .trv-report-page{border:0}
.trv-pages-area-kendo-tooltip{font-size:.7em}
.trv-pages-area-kendo-tooltip-title{font-weight:700}
.trv-pages-area-kendo-tooltip-text{font-weight:400}.trv-parameter-container .trv-parameter-title{font-weight:700;width:100%;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.trv-parameters-area .trv-parameters-area-overlay{display:none;position:absolute;top:0;left:0;right:0;bottom:0;background-color:#fff;opacity:.6}
.trv-parameters-area.loading .trv-parameters-area-overlay{display:block}
.trv-parameter-container .trv-parameter-error{font-size:8pt}
.trv-parameters-area .trv-parameters-area-content{position:absolute;left:0;right:0;top:0;bottom:0;overflow:auto}
.trv-parameters-area .trv-parameters-area-footer{position:absolute;left:0;right:0;bottom:0;height:3em;display:none}
.trv-parameters-area.preview .trv-parameters-area-content{bottom:3em}
.trv-parameters-area.preview .trv-parameters-area-footer{display:block}
.trv-parameters-area .trv-error-pane{position:absolute;width:100%;top:0;left:0;display:none}
.trv-parameters-area.error .trv-error-pane{display:block}
.trv-parameters-area .trv-parameters-area-preview-button{position:absolute;top:.5em;left:.4em}
.trv-parameters-area-preview-button.k-state-disabled:hover{background-color:transparent!important}
.trv-parameters-area .trv-parameter-container{margin:.3em;margin-bottom:10px;padding:.1em}
.trv-parameter-title{}
.trv-parameter-header{width:100%;position:relative}
.trv-parameter-error{padding:3px;margin-bottom:3px}
.trv-parameter-value{}
.trv-parameter-error-message{vertical-align:middle}
.trv-parameter-editor-available-values-multiselect{}
.trv-parameter-editor-available-values-multiselect .list{overflow:auto}
.trv-parameter-editor-available-values-multiselect .footer{font-size:8pt}
.trv-parameter-editor-available-values-multiselect .select-all{}
.trv-parameter-editor-available-values-multiselect .select-none{}
.trv-parameter-editor-available-values{}
.trv-parameter-editor-available-values .footer{font-size:8pt}
.trv-parameter-editor-datetime{width:100%}
.trv-parameter-editor-text{width:100%}
.trv-parameter-editor-number{width:100%}
.trv-parameter-editor-multivalue textarea{width:100%;resize:none}.trv-report-viewer{position:relative;width:100%;height:100%;overflow:hidden}
.trv-side-menu{overflow:auto;position:absolute;top:0;bottom:0;left:0;display:none}
.trv-side-menu>ul{border-right:0 none transparent}
.trv-side-menu li>a{border-bottom:0 none transparent!important}
.trv-side-menu span{margin-left:1em}
.trv-side-menu a{background-image:none!important}
.trv-report-viewer div.trv-content-wrapper{display:-ms-flexbox;display:flex;-ms-flex-direction:column;flex-direction:column;height:100%;position:absolute;left:0;right:0;top:0;bottom:0;transition:100ms}
.trv-nav{-ms-flex:0 1 auto;flex:0 1 auto}
.trv-nav a{color:inherit}
.trv-nav>ul{position:relative}
.trv-nav li{border-width:0!important;border-style:none!important}
.trv-nav input{width:2em;height:99%}
.trv-content{position:relative;-ms-flex:1 1;flex:1 1 0;height:100%;margin-top:-1px}
.k-ie9 .trv-content{position:absolute;margin-top:1px;top:2.5em;bottom:0;left:0;right:0;height:auto}
.trv-menu-large{display:block;border-style:none}
.trv-menu-large .k-item>.k-link>.k-icon{margin:-8px 0 0}
.trv-menu-small{display:none;border-style:none}
.k-ie9 .trv-menu-small .k-link,.k-ie9 .trv-menu-large .k-link{white-space:nowrap}
.trv-document-map{position:absolute;width:15em;height:auto;top:0;bottom:0;left:0;z-index:10}
.trv-document-map>div{position:absolute;top:0;left:0;right:0;bottom:0}
.trv-document-map .trv-document-map-overlay{display:none;background:#fff;opacity:.6;z-index:100000}
.trv-document-map.loading .trv-document-map-overlay{display:block}
.trv-document-map.hidden{display:none}
.trv-parameters-area{position:absolute;width:15em;height:auto;top:0;bottom:0;right:0;z-index:10}
.trv-parameters-area.hidden{display:none}
.trv-pages-area{position:absolute;height:auto;top:0;bottom:0;left:15.3em;right:15.3em}
.trv-parameters-area.hidden~.trv-pages-area
{right:0}
.trv-document-map.hidden~.trv-pages-area
{left:0}
.trv-error-pane{padding:1em;font-size:.7em}
.trv-report-viewer input[type=number]::-webkit-inner-spin-button,.trv-report-viewer input[type=number]::-webkit-outer-spin-button{-webkit-appearance:none;margin:0}
.trv-report-viewer input[type=number]{-moz-appearance:textfield}
@media screen and (max-width:28.75em){}
@media screen and (min-width:1px) and (max-width:40.5em){.trv-side-menu{display:block;padding-top:.1em;left:-3em;transition:100ms}
.trv-side-menu-visible .trv-side-menu{left:0;width:15em;padding-left:0;transition:500ms}
.trv-side-menu-visible .trv-report-viewer div.trv-content-wrapper{left:15em;right:-15em;transition:500ms}
.trv-menu-large{display:none}
.trv-menu-small{display:block}
.trv-document-map{position:absolute;width:auto;top:0;left:0;right:0;bottom:0}
.trv-parameters-area{position:absolute;width:auto;top:0;left:0;right:0;bottom:0}
.trv-pages-area{position:absolute;width:auto;top:0;left:0;right:0;bottom:0}
.trv-nav{left:0;right:0}
.trv-parameters-area.hidden~.trv-pages-area{right:0}
.trv-document-map.hidden~.trv-pages-area
{left:0}}
/* DO NOT MODIFY OR DELETE THIS LINE! UPGRADE WIZARD CHECKSUM A811855349D889E9EAB1F1A8D36BE0CC */
```
Modify the appropriate styles to achieve the desired report appearance in the viewer.

2\. Create **templates** folders in (_**Telerik Report Server** installation folder_)\\Telerik.ReportServer.Web\\ReportViewer and add file **telerikReportViewerTemplate.html** - the report viewer template. The default template code looks like:
```HTML
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
	<title>Telerik HTML5 Report Viewer Templates</title>

	<!--Telerik served resources. For more information see: http://docs.telerik.com/reporting/html5-report-viewer-styling-and-appearance -->
	<link href="{service}resources/font/fonticons-css" rel="stylesheet" />
	<!--<link href="{service}resources/styles/telerikReportViewer-css" rel="stylesheet" />-->
  <!--THE FOLLOWING CODE REFERS THE JUST CREATED LOCAL CSS STYLES -->
	<link href="/ReportViewer/styles/telerikReportViewer.css" rel="stylesheet" />

    <script type="text/javascript">
        //IE9 fix
        if (document.documentMode && document.documentMode < 10) {
            $(".trv-content")[0].style.top = $(".trv-nav").height() + "px";
        }
    </script>
</head>
<body>
	<template id="trv-parameter">
		<div class='trv-parameter-container k-content'>
			<div class='trv-parameter-header k-header'>
				<div class='trv-parameter-title'></div>
			</div>
			<div class='trv-parameter-error k-tooltip-validation k-widget'>
				<span class='k-icon k-warning'></span>
				<span class='trv-parameter-error-message'></span>
			</div>
			<div class='trv-parameter-value'></div>
		</div>
	</template>

	<template id="trv-parameter-editor-available-values-multiselect">
		<div class="trv-parameter-editor-available-values-multiselect">
			<div class="list" id="parameter-editor-multiselect-list"></div>
			<div class="footer">
				<a class="select-all k-link" href="#">select all</a>
				<a tabindex="-1" class="select-none k-link" href="#">clear selection</a>
			</div>
		</div>
	</template>

	<template id="trv-parameter-editor-available-values">
		<div class="trv-parameter-editor-available-values">
			<div class="list" id="parameter-editor-singleselect-list"></div>
			<div class="footer">
				<a tabindex="-1" class="select-none k-link" href="#">clear selection</a>
			</div>
		</div>
	</template>

	<template id="trv-parameter-editor-datetime">
		<input type="datetime" class="trv-parameter-editor-datetime" />
	</template>

	<template id="trv-parameter-editor-text">
		<input type="text" class="k-textbox trv-parameter-editor-text" />
	</template>

	<template id="trv-parameter-editor-number">
		<input type="number" step="any" class="k-textbox trv-parameter-editor-number" />
	</template>

	<template id="trv-parameter-editor-boolean">
		<input type="checkbox" class="trv-parameter-editor-boolean" />
	</template>

	<template id="trv-parameter-editor-multivalue">
		<div class="trv-parameter-editor-multivalue">
			<textarea class="k-textbox"></textarea>
		</div>
	</template>

	<template id="trv-report-viewer">
		<div class="trv-report-viewer">
			<div tabindex="3" class="trv-side-menu k-content" data-role="telerik_ReportViewer_SideMenu">
				<ul tabindex="3" aria-label="SideMenu" id="side-menu">
					<li aria-label="Navigate Backward"><a data-command="telerik_ReportViewer_historyBack" title="Navigate Backward" href="#"><i class="t-font-icon t-i-undo"></i><span>Navigate Backward</span></a></li>
					<li aria-label="Navigate Forward"><a data-command="telerik_ReportViewer_historyForward" title="Navigate Forward" href="#"><i class="t-font-icon t-i-redo"></i><span>Navigate Forward</span></a></li>
					<li aria-label="Refresh"><a data-command="telerik_ReportViewer_refresh" href="#" title="Refresh"><i class="t-font-icon t-i-refresh-a"></i><span>Refresh</span></a></li>
					<li aria-label="Print"><a data-command="telerik_ReportViewer_print" title="Print" href="#"><i class="t-font-icon t-i-print"></i><span>Print...</span></a></li>
					<li aria-label="Export. Expandable" id="side-menu-export-command">
						<a title="Export" href="#" data-command="telerik_ReportViewer_export"><i class="t-font-icon t-i-download"></i><span>Export</span></a>
						<ul data-command-list="export-format-list"></ul>
					</li>
					<li aria-label="Toggle Print Preview"><a data-command="telerik_ReportViewer_togglePrintPreview" title="Toggle Print Preview" href="#"><i class="t-font-icon t-i-file"></i><span>Toggle Print Preview</span></a></li>
				</ul>
			</div>
			<div class="trv-content-wrapper k-content">
				<div class="trv-nav k-widget">
					<ul tabindex="1" aria-label="Main menu" class="trv-menu-large" data-role="telerik_ReportViewer_MainMenu" >
						<li><a data-command="telerik_ReportViewer_historyBack" title="Navigate Backward" href="#"><i class="t-font-icon t-i-undo"></i></a></li>
						<li><a data-command="telerik_ReportViewer_historyForward" title="Navigate Forward" href="#"><i class="t-font-icon t-i-redo"></i></a></li>

						<li><a data-command="telerik_ReportViewer_refresh" href="#" title="Refresh" ><i class="t-font-icon t-i-refresh-a"></i></a></li>

						<li><a data-command="telerik_ReportViewer_goToFirstPage" title="First Page" href="#"><i class="t-font-icon t-i-arrow-double-60-w"></i></a></li>
						<li><a data-command="telerik_ReportViewer_goToPrevPage" title="Previous Page" href="#"><i class="t-font-icon t-i-seek-w"></i></a></li>

						<li title="Page Number Selector" class="trv-report-pager">
							<input data-role="telerik_ReportViewer_PageNumberInput" type="number"/>
							<span>&nbsp;/&nbsp;</span>
							<span data-role="telerik_ReportViewer_PageCountLabel"></span>
						</li>

						<li><a data-command="telerik_ReportViewer_goToNextPage" title="Next Page" href="#"><i class="t-font-icon t-i-seek-e"></i></a></li>
						<li><a data-command="telerik_ReportViewer_goToLastPage" title="Last Page" href="#"><i class="t-font-icon t-i-arrow-double-60-e"></i></a></li>

						<li><a data-command="telerik_ReportViewer_togglePrintPreview" title="Toggle Print Preview" href="#"><i class="t-font-icon t-i-file"></i></a></li>

						<li id="main-menu-export-command">
							<a title="Export" href="#" data-command="telerik_ReportViewer_export"><i class="t-font-icon t-i-download"></i>&nbsp;</a>
							<ul data-command-list="export-format-list" id="mainmenu-export-format-list"></ul>
						</li>

						<li><a data-command="telerik_ReportViewer_print" title="Print" href="#"><i class="t-font-icon t-i-print"></i></a></li>

						<li><a data-command="telerik_ReportViewer_toggleDocumentMap" title="Toggle Document Map" href="#"><i class="t-font-icon t-i-book"></i></a></li>
						<li><a data-command="telerik_ReportViewer_toggleParametersArea" title="Toggle Parameters Area" href="#"><i class="t-font-icon t-i-filter"></i></a></li>

						<li><a title="Zoom In" href="#" data-command="telerik_ReportViewer_zoomIn"><i class="t-font-icon t-i-zoom-in"></i></a></li>
						<li><a title="Zoom Out" href="#" data-command="telerik_ReportViewer_zoomOut"><i class="t-font-icon t-i-zoom-out"></i></a></li>
						<li><a title="Toggle FullPage/PageWidth" href="#" data-command="telerik_ReportViewer_toggleZoomMode"><i class="t-font-icon t-i-zoom"></i></a></li>
					</ul>
					<ul tabindex="2" aria-label="Compact Menu" class="trv-menu-small" data-role="telerik_ReportViewer_MainMenu">
						<li><a data-command="telerik_ReportViewer_toggleSideMenu" title="Toggle Side Menu" href="#"><i class="t-font-icon t-i-reorder"></i></a></li>
						<li title="Page Number Selector" class="trv-report-pager">
							<input data-role="telerik_ReportViewer_PageNumberInput" type="number"/>
							<span>&nbsp;/&nbsp;</span>
							<span data-role="telerik_ReportViewer_PageCountLabel"></span>
						</li>
						<li><a data-command="telerik_ReportViewer_toggleDocumentMap" title="Toggle Document Map" href="#"><i class="t-font-icon t-i-book"></i></a></li>
						<li><a data-command="telerik_ReportViewer_toggleParametersArea" title="Toggle Parameters Area" href="#"><i class="t-font-icon t-i-filter"></i></a></li>
					</ul>
				</div>

				<div class="trv-content" role="form">
					<div class="trv-document-map k-widget hidden" data-role="telerik_ReportViewer_DocumentMapArea" >
						<div tabindex="200" class="trv-document-map-overlay" role="navigation" aria-label="Document map area"></div>
					</div>

					<div class="trv-parameters-area k-widget hidden" data-role="telerik_ReportViewer_ParametersArea" >
						<div tabindex="300" class='trv-parameters-area-content' role="complementary"></div>
						<div class='trv-parameters-area-footer'>
							<button tabindex="399" aria-label="Preview the report" class='k-button trv-parameters-area-preview-button'>Preview</button>
						</div>
						<div class='trv-error-pane k-tooltip-validation k-widget'>
							<div class='trv-error-message'></div>
						</div>
						<div class="trv-parameters-area-overlay"></div>
					</div>

					<div class="trv-pages-area k-widget" tabindex="1000" data-role="telerik_ReportViewer_PagesArea" role="main" aria-label="Report contents area">
						<div class='trv-page-container'>
							<div class='trv-page-wrapper active'></div>
						</div>
						<div class='trv-error-pane'>
							<div class="centered k-tooltip-validation k-widget">
								<div class='trv-error-message'></div>
							</div>
							<div style="clear: both;"></div>
						</div>
					</div>
				</div>

			</div>
		</div>
	</template>

    <template id="trv-pages-area-kendo-tooltip">
        <div class="trv-pages-area-kendo-tooltip">
            <div class="trv-pages-area-kendo-tooltip-title"></div>
            <div class="trv-pages-area-kendo-tooltip-text"></div>
        </div>
    </template>

</body>
</html>
<!-- DO NOT MODIFY OR DELETE THIS LINE! UPGRADE WIZARD CHECKSUM 3DC58F101DE7A0160F81A46F4459220C -->
```
3\. The viewer is configured in the _Preview.cshtml_ View file that could be found in the folder (_Telerik Report Server installation folder_)\\Telerik.ReportServer.Web\\Views\\Report (for example _C:\\Program Files (x86)\\Progress\\Telerik Report Server\\Telerik.ReportServer.Web\\Views\\Report_). Modify **Preview.cshtm** by setting **templateUrl** property of the ReportViewer:
```C#
.telerik_ReportViewer({
serviceUrl: '@Url.Content("~/api/reports/")',
// ADD THE FOLLOWING LINE TO REFER THE JUST CREATED CUSTOM TEMPLATE
templateUrl: '/ReportViewer/templates/telerikReportViewerTemplate.html',
reportSource: {
report: '@Model.ReportSource',
parameters: @Html.Raw(Json.Encode(Model.Parameters))
},
...........
});
```
4\. Restart the Report Server.
  

Do you want to have your say when we set our development plans?
Do you want to know when a feature you care about is added or when a bug fixed?
Explore the [Telerik Feedback Portal](http://www.telerik.com/support/feedback)
and vote to affect the priority of the items
