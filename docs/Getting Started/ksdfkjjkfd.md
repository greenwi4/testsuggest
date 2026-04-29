---
title: ksdfkjjkfd
deprecated: false
hidden: false
metadata:
  robots: index
---
# Promos API Integration Overview

Use the Affirm Promos API to add dynamic pricing and educational modals to your site. Customize promotional messaging, integrate prequalification, and enhance customer engagement with flexible financing options. Includes setup, API requests, and implementation details.

<HTMLBlock>{`
<style>
  .country-dropdown-menu {
    font-family: Arial, sans-serif;
    max-width: 250px;
    margin-left: auto;
    margin-right: 0;
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 10px;
    background: #4A4AF4;
    overflow: hidden;
  }

  .country-dropdown-content {
    display: none;
    margin-top: 5px;
    padding: 10px;
    background: #fff;
    border: 1px solid #ddd;
    border-radius: 4px;
  }

  .country-dropdown-item.open .country-dropdown-content {
    display: block;
  }

  .country-dropdown-toggle {
    display: block;
    width: 100%;
    text-align: left;
    padding: 10px;
    background: #fff;
    border: 1px solid #ddd;
    border-radius: 4px;
    cursor: pointer;
  }

  .country-flag-icon {
    width: 20px;
    height: 20px;
    margin-right: 10px;
    vertical-align: middle;
  }

  .country-title {
    font-size: 20px;
    text-align: center;
    font-weight: bold;
    color: #fff;
  }
</style>

<div class="country-dropdown-menu">
  <p class="country-title">Country Availability</p>

  <div class="country-dropdown-item">
    <button class="country-dropdown-toggle" type="button" aria-expanded="false">
      <b>Country List</b> ↓
    </button>

    <div class="country-dropdown-content">
      <div>
        <img src="https://files.readme.io/a4c8b3d6596d943e2b93c82cb1d432a2edaf6998667835c2e97ef4a31d460c7e-us-circle-01.png" alt="USA" class="country-flag-icon">
        USA
      </div>
      <div>
        <img src="https://files.readme.io/3ca294a1b4b8b8506c3ff32876abc6e3e33d0e65a509dab81398915094bdbc5c-61TcZ33ZrJL._AC_UY1000_.jpg" alt="Canada" class="country-flag-icon">
        Canada
      </div>
      <div>
        <img src="https://files.readme.io/db98461fef617df7c9970e98f01150f067fcee1fc823a450f09056138b9f70be-united-kingdom-flag-rounded-icon-uk-flag-union-jack-vector.jpg" alt="UK" class="country-flag-icon">
        UK
      </div>
    </div>
  </div>
</div>

<script>
  document.querySelectorAll('.country-dropdown-toggle').forEach(function (button) {
    button.addEventListener('click', function () {
      var item = button.closest('.country-dropdown-item');
      var isOpen = item.classList.toggle('open');
      button.setAttribute('aria-expanded', String(isOpen));
    });
  });
</script>
`}</HTMLBlock>


## Overview

You can use the promos server-side API endpoint to render dynamic prices (or other promotional text) and to present Affirm-hosted educational modals on your website. We've designed our promos service to be lightweight and usable for both merchants and Affirm developers, making it easy to implement in different environments.  Below you’ll find information about our newest Promos API along with integration instructions.

## How It Works

The promos endpoint interfaces with our promos service. Based on query parameters sent by the client, our service returns the correct response containing the financing terms and styles for the Affirm modal and ALA (“As Low As”) messaging.

## Inputs

**Base Path:** `https://www.affirm.com/api/promos/v2/{YOUR_PUBLIC_KEY}` where YOUR\_PUBLIC\_KEY is your public api key.

> 📘 Public API Key
>
> Every Affirm merchant has a unique public API Key, so you should work with an Affirm CSM to onboard a new merchant you want to use this API endpoint.

## Attributes

