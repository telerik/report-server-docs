---
title: Configuring Report Server to be used with external authentication provider
page_title: External authentication provider configuration
description: Configuring Report Server to be used with external authentication provider
slug: login-using-ext-auth-provider
tags: login,authentication,federation
published: True
position: 500
---

# Configuring Report Server to be used with external authentication provider



Along with the local accounts support, Telerik Report Server supports authentication using the Web Services Federation (WS-Federation) [specification](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html). It’s an identity specification that allows to delegate the user authentication to an external provider, forming a trust relationship between a *Relying Party* and an *Identity Provider*. This allows to use a previously configured system of users, roles and trusts (like ActiveDirectory) for authentication against the Report Server user definitions. The WS-Federation standard is acquired by many service providers and it’s relatively easy to setup your own, so its support by Report Server adds to the product versatility and effectiveness.

The authentication process uses *claim-based identification* to gather the required information about the user, requesting the application resources. This simplifies the login process, because the authentication logic is moved to a pre-existing trusted service that guarantees for the requestors’ identity. A claim is a single piece of information about an individual user that the one making the claim asserts to be true for a certain *realm* (the Report Server domain). In our case the claims are issued by the external identity provider and are processed on the server side to decide if the user is authorized to use the Report Server resources. Because the claims can greatly vary by their type and contained information, the account manager processes only three claims, ordered by priority: *NameIdentifier*, *Email* and *Name*.

The WS-Federation service uses an XML document, called *federation metadata*, to describe all the provided claims along with the URIs used from the relying party to authenticate its users. This document must be in a format defined by the WS-Federation standards and is provided to the application from the issuer.

**Configuring Report Server to be used with external authentication providers**

The settings needed to setup the WS-Federation authentication are listed in the section “**External authentication providers settings**” on the **Configuration page** of Telerik Report Server.

-   **Enabled** – if checked, a button “Federation” will appear on the login screen, allowing the users to connect using their WS-Federation accounts. If not checked, the authentication of the users will be done only using the local accounts registered in Telerik Report Server.

-   **Metadata Uri** – this is an Uri that should point to a valid address, used to obtain the *federation metadata* XML document. It must follow the pattern [*http://myFederationServer.com/federationmetadata/2007-06/federationmetadata.xml*](http://myFederationServer.com/federationmetadata/2007-06/federationmetadata.xml)

-   **Relying Party ID** – this URI (not necessarily an URL) that identifies the relying party to the security token service, used from the external identity provider. When you perform the setup for the first time, the field will be automatically populated with the URL of the Telerik Report Server instance you are currently logged into.

-   **Authority –** the URL to the authority that issues the authorization token. It should be noted in the federation metadata document and usually follows the pattern *https://myFederationServer.com/adfs/*.

-   **Client ID** – this is a unique identifier that represents the client application – in this case the Standalone Report Designer – against the authority mentioned above. This ID must be registered into the AD FS. However, in Azure Active Directory it is automatically generated and cannot be changed.
