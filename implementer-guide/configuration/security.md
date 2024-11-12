---
title: Security
page_title: Security
description: Security Settings
slug: security
tags: security,settings,report,server
published: True
position: 850
---

# Security

>caption The Security tab of the Report Server Configuration page:

![The Report Server Configuration page.](../../images/report-server-images/security-rate-limiter-configuration.png)

## Rate Limiter

Introduced with [2024 Q3 (10.2.24.806)](https://www.telerik.com/support/whats-new/report-server/release-history/progress-telerik-report-server-2024-q3-10-2-24-806).

Rate limiting is a technique used to control the rate of incoming requests to an API. It sets limits on the number of requests that can be made by an IP address to a specific anonymous endpoint within a defined time period (window). The rate limiter is applied only to non-authenticated users. The Guest special account is not affected by the rate limiter.

When the client has exhausted the number of requests allowed, a 409 "Conflict" response with "The endpoint "{endpointName}" is currently not accessible." message is returned from the server.

### Enable rate limiter

Enables/Disables the rate limiter. By default, the value is set to `enabled`.

### Window

Specifies the time window in milliseconds that takes in the requests. It must be set to a value greater than 0. By default, the value is set to `1000 milliseconds`.

### Permit Limit

The maximum permitted number of requests that can be allowed in a time window. It must be set to a value greater than 0. By default, the value is set to `1`.

## Encryption

Introduced with 2024 Q4 (10.3.24.1112).

With enabled encryption, the Report Server assets are stored in the [Report Server Storage]({%slug storage-settings%}) in encrypted form. The encryption algorithm uses a pair of keys, __Main Key__ and __Backup Key__ created during the initial configuration of the Report Server:

![The Encryption page of the Report Server Configuration with the buttons to download the encryption keys.](../../images/report-server-images/security-configure-encryption.png)

The administrator should type `Confirm` (case insensitive) in the input field just above the __Complete__ button to validate that the keys are safely stored and complete the process.

The encryption keys are stored as environment variables for the user, who is used to run the Report Server and Report Server Service Agent.

The administrator can generate a new pair of encryption keys through the `RESET ENCRYPTION KEYS` or upload a specific pair of encryption keys through the `OVERWRITE ENCRYPTION KEYS` buttons in the __Configuration__ page / __Security__ tab:

![Buttons to reset or upload the encryption keys in the Report Server Configuration page.](../../images/report-server-images/security-reset-upload-encryption-keys.png)

In both cases, the security-sensitive assets will be re-encrypted and left in a working state.

### Install New Report Server Instance

Starting with version 2024 Q4 (10.3.24.1112), encryption is mandatory upon each new installation of the Report Server. __Step 3/3 (Configure Encryption)__ should be completed during the installation process.

### Upgrade an Existing Report Server Instance

When upgrading an existing Report Server instance to 2024 Q4 (10.3.24.1112) or newer, the admin user of the Report Server may choose whether to encrypt the Storage (recommended) or keep up with the unencrypted Storage (not recommended). Once encrypted, the Storage cannot be reverted to its unencrypted state.

If the Report Server administrator decides to preserve the Storage unencrypted, when the admin user is logged in the Report Server will show the following notification reminding to encrypt the Storage at the top of each [Report Server Manager]({%slug search%}) View:

![The message reminding the administrator to enable encryption in the Report Server.](../../images/report-server-images/security-enable-encryption-message.png)

