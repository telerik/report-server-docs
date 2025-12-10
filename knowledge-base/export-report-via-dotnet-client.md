---
title: How to export a report from Telerik Report Server via .NET Client
description: How to export a report from Telerik Report Server via .NET Client
type: how-to
page_title: How to export a report from Telerik Report Server via .NET Client
slug: export-report-via-dotnet-client
tags: export,api,net
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

Telerik Report Server provides a [REST API](slug:rs-v2-api-reference) which can be used to consume resources from an external application. How to communicate with the REST API using a JavaScript client is demonstrated in:

- [Login](slug:rest-api-login)
- [Resources](slug:rest-api-get-resources)
- [Export](slug:rest-api-export)

The purpose of this article is to provide a demonstration of the same functionality but using a .NET client.

## Solution

The same JavaScript client can be written as a .NET client that executes requests and handles their responses. The following example illustrates how to send requests to the Report Server API and ultimately export a report to a report document.

```C#
    using Newtonsoft.Json.Linq;
    using System;
    using System.Collections.Generic;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Threading.Tasks;

    namespace GetAndExportReportFromRSWebApi
    {
        class Program
        {
            static readonly string reportServerUrl = "http://localhost:83/";
            static readonly string reportServerApiUrl = reportServerUrl + "api/reportserver/";
            static readonly string username = "yourUsername";
            static readonly string password = "yourPassword";

            static void Main(string[] args)
            {
                var reportName = "Dashboard";
                var parameters = new { ReportYear = 2004 };
                var format = "PDF";

                CreateAndDownloadReportDocument(reportName, parameters, format).Wait();
            }

            static async Task CreateAndDownloadReportDocument(string reportName, object parameters, string format)
            {
                using (var client = new HttpClient())
                {
                    client.BaseAddress = new Uri(reportServerApiUrl);
                    client.DefaultRequestHeaders.Accept.Clear();
                    client.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

                    // Authenticate via OAuth 2.0 Password Grant.
                    var authToken = GetAuthenticationToken(client, username, password);
                    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", authToken);

                    // List all reports.
                    var reports = await GetAllReports(client, reportServerApiUrl);

                    // Render the desired report.
                    var report = reports.Find(r => r["Name"].Equals(reportName))["Id"];
                    var documentUrl = await CreateDocument(client, reportServerApiUrl, format, report, parameters);

                    // Download the created document.
                    var downloadPath = DownloadDocument(documentUrl, reportName, false);

                    // Open the document.
                    System.Diagnostics.Process.Start(downloadPath);
                }
            }

            static string GetAuthenticationToken(HttpClient client, string usernameInput, string passwordInput)
            {
                var data = new FormUrlEncodedContent(new[]
                {
                    new KeyValuePair<string, string>("grant_type", "password"),
                    new KeyValuePair<string, string>("username", usernameInput),
                    new KeyValuePair<string, string>("password", passwordInput)
                });

                // POST Token
                    var response = client.PostAsync(reportServerUrl + "Token", data).Result;
                    response.EnsureSuccessStatusCode();

                    var result = response.Content.ReadAsStringAsync().Result;
                    var token = JObject.Parse(result).SelectToken("access_token").ToString();

                    return token;
                }

                static async Task<List<Dictionary<string, string>>> GetAllReports(HttpClient client, string apiUrl)
                {
                    // GET api/reportserver/reports
                    var response = await client.GetAsync(apiUrl + "reports");

                    if (response.IsSuccessStatusCode)
                    {
                        return await response.Content.ReadAsAsync<List<Dictionary<string, string>>>();
                    }

                    return null;
                }

                static async Task<string> CreateDocument(HttpClient client, string apiUrl, string format, string reportId, object parameterValues)
                {
                    var data = new { ReportId = reportId, Format = format, ParameterValues = parameterValues };
                    // POST api/reportserver/documents
                    var response = await client.PostAsJsonAsync(apiUrl + "documents", data);
                    response.EnsureSuccessStatusCode();

                    var documentUrl = response.Headers.Location;

                    return documentUrl.ToString();
                }

                static string DownloadDocument(string url, string reportName, bool asAttachment)
                {
                    var queryString = asAttachment ? "?content-disposition=attachment" : "";
                    var fileName = reportName + ".pdf";
                    var folderName = System.IO.Path.GetTempPath();
                    var filePath = System.IO.Path.Combine(folderName, fileName);

                    using (var webClient = new System.Net.WebClient())
                    {
                        webClient.DownloadFile(url + queryString, filePath);
                    }

                    return filePath;
                }
            }
        }
```
