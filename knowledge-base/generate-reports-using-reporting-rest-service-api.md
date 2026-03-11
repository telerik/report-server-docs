---
title: Generate and Download Reports via the Reporting REST Service API
description: "Learn how to use the Telerik Reporting REST Service API to programmatically generate and download reports from the Report Server for .NET when the Report Server v2 API does not cover your scenario."
type: how-to
page_title: How to Generate and Download Reports Using the Reporting REST Service API
slug: generate-reports-using-reporting-rest-service-api
tags: report-server, rest-api, export, generate, download, reporting-rest-service, workaround
res_type: kb
---

## Environment

<table>
 <tbody>
  <tr>
   <td>Product</td>
   <td>Progress® Telerik® Report Server for .NET</td>
  </tr>
  <tr>
    <td>Version</td>
    <td>12.0.26.304</td>
  </tr>
 </tbody>
</table>

## Description

The [Report Server v2 API](slug:rs-v2-api-reference) is fully supported and feature‑complete in Report Server for .NET Framework. In Report Server for .NET (RS.NET), support for the v2 API is still in progress, as some of the endpoints are not exposed yet.

As a workaround, to programmatically generate and download report documents from RS.NET, you can use the [Reporting REST Service API](https://www.telerik.com/products/reporting/documentation/embedding-reports/host-the-report-engine-remotely/rest-api-reference/overview) at `/api/reports/`. This is the same API that the built-in report viewer uses internally to render reports.

## Solution

### Step 1 - Obtain a Bearer Token

The Report Server for .NET supports two authentication methods.

#### Option A - Username/Password (Legacy)

Request:

- Method: `POST`
- URL: `http://localhost:81/Token`
- Header: `Content-Type: application/x-www-form-urlencoded`
- Body (`x-www-form-urlencoded`):

```text
grant_type=password
username=YOUR_USERNAME
password=YOUR_PASSWORD
```

Response:

- Read `accessToken` from the JSON body.
- Use it as: `Authorization: Bearer ACCESS_TOKEN` for upcoming requests.

#### Option B - Personal Access Token (Recommended for RS.NET 2025 Q4+)

Starting with 2025 Q4 (version `11.3.25.1111`), users can create [Personal Access Tokens](slug:rs-net-token-authentication) from the Report Server Manager UI.

Request:

- Method: `POST`
- URL: `http://localhost:81/PersonalToken`
- Header: `Content-Type: application/json`
- Body:

```json
"YOUR_PERSONAL_ACCESS_TOKEN"
```

Response:

- Read `accessToken` from the JSON body.
- Use it as: `Authorization: Bearer ACCESS_TOKEN` for upcoming requests.

> The short-lived `accessToken` returned by `/PersonalToken` has a default lifespan of 1 hour, while `refreshToken` is longer-lived (typically 2 days).
>
> In practice:
>
> - Use `accessToken` in `Authorization: Bearer ...` for all API requests.
> - If a request fails with `401 Unauthorized` because the access token expired, call `POST /refresh` with the current `refreshToken`.
> - The `/refresh` response returns a new token pair (`accessToken` + `refreshToken`). Replace both values and continue.
> - If refresh also fails (for example, expired/invalid refresh token, disabled personal token, or user/token state change), call `/PersonalToken` again to start a new session.
>
> Refresh request example:
>
> - Method: `POST`
> - URL: `http://localhost:81/refresh`
> - Header: `Content-Type: application/json`
> - Body:
>
> ```json
> {
>   "refreshToken": "YOUR_REFRESH_TOKEN"
> }
> ```

### Step 2 - Get the Report ID

To generate a report, you need its **Report ID**.

Request:

- Method: `GET`
- URL: `http://localhost:81/api/reportserver/v2/reports`
- Header: `Authorization: Bearer ACCESS_TOKEN`

Response:

- JSON array with report metadata.
- Use the `Id` of the target report.
- `Name` is commonly used to identify the report and then read its `Id`.

### Step 3 - Generate and Download the Report

Once you have the **bearer token** and the **report ID**, use the Reporting REST Service API with five sequential requests.

#### 3.1 - Register a Client

Request:

- Method: `POST`
- URL: `http://localhost:81/api/reports/clients`
- Header: `Authorization: Bearer ACCESS_TOKEN`

Response:

- Read `clientId`.

#### 3.2 - Create a Report Instance

Request:

- Method: `POST`
- URL: `http://localhost:81/api/reports/clients/{clientId}/instances`
- Headers:
  - `Content-Type: application/json`
  - `Authorization: Bearer ACCESS_TOKEN`
- Body:

```json
{
  "report": "ID/{reportId}/",
  "parameterValues": {}
}
```

Response:

- Read `instanceId`.

#### 3.3 - Create a Document

Request:

- Method: `POST`
- URL: `http://localhost:81/api/reports/clients/{clientId}/instances/{instanceId}/documents`
- Headers:
  - `Content-Type: application/json`
  - `Authorization: Bearer ACCESS_TOKEN`
- Body:

```json
{
  "format": "PDF"
}
```

Response:

- Read `documentId`.

#### 3.4 - Poll Document Info Until Ready

Request:

- Method: `GET`
- URL: `http://localhost:81/api/reports/clients/{clientId}/instances/{instanceId}/documents/{documentId}/info`
- Header: `Authorization: Bearer ACCESS_TOKEN`

Response:

- Poll until `documentReady = true`.

#### 3.5 - Download the Generated Document

Request:

- Method: `GET`
- URL: `http://localhost:81/api/reports/clients/{clientId}/instances/{instanceId}/documents/{documentId}?response-content-disposition=attachment`
- Header: `Authorization: Bearer ACCESS_TOKEN`

Response:

- Binary file content in the requested format.

### Full Example (Fetch)

Below is a self-contained example that combines all the steps above. You can paste this directly into the browser developer console (`F12`) while on the Report Server page, or use it in any JavaScript environment:

```js
(async function () {
    // ===== Configuration =====
    const serverHost = "http://localhost:81";
    const reportsApiBase = `${serverHost}/api/reports/reports`;

    // Authentication - choose one of the following:
    const username = "myUsername";
    const password = "myPassword";
    // const personalAccessToken = "your-personal-access-token";

    const reportName = "Dashboard"; // The name of the report to generate
    const format = "PDF";           // The desired export format (PDF, XLSX, CSV, DOCX, etc.)
    const parameterValues = {};     // Report parameter values, e.g., { "Year": 2024 }

    // ===== 1. Authenticate =====
    // Option A: Username/Password
    const loginResponse = await fetch(`${serverHost}/Token`, {
        method: "POST",
        headers: { "Content-Type": "application/x-www-form-urlencoded" },
        body: new URLSearchParams({
            grant_type: "password",
            username: username,
            password: password
        })
    });
    const loginData = await loginResponse.json();
    const token = loginData.accessToken;

    // Option B: Personal Access Token (uncomment to use instead)
    // const patResponse = await fetch(`${serverHost}/PersonalToken`, {
    //     method: "POST",
    //     headers: { "Content-Type": "application/json" },
    //     body: JSON.stringify(personalAccessToken)
    // });
    // const patData = await patResponse.json();
    // const token = patData.accessToken;

    console.log("Authenticated successfully.");

    // ===== 2. Get the Report ID =====
    const reportsResponse = await fetch(`${serverHost}/api/reportserver/v2/reports`, {
        headers: { "Authorization": `Bearer ${token}` }
    });
    const reports = await reportsResponse.json();
    const report = reports.find(r => r.Name === reportName);

    if (!report) {
        throw new Error(`Report "${reportName}" not found.`);
    }

    const reportId = report.Id;
    console.log(`Found report "${reportName}" with ID: ${reportId}`);

    // ===== 3. Register a Client =====
    const clientResponse = await fetch(`${reportsApiBase}/clients`, {
        method: "POST",
        headers: { "Authorization": `Bearer ${token}` }
    });
    const clientData = await clientResponse.json();
    const clientId = clientData.clientId;
    console.log("Client ID:", clientId);

    // ===== 4. Create a Report Instance =====
    const instanceResponse = await fetch(`${reportsApiBase}/clients/${clientId}/instances`, {
        method: "POST",
        headers: {
            "Content-Type": "application/json",
            "Authorization": `Bearer ${token}`
        },
        body: JSON.stringify({
            report: `ID/${reportId}/`,
            parameterValues: parameterValues
        })
    });
    const instanceData = await instanceResponse.json();
    const instanceId = instanceData.instanceId;
    console.log("Instance ID:", instanceId);

    // ===== 5. Create a Document =====
    const docResponse = await fetch(
        `${reportsApiBase}/clients/${clientId}/instances/${instanceId}/documents`,
        {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
                "Authorization": `Bearer ${token}`
            },
            body: JSON.stringify({ format: format })
        }
    );
    const docData = await docResponse.json();
    const documentId = docData.documentId;
    console.log("Document ID:", documentId);

    // ===== 6. Poll Until Document is Ready =====
    let documentReady = false;
    while (!documentReady) {
        const infoResponse = await fetch(
            `${reportsApiBase}/clients/${clientId}/instances/${instanceId}/documents/${documentId}/info`,
            {
                headers: { "Authorization": `Bearer ${token}` }
            }
        );
        const info = await infoResponse.json();
        documentReady = info.documentReady === true;

        if (!documentReady) {
            await new Promise(resolve => setTimeout(resolve, 500));
        }
    }
    console.log("Document is ready for download.");

    // ===== 7. Download the Document =====
    const downloadUrl =
        `${reportsApiBase}/clients/${clientId}/instances/${instanceId}/documents/${documentId}?response-content-disposition=attachment`;

    const downloadResponse = await fetch(downloadUrl, {
        headers: { "Authorization": `Bearer ${token}` }
    });
    const blob = await downloadResponse.blob();
    const url = URL.createObjectURL(blob);
    const a = document.createElement("a");
    a.href = url;
    a.download = `${reportName}.${format.toLowerCase()}`;
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    URL.revokeObjectURL(url);

    console.log(`Downloaded "${reportName}.${format.toLowerCase()}" successfully.`);
})();
```

> The **client ID** becomes invalid after a period of inactivity (the session timeout). Therefore, obtain the client ID, instance ID, and document ID sequentially and use them promptly.

## See Also

- [Using Personal Tokens for Authentication](slug:rs-net-token-authentication)
- [Reporting REST Service API](https://www.telerik.com/products/reporting/documentation/embedding-reports/host-the-report-engine-remotely/rest-api-reference/overview)