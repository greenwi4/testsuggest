---
title: sdfvdf
deprecated: false
hidden: false
metadata:
  robots: index
---
# Create a Hosted Checkout session request

<meta name=" description" content="Learn how to create a Hosted Checkout session using the Clover REST API to start a hosted checkout experience for your merchants.">

[block:html]
{
  "html": "<div class=\"container-top\"> \n  <!--North America-US and Canada-->\n  <div class=\"container-reg\">\n    <div class=\"pill-reg\">\n      <div class=\"label-reg\">North America—United States and Canada</div>\n    </div>\n  </div>\n</div>\n<!--syles in global css-->"
}
[/block]

Use the Create checkout endpoint to request a new Hosted Checkout session for a customer transaction. Hosted Checkout sessions are intended to be short-lived and expire 15 minutes after creation.

# Prerequisites

1. [Create a global developer account](https://docs.clover.com/docs/gdp-create-global-developer-account) and select the **Hosted Checkout** checkbox in the [Ecommerce Settings](https://docs.clover.com/dev/docs/clover-development-basics-ecommerce#enable-online-payments-for-ecommerce-card-not-present-transactions).
2. Generate the merchant public token or `apiAccessKey` to make calls to the <<glossary:card tokenization>> server to tokenize a card, as follows:
   * **For a single merchant**—[Generate an Ecommerce API token](https://docs.clover.com/dev/docs/create-ecommerce-api-tokens#step-2-generate-ecommerce-api-tokens-for-integration-types) on the Clover Merchant Dashboard for a Hosted Checkout integration type and note the `merchantId`.
     * **Public key**—Use as the Ecommerce public API key or `apiAccessKey` for tokenization.
     * **Private key**—Set as the Bearer token in the Authorization header to use Ecommerce APIs. When the merchant integrates Clover Hosted Checkout on their website, the token is automatically set up with the required Clover permissions.
   * **For multiple merchant businesses**—First [generate an OAuth `access_token`](https://docs.clover.com/dev/docs/generate-oauth-expiring-access-and-refresh-token) and then use it to [generate an Ecommerce API key (PAKMS key)](https://docs.clover.com/dev/docs/generate-ecommerce-api-key-or-pakms-key) or `apiAccessKey`.

# Create a Hosted Checkout session request

A Hosted Checkout session request must include an empty `customer` object and a `shoppingCart` with one or more items. The `shoppingCart` provides information about the item or items being purchased.

1. Send a `POST` request to the `/invoicingcheckoutservice/v1/checkouts` endpoint.\
   Optionally, include the new configuration parameters for merchants on the Essential SaaS plan and above:
2. If you're creating multiple Hosted Checkout pages, enter the unique page identifier (UUID) of the custom page. The `pageConfigUuid` is automatically generated for each new Hosted Checkout page created in the Merchant Dashboard. Example: `"pageConfigUuid": "7G9V9DP834ZY2"`\
   For more information, see [Take payments with the Clover Hosted Checkout](https://www.clover.com/en-US/help/take-payments-hosted-checkout).\
   **Note:** If you do not enter the pageConfigUuid, the Default Hosted Checkout configuration is used for the merchant.
3. Enter the required parameters in the `shoppingCart` object in the `lineItems` array of objects:

* `note`—Description or note related to the item, for example, additional information if item variants are available for purchase.
* `price`—Unit price of the item.
* `name`—Item name.
* `unitQty`—Item quantity.

4. Enter the required customer parameters as follows:

* If the **customer information feature** is enabled for the merchant (HCO\_CUSTOMER\_INFO\_FEATURE\_ENABLED) then enter:
  * `firstName`—Customer's first name.
  * `lastName`—Customer's last name.
  * `email`—Email address to receive a receipt when the checkout process is finished.
* If the merchant has not enabled the customer information feature, then enter only one of the following: `firstName` `lastName` or `email`.

5. Optional. Set the `tips` parameter to **true**. The tip section is available on the Hosted Checkout page only if the parameter is **true** and the merchant has enabled tipping through the Merchant Dashboard. [See Set tipping preferences](https://www.clover.com/en-US/help/set-tipping-preferences).
6. Optional. Enter the merchant's tax rate in the `taxRates` array. See [Add taxes to transactions](https://docs.clover.com/dev/docs/creating-a-hosted-checkout-session#add-taxes-to-transactions).

* `name`—Tax name.
* `rate`—Tax rate, as an integer where a 10% tax is defined as `1000000`.

7. In the header X-Clover-Merchant-Id, enter the <<glossary:merchantId>>.
8. Set the `authorization: Bearer` as the merchant-specific private key or the OAuth-generated expiring `access_token`.

The  response includes the following elements:

* `href`—URL for the checkout session.
* `checkoutSessionId`—Unique session identifier.
* `createdTime`—Time the session was created (in Unix time).
* `expirationTime`—Time when the checkout session will expire (in Unix time).

# Request and response example—Hosted Checkout session

```curl Request
curl --request POST \
  --url 'https://apisandbox.dev.clover.com/invoicingcheckoutservice/v1/checkouts' \
  --header 'accept: application/json' \
  --header 'content-type: application/json' \
  --header 'X-Clover-Merchant-Id: {merchantId}' \
  --data '{
  "pageConfigUuid": "7G9V9DP834ZY2", //Optional for multiple HCO configurations
  "customer": {
    "email": "customer@example.com",
    "firstName": "Alex",
    "lastName": "Smith",
    "phoneNumber": "5555551010"
  },
  "tips": {
    "enabled": true
  },
  "shoppingCart": {
    "lineItems": [
      {
        "note": "No pulp",
        "name": "Orange juice",
        "price": 600,
        "unitQty": 2
      },
      {
        "note": "Non-dairy",
        "name": "French toast",
        "price": 1200,
        "unitQty": 1
      }
    ]
  }
}'
```
```curl Response
{
    "href": "https://example.com/checkout/59283e4a-cade-4aba-b99d-e4d6c7c4b81a",
    "checkoutSessionId": "59283e4a-cade-4aba-b99d-e4d6c7c4b81a",
    "createdTime": 1603917691672,
    "expirationTime": 1603918591667
}
```

# Add taxes to transactions

Hosted Checkout requests are not linked to the merchant's Clover inventory, so any default tax configuration is not applied to Hosted Checkout payments. There are two requirements for taxes to be applied to a request:

* The merchant must have an existing tax rate.
* The tax is included on any applicable line items in the request. To do so, when you create a checkout session request, add the `taxRates` array and a `rate` for the merchant's tax rates. The `rate` is an integer where a 10% tax is defined as `1000000`. If more than one rate has the same value, the first is used for the checkout process.

```curl
{
  "lineItems": [
    {
      "name": "Mug",
      "price": 1000,
      "unitQty": 1,
      "taxRates": [
        {
          "name": "CO state tax",
          "rate": 1000000
        }
      ]
    }
  ]
}
```

***

# Related topics

* [Clover Hosted Checkout integration](https://docs.clover.com/dev/docs/hosted-checkout-api)
* [Customize Hosted Checkout page](https://docs.clover.com/dev/docs/making-a-checkout-request)
* [Configure Hosted Checkout webhooks](https://docs.clover.com/dev/docs/ecomm-hosted-checkout-webhook)
* [Redirect customers to another URL](https://docs.clover.com/dev/docs/redirecting-customers)