<table>
  <tr>
    <td><strong>Query Param Name</strong></td>
    <td><strong>Data type</strong></td>
    <td><strong>Description</strong></td>
    <td><strong>Supported Values</strong></td>
    <td><strong>Default</strong></td>
  </tr>

  <tr>
    <td>
      amount
      <p>required</p>
    </td>

    <td><em>int32</em></td>
    <td>The total amount of the checkout in USD or CAD cents (e.g., 10000 cents to charge $100.00).</td>

    <td />

    <td>Current currency default locale</td>
  </tr>

  <tr>
    <td>page\_type</td>
    <td><em>string</em></td>

    <td>
      Identifies your promotional messaging so Affirm can apply the necessary customizations based on which page they are displayed.<strong> </strong>

      <ul>
        <li><em>homepage</em>: Your site's homepage</li>
        <li><em>landing</em>: A landing page that describes Affirm</li>
        <li><em>search</em>: Your site's search results page</li>
        <li><em>category</em>: Your site's category page</li>
        <li><em>product</em>: A product description page</li>
        <li><em>cart</em>: Your site's cart page</li>
        <li><em>payment</em>: The payment selection page</li>
        <li><em>banner</em>: A banner image (use for any promotional messaging triggered by your banner or image regardless of page location)</li>
        <li><em>marketplace</em>: The marketplace landing page</li>
      </ul>
    </td>

    <td>
      homepage \
      landing \
      search \
      category \
      product
      <p>cart</p>
      <p>payment</p>
      <p>banner \
      marketplace</p>
    </td>

    <td>product</td>
  </tr>

  <tr>
    <td>
      template\_field
      <p><em>optional</em></p>
    </td>

    <td />

    <td>
      Determine what types of promos to render:

      <p />

      <ul>
        <li><em>en\_US</em>: English-speaking United States</li>
        <li><em>en\_CA</em>: English-speaking Canada</li>
        <li><em>fr\_CA</em>: French-speaking Canada</li>
        <li><em>en\_GB</em>: English-speaking United Kingdom</li>
      </ul>
    </td>

    <td>en\_US \ en\_CA \ fr\_CA \ en\_GB</td>
    <td>Current country’s default locale</td>
  </tr>
</table>

## Response Fields

The following demonstrates the data returned from our promo API that can then be used to customize the text. Please work with your Affirm partner to ensure you are compliant.

To customize text returned from promos api, please work with your Affirm partner.

### ALA

```json JSON
{
    "promo": {
        "html_ala": HTML formatted as low as messaging,
        "config": [Internal Use Only],
        "ala": As low as messaging
    }
}
```

### Modal

Note: Many of these fields are used for Affirm modal formatting.

```json
{
    "promo": {
        "headline": Headline for educational modal,
        "tagline": One-line sample of the best term for the specified data amount and merchant,
        "button": Call to action text for user,
        "html_footer": HTML formatted legal disclosures,
        "description": One-line message about what Affirm is,
        "config": {
             "promo_prequal_enabled": Indicator of if prequalification
                                      is enabled for this merchant and
                                      this promotional message (true or
                                      false),
             "images": {
                "hero2x": High quality merchant promotional image url 
                          (default null),
                "logo": Merchant logo url (default null),
                "hero": Merchant promotional image url (default null),
                "logo2x": High quality merchant logo url (default null),
              },
             "merchant_name": Merchant's name,
             "merchant_ari": Merchant's unique identifier,
             "enabled_integrations": What integrations are enabled for this merchant,
             "user_ari": User's unique identifier,
             "toast_enabled": Whether or not toast messaging is enabled for the merchant,
          }
    },
    "offer": {
        "terms": List of sample loan terms for the given cart amount.
                 Each term will have the following format:
                 {
                    "amount": Total amount due when loan is completed,
                    "loan_type": Loan type available for this merchant 
                                 (classic, affirm_go_v3, affirm_go),
                    "interest_amount": Amount of interest for this
                                       loan term,
                    "billing_frequency": Frequency at which the user will
                                         need to pay back the loan,
                    "apr": APR for this loan term,
                    "installment_amount": Amount due at each payment,
                    "minimum_loan_amount": Minimum loan amount available
                                           to the user,
                    "installment_count": Total number of installments,
                    "downpayment_amount": The amount required for a downpayment, if any,
                 },
        "expiry_date": [Internal Use Only],
        "minimum_loan_amount": Minimum loan amount available to the user,
        "maximum_loan_amount": Maximum loan amount available to the user
    }
}
```

### All

