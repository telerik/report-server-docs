---
title: Login
page_title: Login
description: Report Server REST API Login
slug: rest-api-login
tags: rest, api, rest api, login
published: True
position: 100
---

# Report Server REST API Login

In order to perform operations with the Report Server you have to authenticate first. This can be done by sending a request to the *Token* endpoint with your credentials and as result get an access token. Here is a sample code snippet which demonstrates how to get the token:

```javascript
  var serverHost = "http://reportserver:83/";
  var serverApi = serverHost + "api/reportserver/";

  function login(username, password) {
  
    var accessToken = "";
  
    $.ajax({
      type: "POST",
      url: serverHost + "Token",
      async: false,
      data: {
        grant\_type: "password",
        username: username,
        password: password
      }
    })
    .done(function (data, textStatus, jqXHR) {
      accessToken = data.access\_token;
    })
    .fail(function (xhr, status, error) {
      window.alert(xhr.status + ": " + error);
    });
    
    return accessToken;
  }
```

Once you get the access token, you can store it in [window.sessionStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/sessionStorage) and later use it in subsequent requests.

For example:

```javascript
  var serverTokenKey = "TelerikReportServerToken";

  $(document).ready(function () {
    var accessToken =
      login("telerik", "telerik");
    window.sessionStorage.setItem(serverTokenKey, accessToken);
  }
``` 

To use the “anonymous” user you have to first enable it from the Report Server management application. 
In order to log in as an anonymous user you have to pass for the username and the password empty strings.
