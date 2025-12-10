---
title: Implement Custom Login Provider
page_title: Implement a Custom Login Provider
description: Implement a Custom Login Provider For Single Sign-On Scenario
slug: custom-login-provider
tags: single sign-on,SSO,custom login provider,implementation
published: True
position: 8
---

# Implement a Custom Login Provider

Custom login provider takes place in a single sign-on scenario when the Report Server Manager needs to be accessed as a part of another web application - usually an enterprise web application or company business portal.

In these cases, the users that have already authenticated themselves against the company application, should not be forced to enter their credentials again to login in Report Server Manager.

Instead, they should be seamlessly logged in when the browser gets redirected to the Report Server URL from the calling web application (below mentioned as **client application**).

## Authentication workflow

When the user, already authenticated in client application, wants to access the Report Server Manager, the client application must send a POST request to a specific WebAPI endpoint and provide the user credentials as a list of claims.

To ensure that the data is secured, it must be signed with a X509Certificate, which will be verified on the Report Server side and if the provided user credentials are valid, the response to the POST request will return an authentication cookie that will be automatically appended to the subsequent requests when the browser is redirected to Report Server Manager address.

## Report Server Configuration

The users in the client application must have corresponding registered users in Report Server.

It is not necessary that their names match, but in this case a mapping should be done on the client side.

The properties specific to this login type are located in the **Custom Provider** group under **Authentication** tab:

- `Enabled` – determines if custom login is allowed.
- `Hash Algorithm` – determines the hash algorithm used to sign the user claims. The supported algorithms are MD5, SHA1, SHA256, SHA384 and SHA512.
- `X509 Certificate` – a Base64-encoded representation of the certificate used to sign the claims. The verification will be done using the public key, so setting a certificate with only a public key is sufficient. The most convenient way to obtain the Base64 string is to export the certificate from the store using the _Base-64 encoded X.509 (.CER)_ format.

## Authentication examples

The POST request that will return the authentication cookie can be performed in many ways. We have created a sample project named **CustomLoginApp** that shows how this task can be done on the client - using jQuery AJAX request, and on the server - using C# code and HttpClient instance.