```json
{
    "promo": {
        "ala": As low as messaging
        "html_ala": HTML formatted as low as messaging,
        "headline": Headline for educational modal,
        "tagline": One-line sample of the best term for the specified data amount and merchant,
        "button": Call to action text for user,
        "html_footer": HTML formatted legal disclosures,
        "description": One-line message about what Affirm is,
        "config": {
             "promo_prequal_enabled": Indicator of if prequalification
                                      is enabled for this merchant and
                                      this promotional message (true or
                                      false),
             "images": {
                "hero2x": High quality merchant promotional image url 
                          (default null),
                "logo": Merchant logo url (default null),
                "hero": Merchant promotional image url (default null),
                "logo2x": High quality merchant logo url (default null),
              },
             "merchant_name": Merchant's name,
             "merchant_ari": Merchant's unique identifier,
             "enabled_integrations": What integrations are enabled for this merchant,
             "user_ari": User's unique identifier,
             "toast_enabled": Whether or not toast messaging is enabled for the merchant,
          }
    },
    "offer": {
        "terms": List of sample loan terms for the given cart amount.
                 Each term will have the following format:
                 {
                    "amount": Total amount due when loan is completed,
                    "loan_type": Loan type available for this merchant 
                                 (classic, affirm_go_v3, affirm_go),
                    "interest_amount": Amount of interest for this
                                       loan term,
                    "billing_frequency": Frequency at which the user will
                                         need to pay back the loan,
                    "apr": APR for this loan term,
                    "installment_amount": Amount due at each payment,
                    "minimum_loan_amount": Minimum loan amount available
                                           to the user,
                    "installment_count": Total number of installments,
                    "downpayment_amount": The amount required for a downpayment, if any,
                 },
        "expiry_date": [Internal Use Only],
        "minimum_loan_amount": Minimum loan amount available to the user,
        "maximum_loan_amount": Maximum loan amount available to the user
    }
}
```

***

## Requests

### As Low As Messaging

#### Basic Request Using Defaults

```curl
https://affirm.com/api/promos/v2/{YOUR_PUBLIC_KEY}?amount={AMOUNT_IN_CENTS}&field=ala&use_best_terms=true&show_cta=true
```

##### Sample Request

```curl
https://affirm.com/api/promos/v2/L6MZWHPL1AHQOYOJ?amount=18500&field=ala&use_best_terms=true&show_cta=true
```

##### Sample Response

```json
{
    "promo":
    {
        "ala": "Starting at $17/mo with Affirm. See if you qualify" 
        "html_ala": "Starting at <span class='affirm-ala-price'>$17</span>/mo with <span class='__affirm-logo __affirm-logo-blue'>Affirm</span>. <a class='affirm-modal-trigger'>See if you qualify</a>",
        "config":
          {
            "promo_prequal_enabled": true,
            "merchant_ari": "ABCDEXZ",
              "enabled_integrations": [],
               "user_ari": "",
               "toast_enabled": false
          },
    }
}
```

#### Basic Request with Custom Items

```curl
https://www.affirm.com/api/promos/v2/{YOUR_PUBLIC_KEY}?amount={AMOUNT_IN_CENTS}&field=ala&items=%5B%7B%22sku%22%3A%22{ITEM_SKU}%22%2C%22display_name%22%3A{ITEM_NAME}%2C%22qty%22%3A{QUANTITY}%2C%22unit_price%22%3A{UNIT_PRICE}%7D%5D&page_type=product
```

##### Sample Request

```curl
https://www.affirm.com/api/promos/v2/L6MZWHPL1AHQOYOJ?amount=10000&field=ala&items=%5B%7B%22sku%22%3A%22ABC123%22%2C%22display_name%22%3A%22Glasses%22%2C%22qty%22%3A2%2C%22unit_price%22%3A5000%7D%5D&page_type=product
```

##### Sample Response

```json
{
    "promo":
    {
        "ala": "Starting at $10/mo with Affirm. See if you qualify"
        "html_ala": "Starting at <span class='affirm-ala-price'>$10</span>/mo with <span class='__affirm-logo __affirm-logo-blue'>Affirm</span>. <a class='affirm-modal-trigger'>See if you qualify</a>",
        "config":
          {
            "promo_prequal_enabled": true,
            "merchant_ari": "ABCDEXZ",
              "enabled_integrations": [],
               "user_ari": "",
               "toast_enabled": false
          },
    }
}
```

