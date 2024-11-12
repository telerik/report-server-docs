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

![security-rate-limiter-configuration](../../images/report-server-images/security-rate-limiter-configuration.png)

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

Introduced with 2024 Q4 (10.3.24.112).

With enabled encryption, the Report Server assets are stored in the [Report Server Storage]({%slug storage-settings%}) in encrypted form. The encryption algorithm uses a pair of keys, __Main Key__ and __Backup Key__ created during the initial configuration of the Report Server:

![security-rate-limiter-configuration](../../images/report-server-images/security-configure-encryption.png)

Starting with version 2024 Q4 (10.3.24.112), the encryption is forced upon each new installation of the Report Server.

When upgrading an existing Report Server instance to 2024 Q4 (10.3.24.112) or newer, the administrator user of the Report Server may choose whether to encrypt the Storage (recommended), or keep up with the unencrypted Storage (not recommended). Once encrypted, the Storage cannot be reverted to its unencrypted state.

If the Report Server administrator decides to preserve the Storage unencrypted, when logged in, the Report Server will show the following notification reminding to encrypt the Storage:

![security-rate-limiter-configuration](../../images/report-server-images/security-enable-encryption-message.png)

The operations below allow to generate new pair of encryption keys or uploading a specific pair of encryption keys.

In both cases the security-sensitive assets will be re-encrypted and left in a working state
