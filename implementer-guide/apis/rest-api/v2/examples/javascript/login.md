---
title: Login
page_title: Login
description: Report Server Login
slug: rest-api-login-v2
tags: rest, api, rest api, login
published: True
position: 100
---

# Login

In order to perform operations with the Report Server you have to authenticate first. This can be done by sending a request to the *Token* endpoint with your credentials and as result get an access token. 

Here is a sample code snippet which demonstrates how to login and get the token:

###### Example

	  var serverHost = "http://reportserver:83/";	  

	  function login(username, password) {
	  
		var accessToken = "";
	  
		$.ajax({
		  type: "POST",
		  url: serverHost + "Token",
		  async: false,
		  data: {
			grant_type: "password",
			username: username,
			password: password
		  }
		})
		.done(function (data, textStatus, jqXHR) {
		  accessToken = data.access_token;
		})
		.fail(function (xhr, status, error) {
		  window.alert(xhr.status + ": " + error);
		});
		
		return accessToken;
	  }

Once you get the access token, you can store it in [window.sessionStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/sessionStorage) and later use it in subsequent requests.

###### Example

	  var serverTokenKey = "TelerikReportServerToken";

	  $(document).ready(function () {
		var accessToken =
		  login("telerik", "telerik");
		window.sessionStorage.setItem(serverTokenKey, accessToken);
	  })

The [Guest]({%slug guest-user%}) user account does not need an authentication token to log in, therefore you cannot obtain a token when providing null or empty strings as login arguments. In this case a 1.1.400 Bad Request will be returned from the server.