### Modal Rendering

#### Basic Request Using Defaults

```curl
https://affirm.com/api/promos/v2/{YOUR_PUBLIC_KEY}?amount={AMOUNT_IN_CENTS}&field=modal&use_best_terms=true
```

##### Sample Request

```curl
https://affirm.com/api/promos/v2/L6MZWHPL1AHQOYOJ?amount=10000&field=modal&use_best_terms=true
```

##### Sample Response

```json
{
    "promo":
    {
        "description": "Get a real-time decision with just 5 pieces of info.",
        "headline": "Make easy monthly payments over 3, 6, or 12 months",
        "tagline": "$9.04/mo. based on a purchase price of $100.00 at 15% APR for 12 months. Rates from 10–30% APR.",
        "button": "See if you qualify",
        "html_footer": "Rates are between 10–30% APR. A down payment may be required. Subject to eligibility check and approval. Payment options depend on your purchase amount. Estimated payment amount excludes taxes and shipping fees. Actual terms may vary. Payment options through Affirm are provided by these lending partners: [affirm.com/lenders](https://www.affirm.com/lenders). Visit [affirm.com/help](https://affirm.com/help) for more info.",
        "config":
        {
           "promo_prequal_enabled": true,
           "images":
            {
                "hero2x": null,
                "logo": null,
                "hero": null,
                "logo2x": null
            },
            "merchant_name": "[TEST] Sandbox Merchant"
            "merchant_ari": "ABCXYZ",
            "enabled_integrations": [],
            "user_ari": "",
            "toast_enabled": false,
        }
    },
    "offer":
    {
        "terms":
        [
            {
                "downpayment_amount": null,
                "loan_type": "classic",
                "interest_amount": 256,
                "billing_frequency": "monthly",
                "apr": 15.29,
                "installment_amount": 3418,
                "minimum_loan_amount": 50,
                "amount": 10256,
                "installment_count": 3
            },
            {
                "downpayment_amount": null,
                "loan_type": "classic",
                "interest_amount": 449,
                "billing_frequency": "monthly",
                "apr": 15.24,
                "installment_amount": 1742,
                "minimum_loan_amount": 50,
                "amount": 10449,
                "installment_count": 6
            },
            {
                "downpayment_amount": null,
                "loan_type": "classic",
                "interest_amount": 843,
                "billing_frequency": "monthly",
                "apr": 15.22,
                "installment_amount": 904,
                "minimum_loan_amount": 100,
                "amount": 10843,
                "installment_count": 12
            }
        ],
        "expiry_date": null,
        "minimum_loan_amount": 50
        "minimum_loan_amount": 2000
    }
}
```

#### Basic Request with Custom Items

```curl
https://www.affirm.com/api/promos/v2/{YOUR_PUBLIC_KEY}?amount={AMOUNT_IN_CENTS}&field=modal&items=%5B%7B%22sku%22%3A%22{ITEM_SKU}%22%2C%22display_name%22%3A{ITEM_NAME}%2C%22qty%22%3A{QUANTITY}%2C%22unit_price%22%3A{UNIT_PRICE}%7D%5D&page_type=product
```

##### Sample Request

```curl
https://www.affirm.com/api/promos/v2/L6MZWHPL1AHQOYOJ?amount=10000&field=modal&items=%5B%7B%22sku%22%3A%22ABC123%22%2C%22display_name%22%3A%22Glasses%22%2C%22qty%22%3A2%2C%22unit_price%22%3A5000%7D%5D&page_type=product
```

##### Sample Response

