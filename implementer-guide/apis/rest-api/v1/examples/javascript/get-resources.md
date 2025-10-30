---
title: Resources
page_title: Resources
description: Get Report Server Resources
slug: rest-api-get-resources
tags: rest, api, rest api, resources
published: True
position: 200
---

# Resources

Get Reports, Categories, and other resources.

> In order to perform report server operations, you have to login first and get an access token.

Here is a sample code snippet which illustrates how to read the report catalog items from the report server:

## Example

```JavaScript
var token = window.sessionStorage.getItem(serverTokenKey);
var headers = {};

if (token) {
	headers.Authorization = 'Bearer ' + token;
	}

var serverHost = "http://reportserver:83/";
var serverApi = serverHost + "api/reportserver/v1/";

$.ajax({
		type: "GET",
		url: serverApi + "reports",
		headers : headers
	  })
	.done(function (reports, status, xhr) {
		var length = reports.length;
		var reportNames = "";
		for (var i = 0; i &lt; length; i++) {
		  reportNames += (reports[i].Name + "\r\n")
		}
		window.alert(reportNames);
	  })
	.fail(function (xhr, status, error) {
		window.alert(xhr.status + ": " + error);
	});
```

You can get the report categories and the other report server resources such as scheduled tasks, data alerts, data connections, etc. in the same way just by changing the request url.

For example: _serverApi + "categories"_ to get report categories, _serverApi + "dataconnections"_ to get data connections, etc.
