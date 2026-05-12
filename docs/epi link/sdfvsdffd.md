---
title: sdfvsdffd
deprecated: false
hidden: false
metadata:
  robots: index
---
sfvsdvdsf

<br />

|                                                                          |   |   |
| ------------------------------------------------------------------------ | - | - |
| [fsdsdds](https://docs.tstcasce.infinityfree.me/create/docs/epi%20link)  |   |   |
|                                                                          |   |   |

EPI offers its members the ability to use their own single sign-on (SSO) to login to Wero Works by federating access to the members identity provider.

Members who want their users to log into Wero Works with their existing SSO credentials can use the following information to configure a federated identity authorisation protocol that EPI supports.

## Supported federated identity providers

Members can select between or implement both of the following federated identity authorisation protocols that EPI supports:

- SAML 2.0
- OpenID Connect (OIDC)

While members can select either or both identity authorisation protocols, OIDC has the following advantages:

- Simplicity (based on OAuth2.0 and uses JWT token compared to SAML 2.0’s XML)
- Improved usability
- Better compatibility with modern web and mobile applications

## Configuration

### Identifier

To add a member's federated identity provider to Wero Works, EPI requires all the email address domains that users will use to access Wero Works through federation.

The email address domains are required so that EPI can route users to the correct federated identity provider when they sign in. Most use cases involve only one domain name. However,
mapping multiple email address domains to a single federated identity provider is also supported.

| Field      | Format                                    | Example Values                                                                                |
| :--------- | :---------------------------------------- | :-------------------------------------------------------------------------------------------- |
| Identifier | A comma-separated string of email domains | `testbank.com` (single email domain) `testbank.com,testbankmail.com` (multiple email domains) |

### Federation method

Whether members choose OIDC or SAML 2.0, both EPI and the members must provide each other with specific values to configure the federated identity provider. The following tables outline each case.

Note that the following tables show the values required by members for configuring either the Production (Prod), Integration (INT) or User Acceptance Testing (UAT) environments.

Provide the requested information to member support. EPI will respond with a timeline of configuration accordingly.

### OpenID Connect (OIDC)

For OIDC, EPI provides the following values for members to configure OIDC.

|                 | Production (PROD)                                                                                       |
| :-------------- | :------------------------------------------------------------------------------------------------------ |
| Field           | Value                                                                                                   |
| Redirect URL    | `https://auth-sso-epicentre.weropay.eu/oauth2/idpresponse`                                              |
| Flow Type       | Authorization Code Flow                                                                                 |
| Application URL | <Anchor target="_blank" href="https://backoffice.weropay.eu/"><https://backoffice.weropay.eu/></Anchor> |

|                 | Integration (INT)                                                                                                         |
| :-------------- | :------------------------------------------------------------------------------------------------------------------------ |
| Field           | Value                                                                                                                     |
| Redirect URL    | `https://auth-sso-epicentre.int.epi.engineering/oauth2/idpresponse`                                                       |
| Flow Type       | Authorization Code Flow                                                                                                   |
| Application URL | <Anchor target="_blank" href="https://backoffice.int.epi.engineering/"><https://backoffice.int.epi.engineering/></Anchor> |

|                 | User Acceptance Testing (UAT)                                                                                             |
| :-------------- | :------------------------------------------------------------------------------------------------------------------------ |
| Field           | Value                                                                                                                     |
| Redirect URL    | `https://auth-sso-epicentre.werouat.eu/oauth2/idpresponse`                                                                |
| Flow Type       | Authorization Code Flow                                                                                                   |
| Application URL | <Anchor target="_blank" href="https://backoffice.uat.epi.engineering/"><https://backoffice.uat.epi.engineering/></Anchor> |

EPI requires the following fields from members to configure the OIDC federated identity provider:

| Field                     | Description                                                                                                                              |
| :------------------------ | :--------------------------------------------------------------------------------------------------------------------------------------- |
| Client ID                 | Obtained from the OAuth 2.0 application                                                                                                  |
| Client Secret             | Obtained from the OAuth 2.0 application - 128-bit security level (minimum is alphanumeric password 22 chars, special characters allowed) |
| Authorised Scopes         | openId email profile                                                                                                                     |
| Issuer URL                | If members include this value, all fields marked with an asterisk become optional.                                                       |
| Authorization endpoint \* |                                                                                                                                          |
| Token endpoint \*         |                                                                                                                                          |
| Userinfo endpoint \*      |                                                                                                                                          |
| Jwks\_url endpoint \*     |                                                                                                                                          |

| Field   | OAuth Claims                                                |
| :------ | :---------------------------------------------------------- |
| Claim   | Value                                                       |
| `email` | The email address the user logs in with                     |
| `name`  | The full name of the user (i.e. `first_name` + `last_name`) |

### SAML 2.0

For SAML 2.0, EPI provides the following values for a third party to configure their SAML 2.0 application.

|                                | Production (PROD)                                                                                                             |
| :----------------------------- | :---------------------------------------------------------------------------------------------------------------------------- |
| Field                          | Value                                                                                                                         |
| Application URL                | [https://backoffice.weropay.eu/](https://backoffice.weropay.eu/)                                                              |
| Entity ID or Audience URL      | [https://auth-sso-epicentre.weropay.eu/eu-central-1\_DW1KxuaOV](https://auth-sso-epicentre.weropay.eu/eu-central-1_DW1KxuaOV) |
| Assertion Consumer Service URL | `https://auth-sso-epicentre.weropay.eu/eu-central-1_DW1KxuaOV/saml2/idpresponse`                                              |

|                                | Integration (INT)                                                                                                         |
| :----------------------------- | :------------------------------------------------------------------------------------------------------------------------ |
| Application URL                | <Anchor target="_blank" href="https://backoffice.int.epi.engineering/"><https://backoffice.int.epi.engineering/></Anchor> |
| Entity ID or Audience URL      | `https://auth-sso-epicentre.int.epi.engineering/eu-central-1_fVXxjM2vB`                                                   |
| Assertion Consumer Service URL | `https://auth-sso-epicentre.int.epi.engineering/eu-central-1_fVXxjM2vB/saml2/idpresponse`                                 |

|                                | User Acceptance Testing (UAT)                                                                           |
| :----------------------------- | :------------------------------------------------------------------------------------------------------ |
| Application URL                | <Anchor target="_blank" href="https://backoffice.werouat.eu/"><https://backoffice.werouat.eu/></Anchor> |
| Entity ID or Audience URL      | `https://auth-sso-epicentre.werouat.eu/eu-central-1_27x4hl1gR`                                          |
| Assertion Consumer Service URL | `https://auth-sso-epicentre.werouat.eu/eu-central-1_27x4hl1gR/saml2/idpresponse`                        |

EPI requires the following fields from members to configure the SAML federated identity provider:

| Field                             | Description             |
| :-------------------------------- | :---------------------- |
| Metadata URL or Metadata xml file | Preferably Metadata URL |

|           | Attribute mapping                                           |
| :-------- | :---------------------------------------------------------- |
| Attribute | Value                                                       |
| `email`   | The email address the user logs in with                     |
| `name`    | The full name of the user (i.e. `first_name` + `last_name`) |

### SAML Certificates

When EPI receives either the metadata URL or metadata xml file, EPI can then supply the following certificates if the provider is configured to sign SAML 2.0 requests or encrypt SAML 2.0 assertions, or both:

- SAML 2.0 Request signing certificate (CRT file)
- SAML 2.0 Encrypted assertions certificate (CRT file)

## Submitting a request

Once your organization is ready to configure a federated identity provider, please submit a request through the <Anchor target="_blank" href="https://epicompany.atlassian.net/servicedesk/customer/portal/2/group/222">EPI Member Run Portal</Anchor>.

### Important:

Before EPI can enable Production (PROD) configuration, members must first request Integration (INT) or User Acceptance Testing (UAT) _(ideally both, but not mandatory)_ and complete testing with EPI to confirm successful setup.<br />The PROD configuration must use different credentials than those used in INT or UAT environments.

EPI will review your request and provide a timeline for configuration.
