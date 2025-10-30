---
title: Export
page_title: Export
description: REST API Export
slug: rest-api-export-v2
tags: rest, api, rest api, overview
published: True
position: 300
---

# Export

To export a report, you need the ID of the report and know the document format in which it would be exported. The actual report export is achieved with two requests. The first request creates a document with the specified parameters and when the document is ready you can get it via a second, GET request.

> In order to perform report server operations, you have to login first and get an access token.

Here is a sample function to illustrate the approach:

## Example

```JavaScript
var serverHost = "http://reportserver:83/";
var serverApi = serverHost + "api/reportserver/v2/";

function exportDocument(reportId, format, parameterValues, asAttachment) {
	if (!reportId) {
		window.alert('Please, select a report.');
	}

	var data = {
		ReportId: reportId,
		Format: format,
		ParameterValues: parameterValues,
	};

	var token = window.sessionStorage.getItem(serverTokenKey);
	var headers = {};

	if (token) {
		headers.Authorization = 'Bearer ' + token;
	}

	$.ajax({
		type: "POST",
		url: serverApi + "documents",
		contentType: 'application/json',
		data: JSON.stringify(data),
		headers: headers
		})
		.done(function (data) {
		  var documentId = data;
		  var queryString = "";

		  if (asAttachment) {
			queryString += "content-disposition=attachment";
		  }

		  var exportUrl = serverApi + "documents/" + documentId + "?" + queryString;
		  window.open(exportUrl);
		})
		.fail(onError);
}
```

The described function can be used in the following way:

```HTML
<input type="button" value="Download in XLSX format" onclick="exportDocument('160945-e651', 'XLSX', { 'OrderNumber' : 'SO51115' }, true);" />
```

> With the _content-disposition_ query parameter you can control whether to download the document as a file or open it directly into the browser window.