```json
{
    "promo":
    {
        "description": "",
        "headline": "Make easy monthly payments over 3, 6, or 12 months",
        "tagline": "$9.04/mo. based on a purchase price of $100.00 at 15% APR for 12 months. Rates from 10–30% APR.",
        "button": "See if you qualify",
        "html_footer": "A down payment may be required. Subject to eligibility check and approval. Payment options depend on your purchase amount. Estimated payment amount excludes taxes and shipping fees. Actual terms may vary. Payment options through Affirm are provided by these lending partners: [affirm.com/lenders](https://www.affirm.com/lenders). Visit [affirm.com/help](https://affirm.com/help) for more info.",
        "config":
        {
            "promo_prequal_enabled": true,
            "images":
            {
                "hero2x": null,
                "logo": null,
                "hero": null,
                "logo2x": null
            },
            "merchant_name": "[TEST] Sandbox Merchant"
            "merchant_ari": "ABCXYZ",
            "enabled_integrations": [],
            "user_ari": "",
            "toast_enabled": false,
        }
    },
    "offer":
    {
        "terms":
        [
            {
                "downpayment_amount": null,
                "loan_type": "classic",
                "interest_amount": 256,
                "billing_frequency": "monthly",
                "apr": 15.29,
                "installment_amount": 3418,
                "minimum_loan_amount": 50,
                "amount": 10256,
                "installment_count": 3
            },
            {
                "downpayment_amount": null,
                "loan_type": "classic",
                "interest_amount": 449,
                "billing_frequency": "monthly",
                "apr": 15.24,
                "installment_amount": 1742,
                "minimum_loan_amount": 50,
                "amount": 10449,
                "installment_count": 6
            },
            {
                "downpayment_amount": null,
                "loan_type": "classic",
                "interest_amount": 843,
                "billing_frequency": "monthly",
                "apr": 15.22,
                "installment_amount": 904,
                "minimum_loan_amount": 100,
                "amount": 10843,
                "installment_count": 12
            }
        ],
        "expiry_date": null,
        "minimum_loan_amount": 50
        "minimum_loan_amount": 2000
    }
}
```

## Implementation

1. Create an API GET request with the required parameters to fetch the ALA messaging from the endpoint below.

   `https://www.affirm.com/api/promos/v2/{YOUR_PUBLIC_KEY}`

2. Use the ala field value in the response to get the ALA promotional messaging (e.g. Starting at $185/mo with Affirm. Prequalify now).

3. Set up an HTML hyperlink on your website for the prequalification CTA (call to action) with a parallel URL following this format:

```html Parallel URL
https://www.affirm.com/apps/prequal/?public_api_key=YOUR_PUBLIC_KEY&unit_price=PRODUCT_PRICE&page_type=PAGE_TYPE&use_promo=true&referring_url=https://www.YourReturningURL.com
```

For instance, if you want to implement prequalification with the ALA “*Starting at $185/mo with Affirm*. Prequalify now” on your product page, you would use the following HTML snippet:

```html
<p>Starting at $185/mo with Affirm. <a href="https://www.affirm.com/apps/prequal/?public_api_key=L6MZWHPL1AHQOYOJ&unit_price=222000&PRODUCT_PRICE&page_type=product&use_promo=true&referring_url=https%253A%252F%252Fwww.affirm.com%252F&" target="_blank">Prequalify now</a></p>
```

#### Parallel URL

The parallel URL is the url that must be visibly linked to the CTA that directs to an informational page due to regulatory requirements. Please see the following example:

parallel URL

`https://www.affirm.com/apps/prequal/?public_api_key=YOUR_PUBLIC_KEY&unit_price=25000&page_type=product&referring_url=https://www.YourReturningURL.com`

### **Note:**

* The key of amount changes to unit\_price for the informational URL.
* The `referring_url` is only applicable if prequalification feature is active.
* If you support sku based financing, you can also pass stringified items.

If prequalification is enabled, this URL will be used to redirect the user back to the website once they complete prequalification.

