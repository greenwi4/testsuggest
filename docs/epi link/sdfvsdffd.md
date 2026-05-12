---
title: sdfvsdffd
deprecated: false
hidden: false
metadata:
  robots: index
---
| Field      | Format                                    | Example Values                                                                                |
| :--------- | :---------------------------------------- | :-------------------------------------------------------------------------------------------- |
| Identifier | A comma-separated string of email domains | `testbank.com` (single email domain) `testbank.com,testbankmail.com` (multiple email domains) |

### Federation method

Whether members choose OIDC or SAML 2.0, both EPI and the members must provide each other with specific values to configure the federated identity provider. The following tables outline each case.

Note that the following tables show the values required by members for configuring either the Production (Prod), Integration (INT) or User Acceptance Testing (UAT) environments.

Provide the requested information to member support. EPI will respond with a timeline of configuration accordingly.

### OpenID Connect (OIDC)

For OIDC, EPI provides the following values for members to configure OIDC.

|                 | Production (PROD)                                          |
| :-------------- | :--------------------------------------------------------- |
| Field           | Value                                                      |
| Redirect URL    | `https://auth-sso-epicentre.weropay.eu/oauth2/idpresponse` |
| Flow Type       | Authorization Code Flow                                    |
| Application URL | https\://backoffice.weropay.eu/                            |

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

<br />

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

<br />

<br />