The project also demonstrates how to instantiate the object containing the client claims, sign it, send it to the Report Server WebAPI endpoint and consume the response. The project can be downloaded from [this link](https://www.telerik.com/docs/default-source/devcraft-documentation/reporting/customloginexampleapp.zip?sfvrsn=c18f4365_2).

Below are shown the code snippets used in the example with explanations about the authentication workflow.

### The following code snippets shows how to perform the request using jQuery:

```JS
    function performLogin(customLoginData) {
        var endpointUrl = "http://reportserver.home.com:92/api/reportserver/customlogin"
        return $.ajax({
            type: "POST",
            contentType: "application/json",
            url: endpointUrl,
            data: JSON.stringify(customLoginData),
            xhrFields: {
                withCredentials: true
            },
            crossDomain: true,
            success: function (data, textStatus, jqXHR) {
                console.log('The user is logged in after successfully verified credentials and signature');
            },
            error: function (XMLHttpRequest, textStatus, errorThrown) {
                console.log(textStatus + ' ' + XMLHttpRequest.statusText + ' ' + XMLHttpRequest.responseText);
            }
        });
    }
```

The **customLoginData** argument is a JavaScript representation of the _Telerik.ReportServer.HttpClient.CustomLoginData_ class that contains the mandatory **nameIdentifier** claim and the signature obtained by signing the data.

In this example, the signing is performed in a single pass in a server-side method named _SignCustomLoginData_ that accepts an instance of _CustomLoginData_, signs it and returns the signed object instance:

```JS
    function createCustomLoginData() {
        var userName = "admin"; //the username is displayed here for demonstration purposes. In real-life scenario it should be obtained based on the currently authenticated user in the client application.

        return new Promise(function (resolve, reject) {
            var customLoginData = {
                claims: {
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": userName
                }
            };

            $.ajax({
                type: "POST",
                url: "@Url.Action("SignCustomLoginData", "Default")",
                data: { serializedCustomLoginData: JSON.stringify(customLoginData)},
                success: function (data, textStatus, jqXHR) {
                    var signedData = JSON.parse(data);
                    console.log('Successfully created and signed CustomLoginData object with signature ' + signedData.Signature);
                    resolve(signedData);
                },
                error: function (XMLHttpRequest, textStatus, errorThrown) {
                    reject('error: ' + textStatus)
                },
                dataType: "json"
            });
        });
    }
```

The sample implementation of the method _SignCustomLoginData_ looks like this:

```C#
    public ActionResult SignCustomLoginData(string serializedCustomLoginData)
        {
            var data = JsonConvert.DeserializeObject<CustomLoginData>(serializedCustomLoginData);

            var certificate = GetCertificate(); //method that will find and return the required X509 certificate from the store
            using (var csp = certificate.GetRSAPrivateKey())
            {
                //The sample implementation uses SHA1 hash algorithm.
                using (var hashAlgorithm = new SHA1Managed())
                {
                    byte[] hash = hashAlgorithm.ComputeHash(data.GetDataForSigning());
                    data.Signature = csp.SignHash(hash, HashAlgorithmName.SHA1, RSASignaturePadding.Pkcs1);
                }
            }

            return new JsonResult()
            {
                Data = JsonConvert.SerializeObject(data)
            };
        }
```

And the main method that would be called when the browser needs to be redirected to the Report Server URL would look like this:

```JS
    function loginJS() {
        createCustomLoginData()
            .then(function (data) {
                return performLogin(data);
            })
            .then(function () {
                window.location.href = "http://reportserver.home.com:92";
            })
            .catch(function (err) {
                console.log('error '+err.responseText);
            });
    }
```

### The following code snippets shows how to perform the request using server-side C# code:

```C#
    async Task<HttpResponseMessage> Login()
        {
            string reason = "";
            var endpointUri = new Uri("http://reporting81.telerik.com:83/api/reportserver/customlogin");
            var data = new CustomLoginData(ClaimTypes.NameIdentifier, "admin");
            SignCustomLoginData(data);

            using (var client = new HttpClient())
            {
                var response = await client.PostAsJsonAsync(endpointUri, data).ConfigureAwait(false);
                if (response.IsSuccessStatusCode)
                {
                    //Get response Set-Cookie
                    var cookieKey = ".AspNet.ApplicationCookie";
                    var appCookie = response.Headers.GetValues("Set-Cookie")?.FirstOrDefault(c => c.StartsWith(cookieKey));
                    if (null != appCookie)
                    {
                        var cookieValue = appCookie.Substring(appCookie.IndexOf("=") + 1);
                        var newCookie = new HttpCookie(cookieKey, cookieValue);

                        newCookie.Shareable = true;
                        newCookie.Domain = "telerik.com";
                        newCookie.Expires = DateTime.Now.AddMinutes(5);
                        newCookie.Path = "/";

                        HttpContext.Response.Cookies.Remove(cookieKey);
                        HttpContext.Response.SetCookie(newCookie);
                        return new HttpResponseMessage(System.Net.HttpStatusCode.OK);
                    }
                }
                else
                {
                    reason = await response.Content.ReadAsStringAsync();
                    System.Diagnostics.Trace.TraceError(reason);
                }
            }

            return new HttpResponseMessage(System.Net.HttpStatusCode.Unauthorized)
            {
                Content = new StringContent(reason)
            };
        }
```

The _Login()_ method creates an instance of _Telerik.ReportServer.HttpClient.CustomLoginData_, signs it and posts it to the Report Server endpoint. If the response is successful, the authentication cookie is inspected and a new cookie is added to the current _HttpContext.Response_.

> The browser will disable sending the cookie if the response and request domains are different, which makes this approach not suitable for all scenarios.

The _Login()_ method signs the _CustomLoginData_ instance using the following sample code:

```C#
      public void SignCustomLoginData(CustomLoginData data)
        {
            var certificate = GetCertificate(); //method that will find and return the required X509 certificate from the store
            using (var csp = certificate.GetRSAPrivateKey())
            {
                //The sample implementation uses SHA1 hash algorithm.
                using (var hashAlgorithm = new SHA1Managed())
                {
                    byte[] hash = hashAlgorithm.ComputeHash(data.GetDataForSigning());
                    data.Signature = csp.SignHash(hash, HashAlgorithmName.SHA1, RSASignaturePadding.Pkcs1);
                }
            }
        }

        static X509Certificate2 GetCertificate()
        {
            var personalStore = new X509Store(StoreName.My, StoreLocation.LocalMachine);
            personalStore.Open(OpenFlags.ReadOnly);

            var certSubject = "CN=myCertificate";
            var certificate = personalStore.Certificates
                                .OfType<X509Certificate2>()
                                .FirstOrDefault(c => c.Subject.Contains(certSubject));

            if (null == certificate)
            {
                throw new NullReferenceException(string.Format("A certificate with subject {0} was not found in the certificate store.", certSubject));
            }

            return certificate;
        }
```

The calling method that redirects to the Report Server if the POST request is successful would look like this:

```C#
    public ActionResult LoginServerSide()
        {
            var result = Login().Result;
            if (result.IsSuccessStatusCode)
            {
                return new RedirectResult("http://reporting81.telerik.com:83/Report/Index");
            }
            else
            {
                var error = string.Format("Status: {0}; Content: {1}", result.StatusCode, result.Content.ReadAsStringAsync().Result);
                System.Diagnostics.Trace.TraceError(error);
                return View("Index");
            }
        }
```

## Certificate requirements

- The current implementation of the custom login method uses certificates whose keys implemet [RSACryptoServiceProvider](https://docs.microsoft.com/en-us/dotnet/api/system.security.cryptography.rsacryptoserviceprovider?redirectedfrom=MSDN&view=netframework-4.6.2) as the default RSA algorithm. Using certificates with keys implementing a different assymetric algorithm is not currently supported.
- Ensure that the certificate has defined the proper permissions to the applications and identities that use it. Usually the IUSR identity needs to have a certificate permission in order to use its private key for signing. [This forum topic](https://stackoverflow.com/questions/45042108/privatekey-threw-an-exception-of-type-system-security-cryptography-cryptographic) explains some of the possible issues in details.