4. Validate the functionality with a [jsfiddle](https://jsfiddle.net/Kelvinaffirm/9y2uv5x7/) sample and ensure the prequalification functionality works

### Questions?

If you have any questions, reach out to your technical contact at Affirm.

## Example Implementation on a Product Page

Any time you would like to add Affirm *As Low As* messaging (e.g. “Starting at $185/mo with Affirm. Prequalify now”), you must include the following two parts:

* The ALA messaging itself: Starting at $185/mo with Affirm
* The CTA which includes a link to a modal with disclosures, etc: Prequalify now

The CTA, a link to an Affirm page with details matching and explaining the *As Low As* messaging, is required to satisfy lending regulations. That is, for any given promo request that is built, a parallel URL for an informational page must be built and visibly linked on the CTA of the ALA message that is returned by the ALA endpoint.

For example, on a product detail page listing, you'll use the following request to retrieve the ALA for a $250.00 product:

### Request

```curl
curl --request GET \
  --url https://www.affirm.com/api/promos/v2/YOUR_PUBLIC_KEY?amount=25000&use_best_terms=true&page_type=product
```

### Response

The response returned by this request would look like the following:

JSON

```json
{
   "promo": {
       "description": "Get a real-time decision with just 5 pieces of info.",
       "headline": "Make easy monthly payments over 3, 6, or 12 months",
       "tagline": "$22.60/mo. based on a purchase price of $250.00 at 15% APR for 12 months. Rates from 0\u201330% APR.",
       "html_ala": "Starting at <span class='affirm-ala-price'>$23</span>/mo with <span class='__affirm-logo __affirm-logo-blue'>Affirm</span>. <a class='affirm-modal-trigger'>Prequalify now</a>",
       "ala": "Starting at $23/mo with Affirm. Prequalify now",
       "html_footer": "Rates are between 0\u201330% APR. A down payment may be required. Subject to eligibility check and approval. Payment options depend on your purchase amount. Estimated payment amount excludes taxes and shipping fees. Actual terms may vary. Payment options through Affirm are provided by these lending partners: <a class='affirm-loan-originator' href='https://www.affirm.com/lenders'>affirm.com/lenders</a>. Visit affirm.com/help for more info.",
       "button": "See if you qualify"
       "config": {
           "promo_prequal_enabled": true,
            "images":
            {
                "hero2x": null,
                "logo": null,
                "hero": null,
                "logo2x": null
            },
            "merchant_name": "[TEST] Sandbox Merchant"
            "merchant_ari": "ABCXYZ",
            "enabled_integrations": [],
            "user_ari": "",
            "toast_enabled": false,

       },
   },
   "offer": {
       "terms": [
           {
               "loan_type": "classic",
               "interest_amount": 0,
               "billing_frequency": "monthly",
               "apr": 0.00,
               "installment_amount": 8333,
               "minimum_loan_amount": 50,
               "amount": 25000,
               "installment_count": 3,
               "downpayment_amount": null,
           },
           {
               "loan_type": "classic",
               "interest_amount": 1128,
               "billing_frequency": "monthly",
               "apr": 15.31,
               "installment_amount": 4355,
               "minimum_loan_amount": 50,
               "amount": 26128,
               "installment_count": 6,
               "downpayment_amount": null,
           },
           {
               "loan_type": "classic",
               "interest_amount": 2115,
               "billing_frequency": "monthly",
               "apr": 15.27,
               "installment_amount": 2260,
               "minimum_loan_amount": 100,
               "amount": 27115,
               "installment_count": 12,
               "downpayment_amount": null,
           }
       ],
        "expiry_date": null,
        "minimum_loan_amount": 50
        "minimum_loan_amount": 2000
   }
}
```

From these two responses, we would then build the HTML to insert on your page:

1. Pull the html\_ala from the promo response:

```html
"html_ala": "Starting at \<span class='affirm-ala-price'>$23\</span>/mo with \<span class='**affirm-logo **affirm-logo-blue'>Affirm\</span>. \<a class='affirm-modal-trigger'>Prequalify now\</a>"
```

2. Identify the CTA. In this example, the CTA is “Prequalify now” and it is wrapped in an `<a>` tag with `class=affirm-modal-trigger`.

Insert your href attribute and link to the parallel URL:

href=`https://www.affirm.com/apps/prequal/?public_api_key=YOUR_PUBLIC_KEY&unit_price=25000&page_type=product&referring_url=https://www.YourReturningURL.com`

The end HTML would look like this:

HTML

```html
Starting at <span class='affirm-ala-price'>$23</span>/mo with <span class='__affirm-logo __affirm-logo-blue'>Affirm</span>. <a class='affirm-modal-trigger' href='https://www.affirm.com/apps/prequal/?public_api_key=YOUR_PUBLIC_KEY&unit_price=25000&page_type=product&referring_url=https://www.YourReturningURL.com'>Prequalify now</a>
```

### Out of Cart Range

By default, Affirm uses the following ALA messaging for out of cart range amounts. For example:

* **Buy with Affirm on orders over $50**

In this example, the ‘$50’ shows the minimum cart amount. This value is customized according to the amount set for your business.

> 📘 Note
>
> The referring\_url is only applicable if the prequalification feature is active.