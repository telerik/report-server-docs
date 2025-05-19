---
title: FAQs
page_title: "Frequently Asked Questions about Telerik Report Server Licensing."
slug: license-frequently-asked-questions
tags: license, telerik, report, server, faq, questions
published: True
position: 9
---

# Frequently Asked Questions

This article lists the answers to the most frequently asked questions (FAQs) about working with the Telerik Report Server license key.

## Does the license key expire?

Yes, the license key expires at the end of your support subscription:

* For trial users, this is at the end of your 30-day trial.
* For commercial license holders, this is when your subscription term expires.

You must download a new license each time you start a trial, buy a license, renew a license, upgrade a license.

An expired perpetual license key is valid for all Telerik Report Server versions installed before its expiration date.

## Will the product function with an expired license key?

This depends on the [Telerik Report Server license type (perpetual, subscription, or trial)](https://www.telerik.com/purchase/faq/licensing-purchasing#licensing):

* *Perpetual licenses* function normally with an expired license key, as long as the application is using a Telerik Report Server version that was released before the expiration date of the license.
* *Subscription licenses* function normally in already deployed applications, but you cannot rebuild and republish the app.
* *Trial licenses* function normally only within the 30-day trial period.

If none of the above conditions are met, the following behaviors occur:

* A watermark appears on each report document page.
* A [warning message]({%slug license-errors-and-warnings%}) is logged in the trace log after attaching a Trace Listener to the [Report Server Manager]({%slug search%}) and [Report Server Agent]({%slug service-agent%}).

## I updated the Telerik Report Server and the invalid license errors have appeared. What is the cause of this behavior?

The most likely cause is that the new Telerik Report Server version was released after the expiration date of your current license or license key. To fix this issue:

1. [Download a new license key]({%slug license-key%}#downloading-the-license-key).
1. [Activate the new license key]({%slug license-key%}#activating-telerik-report-server) in your project.

## Do I need an Internet connection to activate the license?

No, the license activation and validation are performed entirely offline.

## What happens if both the environment variable and the license key file are present?

If both the `TELERIK_LICENSE` environment variable and the `telerik-license.txt` file are present, then the environment variable will be used.

To enforce the use of the license key file, unset the environment variable.

## Are earlier versions of Telerik Report Server affected?

No, versions released before January 2025 do not require a license key.

# See Also

* [License Activation Errors and Warnings]({%slug license-errors-and-warnings%})
* [Setting Up Your License Key]({%slug license-key%})
* [License Agreement](https://www.telerik.com/purchase/license-agreement/report-server)
* [Troubleshooting Report Server]({%slug troubleshoot-report-server%})
* [Troubleshooting Report Server for .NET]({%slug troubleshoot-report-server-net%})
