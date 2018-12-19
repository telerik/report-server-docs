---
title: External Authentication Provider
page_title: External Authentication Provider
description: Configuring Report Server to be used with external authentication provider
slug: login-using-ext-auth-provider
tags: login,authentication,federation
published: True
position: 200
---

# External Authentication Provider

Along with the local accounts support, Telerik Report Server supports two types of authentication:

  * Authenticate using the Web Services Federation (WS-Federation) [specification](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html). It’s an identity specification that allows to delegate the user authentication to an external provider, forming a trust relationship between a *Relying Party* and an *Identity Provider*. This allows to use a previously configured system of users, roles and trusts (like ActiveDirectory) for authentication against the Report Server user definitions. The WS-Federation standard is acquired by many service providers and it’s relatively easy to setup your own, so its support by Report Server adds to the product versatility and effectiveness.
  
  * Authenticate using a custom login provider. This provider is also intended to be used in a single sign-on scenarios where the user is already authenticated in the current application context. The Report Server exposes a WebAPI endpoint that accepts signed _nameIdentifier_ claim with a user name as value. After successful validation the endpoint returns an authentication cookie in the response headers. In the most scenarios this cookie will be automatically used by the browser in the subsequent requests, thus seamlessly signing in the current user.

## Federation Provider
The authentication process uses *claim-based identification* to gather the required information about the user, requesting the application resources. This simplifies the login process, because the authentication logic is moved to a pre-existing trusted service that guarantees for the requestors’ identity. A claim is a single piece of information about an individual user that the one making the claim asserts to be true for a certain *realm* (the Report Server domain). In our case the claims are issued by the external identity provider and are processed on the server side to decide if the user is authorized to use the Report Server resources. Because the claims can greatly vary by their type and contained information, the account manager processes only three claims, ordered by priority: *NameIdentifier*, *Email*, and *Name*.

The WS-Federation service uses an XML document, called *federation metadata*, to describe all the provided claims along with the URIs used from the relying party to authenticate its users. This document must be in a format defined by the WS-Federation standards and is provided to the application from the issuer.

### Configuration

The settings needed to setup the WS-Federation authentication are listed in the **Authentication** tab on the **Configuration** page of Telerik Report Server.

-   **Enabled** – if checked, a button “Federation” will appear on the login screen, allowing the users to connect using their WS-Federation accounts. If not checked, the authentication of the users will be done only using the local accounts registered in Telerik Report Server.

-   **Metadata Uri** – this is an Uri that should point to a valid address, used to obtain the *federation metadata* XML document. It must follow the pattern [*http://myFederationServer.com/federationmetadata/2007-06/federationmetadata.xml*](http://myFederationServer.com/federationmetadata/2007-06/federationmetadata.xml).

-   **Relying Party ID** – this URI (not necessarily an URL) that identifies the relying party to the security token service, used from the external identity provider. When you perform the setup for the first time, the field will be automatically populated with the URL of the Telerik Report Server instance you are currently logged into.

-   **Authority –** the URL to the authority that issues the authorization token. It should be noted in the federation metadata document and usually follows the pattern *https://myFederationServer.com/adfs/*.

-   **Client ID** – this is a unique identifier that represents the client application – in this case the Standalone Report Designer – against the authority mentioned above. This ID must be registered into the AD FS. However, in Azure Active Directory it is automatically generated and cannot be changed.

## Custom Login Provider
Similar to the Federation provider, the object that is used for authentication also contains a claim that identifies the user. For security reasons the claim must be signed with a X509 certificate on the client side. This signature will be verified on the server to make sure the user claim is not tampered. In order to perform the verification process, the following properties of the Custom Login Provider must be configured:

-   **Enabled** – if checked, the specific WebAPI endpoint _api/reportserver/customlogin_ will perform verification of the posted data. Otherwise the controller will return **(409) Conflict** as a response.

-   **Hash algorithm** - determines the hash algorithm used to sign the user claims on the client. The supported algorithms are MD5, SHA1, SHA256, SHA384 and SHA512.

-   **X509 Certificate** – a Base64-encoded representation of the certificate used to sign the claims. The verification will be done using the public key, so setting a certificate with only a public key is sufficient. The most convenient way to obtain the Base64 string is to export the certificate from the store using the  _Base-64 encoded X.509 (.CER)_ format. There is no need to have the certificate installed in the certificate store on the machine that hosts the Report Server instance.

When saving the configuration settings, the authentication provider settings will be validated only if the provider is enabled. Since the X509 certificate might not be installed in the certificate store, its validity will not be verified as well. The verification routine will only check if a X509 certificate can be instantiated by the provided Base64-encoded string. In case the authentication provider settings are invalid, a confirmation dialog will ask the user if the saving should continue with the invalid authentication settings.
