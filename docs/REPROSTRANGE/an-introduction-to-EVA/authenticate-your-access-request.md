---
title: Authentication
deprecated: false
hidden: false
metadata:
  robots: index
---
The Entity Verification API (EVA) uses API keys as an authentication method.

An API key is an access token that you provide with your request when calling an API. This API key string is encrypted, for example, `AIzaSyDaGmWKa4JsXZ-HjGw7ISLn\_3namBGewQe`. This ensures safety as each API key is encrypted by the SSL channel.

<Callout icon="⚠️">
  Do not share secret API keys via publicly accessible avenues such as emails and screenshots. API keys carry many privileges and should only be used by authorized users at all times.
</Callout>

## Authenticate your access request

To authenticate your access request, add the API key to each request’s header in the following format: `-H 'x-apikey: {secret}'`.

For example: `GET /method and header 'x-apikey: abcdef12345'`.
