---
name: Testmcp
---
# API Versioning

Detailed log for the different Airbnb API versions.

_Last modified on Apr 01, 2026_

# Overview

You define the API version through the [header parameter](https://developer.withairbnb.com/homes/docs/authentication-and-encryption), `X-AIRBNB-REQ-API-VERSION`,  in your API requests. Depending on the version you pass, you will get a different response from the API.

To see the documentation of a particular version, use the version dropdown in our docs in the top left corner. Note that the default document version is always the most recent.

We will release a new API version whenever we make any backward-incompatible changes to our APIs in accordance with the [Versioning Schedule](https://developer.airbnb.com/docs/versioning#supported-versions). For simplicity, we name each API version as close as possible to its release date. For example, API version `2023.06.30` was released on June 30, 2023. New versions will apply to each API, meaning that some APIs might have more significant changes for a given new version while others have no changes (aside from the version header). We will regularly deprecate old versions and announce the deprecation date along with the release of the new API version.

***

# Backward-Compatible Changes

We consider the following changes backward-compatible. **We do not release new API versions for backward-compatible changes**—instead, we will add the changes directly to the latest version:

- Adding new APIs
- Adding new optional request parameters to existing APIs
- Adding new properties/parameters to existing API responses
- Changing the order of properties/parameters in an existing API response
- Changing the length or format of opaque strings, such as object IDs, error messages, and other human-readable strings

***

# API Versioning Changelog

The API versioning changelog lists only breaking changes to our APIs. For information regarding feature additions and product updates, see our general [API Changelog](/changelog).

> 📘
>
> Please note that the impact is a **rough estimate of the size** of each change. The level-of-effort required to build such changes will depend on the amount of engineers working on the project and their experience with Airbnb APIs, as well as how your integration was built

| Impact   | Description                                                                                                                                          |
| :------- | :--------------------------------------------------------------------------------------------------------------------------------------------------- |
| Major    | Large size changes with major impact on key APIs, such as pricing, availability or reservations; these changes might affect the reservation flow.    |
| Moderate | Medium size changes that affect how your application interacts with the Airbnb’s APIs, e.g., adding new mandatory functionality and renaming fields. |
| Minor    | Small size changes, e.g., removing already deprecated parameters.                                                                                    |

***

## Version 2025.06.30

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Impact
      </th>

      <th>
        Update
      </th>

      <th>
        Details
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Major
      </td>

      <td>
        Multiple changes to the Messages API
      </td>

      <td>
        Deprecated the ability to send encoded images through the request payload. Instead, use the Media Upload URL to upload an image, then send it via messages

        Removed the `content_type` parameter from the `POST messages` API

        Removed the `attachment_images` parameter from the `GET threads/{thread_id}/messages`, use the `attachment_media` instead
      </td>
    </tr>

    <tr>
      <td>
        Moderate
      </td>

      <td>
        Multiple changes to the Messages API
      </td>

      <td>
        Added better support for threaded replies and translated messages to the message object by adding `parent_message_id` and `translated` parameters

        Added a new required `_inbox_filter` parameter to the `GET threads` API
      </td>
    </tr>

    <tr>
      <td>
        Moderate
      </td>

      <td>
        Reviews API
      </td>

      <td>
        Added a new requirement to the `PUT listing_reviews/{review_id}` API: If the `rating` is negative (\< 5 stars for the respect\_house\_rules category and \< 4 stars for other categories) then a `review_category_tags` must be specified.
      </td>
    </tr>
  </tbody>
</Table>

***

## Version 2024.12.31

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Impact
      </th>

      <th>
        Update
      </th>

      <th>
        Details
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Major
      </td>

      <td>
        Multiple changes to the Reservations API
      </td>

      <td>
        The schema for the Reservations, Reservation Alterations and Price Quote APIs were updated to remove unnecessary extra wording and field complexity. Refer to the [What's new](https://developer.airbnb.com/homes/v2024.12.31/docs/reservations-api#whats-new) section, under the Reservations API guide for more details. This will also affect the payloads on reservation and alteration webhooks.
      </td>
    </tr>

    <tr>
      <td>
        Major
      </td>

      <td>
        Multiple changes to the Messaging API
      </td>

      <td>
        Launched a new `GET v2/threads/{thread_id}/messages endpoint`. Use this endpoint to retrieve paginated messages from a thread.

        Removed the `messages` parameter from the `GET v2/threads` endpoint.

        Removed the `no_messages` query parameter from the `GET v2/threads/{thread_id}` endpoint.
      </td>
    </tr>

    <tr>
      <td>
        Minor
      </td>

      <td>
        Multiple changes to the Rooms API
      </td>

      <td>
        Removed the `room_number` parameter from the `POST v2/listing_rooms` endpoint.

        Removed the `room_type` parameter from the `PUT v2/listing_rooms/{listing_id}/{room_id}` endpoint.

        Renamed `room_amenities` to `accessibility_features`.

        Rooms can only be created with `POST v2/listing_rooms` after Listings API `room_type_category` is set.
      </td>
    </tr>

    <tr>
      <td>
        Minor
      </td>

      <td>
        Multiple changes to the Listings API
      </td>

      <td>
        Removed the `permit_or_tax_id` parameter from the `GET v2/listings/{listing_id}` and `GET v2/listings` endpoints.

        Split regular and accessibility amenities. All accessibility amenities were moved to the new `accessibility_features` parameter. This change affects the PUT and GET Listings endpoints.
      </td>
    </tr>

    <tr>
      <td>
        Minor
      </td>

      <td>
        Deprecate Enhanced Sync Check Response
      </td>

      <td>
        The Enhanced Sync Check Response is now deprecated. Use your preferred PnA endpoint to block the calendar after rejecting a sync availability check.
      </td>
    </tr>

    <tr>
      <td>
        Minor
      </td>

      <td>
        Added validation to Pricing Settings API
      </td>

      <td>
        Added validation to the Pricing Settings API to error requests to set "online" security deposits. Previously, requests succeeded, but the online security deposit was not applied.
      </td>
    </tr>
  </tbody>
</Table>

***

## Version 2024.06.30

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Impact
      </th>

      <th>
        Update
      </th>

      <th>
        Details
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Moderate
      </td>

      <td>
        Deprecating Limited and Undecided Sync Categories
      </td>

      <td>
        The `sync_undecided` and `sync_rates_and_availability` categories are no longer supported.
      </td>
    </tr>

    <tr>
      <td>
        Moderate
      </td>

      <td>
        New Error Details field to Replace Error Reason
      </td>

      <td>
        The `error_reason` field on Validation errors has been replaced with a new `error_details` array.

        The new array will provide a list of objects containing both an `error_message` and an `error_reason` - which will contain multiple errors for supported requests.

        All existing `error_reason` values will still be supported.
      </td>
    </tr>

    <tr>
      <td>
        Minor
      </td>

      <td>
        Async Calendars API require a reason when blocking dates
      </td>

      <td>
        Added three fields to the Async Calendars API related to blocking dates:

        - `busy_subtype` (mandatory): can be `BLOCKED_BY_HOST` or `OUTSIDE_RESERVATION`.

        - `platform` (optional): if `busy_subtype` is `OUTSIDE_RESERVATION`. Can be `VRBO`, `BOOKING_COM` or `OTHER`.

        - `other_platform_name` (optional): if `platform` is `OTHER`. Free text field.
      </td>
    </tr>

    <tr>
      <td>
        Minor
      </td>

      <td>
        Deprecating Approval Status
      </td>

      <td>
        The `listing_approval_status` and `requested_approval_status_category` fields on the Listings API are deprecated. Any errors related to publishing listings will be returned synchronously while listing.
      </td>
    </tr>

    <tr>
      <td>
        Minor
      </td>

      <td>
        Deprecating Online Security Deposits
      </td>

      <td>
        The online Security Deposit feature was removed as part of the 2023 Summer Release. In this version, it will no longer be supported in write or read requests.
      </td>
    </tr>

    <tr>
      <td>
        Minor
      </td>

      <td>
        Change on Listings API for Rate Plan Listings
      </td>

      <td>
        The `rate_plans_enabled` field will be removed for read/write requests. The Pricing and Availability API can be used to enable rate plans.
      </td>
    </tr>

    <tr>
      <td>
        Minor
      </td>

      <td>
        Change on Threads Payload
      </td>

      <td>
        The `roles` field under `thread.attachment` is now deprecated.

        To replace it, a `role` parameter has been added for each user under `thread.users`.
      </td>
    </tr>

    <tr>
      <td>
        Minor
      </td>

      <td>
        Change on Listings API for Amenities
      </td>

      <td>
        In the past, both the `Amenity` and `Sub-Amenity` values in the [table below](/docs/api-versioning#deprecated-sub-amenity-values) have been supported. In this API version, the `Sub-Amenity` values are no longer supported. You can use the `metadata` field to provide more details about an amenity.
      </td>
    </tr>

    <tr>
      <td>
        Minor
      </td>

      <td>
        Change on Listing Rooms API
      </td>

      <td>
        The following room `type` values are no longer supported:

        `COMMON_SPACES  
        COMMON_SPACE  
        CN_ONLY_FLOOR_PLAN  
        FAMILY_ROOM  
        OTHER  
        OUTDOOR_SPACE  
        OUTDOOR_COMMON_AREA  
        ENTRANCE_TO_HOME  
        ENTRY  
        RECREATION_AREA  
        BASEMENT  
        STUDY  
        NEIGHBORHOOD  
        BEACH  
        LOBBY  
        SPA  
        RESTAURANT  
        BAR  
        WRITERS_RETREAT  
        CONSERVATORY`
      </td>
    </tr>

    <tr>
      <td>
        Minor
      </td>

      <td>
        Change on Async Calendar Operations
      </td>

      <td>
        The `_allow_dates_overlap` option is no longer supported.
      </td>
    </tr>

    <tr>
      <td>
        Minor
      </td>

      <td>
        Deprecating Guests with Verified Identity for Instant Book Allowed Category
      </td>

      <td>
        The ‘guests\_with\_verified\_identity’ and ‘well\_reviewed\_guests\_with\_verified\_identity’ values for instant\_booking\_allowed\_category field on the Booking Settings API are deprecated as ID verification is expected for all guests making bookings.
      </td>
    </tr>

    <tr>
      <td>
        Minor
      </td>

      <td>
        Supporting Default Max Nights in LOS Availability Rules API
      </td>

      <td>
        The `default_max_nights` field can be used with the `allow_rtb_above_max_nights` field to allow guests to create a Request to Book for reservations with length of stay above the `default_max_nights`.
      </td>
    </tr>
  </tbody>
</Table>

### Deprecated Sub-Amenity values

| Amenity        | Sub-Amenity                                                              |
| :------------- | :----------------------------------------------------------------------- |
| `TV`           | `CABLE`, `SMART_TV`                                                      |
| `AC`           | `CENTRAL_AIR_CONDITIONING`                                               |
| `BEACH_ACCESS` | `BEACHFRONT`                                                             |
| `COFFEE_MAKER` | `KEURIG_COFFEE_MACHINE`, `NESPRESSO_MACHINE`,  `POUR_OVER_COFFEE`        |
| `GYM`          | `PRIVATE_GYM`, `SHARED_GYM`                                              |
| `POOL`         | `PRIVATE_POOL`, `SHARED_POOL`                                            |
| `JACUZZI`      | `PRIVATE_HOT_TUB`, `SHARED_HOT_TUB`                                      |
| `OVEN`         | `GAS_OVEN`, `STEAM_OVEN`, `DOUBLE_OVEN`, `CONVECTION_OVEN`, `BRICK_OVEN` |
| `KITCHEN`      | `FULL_KITCHEN`                                                           |

***

## Version 2023.06.30

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Impact
      </th>

      <th>
        Update
      </th>

      <th>
        Details
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Major
      </td>

      <td>
        Response Deprecation for all `POST` and `DELETE` APIs
      </td>

      <td>
        Similar to the deprecation of responses to `PUT` APIs, `POST` and `DELETE` APIs will no longer return full responses in 2023.06.30.

        `POST` requests will return an `id` value that can be used along with the appropriate `GET` endpoint to retrieve the full object, if necessary.

        `DELETE` requests will return `200` indicating that the request was successful. If you need the full object value before deletion, you can call the appropriate `GET` endpoint to get the full response.
      </td>
    </tr>

    <tr>
      <td>
        Moderate
      </td>

      <td>
        Changes on Listings API
      </td>

      <td>
        The following fields are now deprecated on the Listings API:<br />bathroom\_shared, `bathroom_shared_with_category`, `common_spaces_shared`, and `common_spaces_shared_with_category`<br />All of these fields have been replaced by existing functionality on the Listing Rooms endpoint.
      </td>
    </tr>

    <tr>
      <td>
        Moderate
      </td>

      <td>
        Changes on Listing Rooms API
      </td>

      <td>
        `room_type` is now required when creating rooms.
      </td>
    </tr>

    <tr>
      <td>
        Moderate
      </td>

      <td>
        Field Deprecations on Reservations API
      </td>

      <td>
        The following fields are now deprecated on the Reservations API, Reservation Alterations API, and Price Quote API, as well as the associated webhooks:<br />listing\_security\_price\_accurate and `listing_cleaning_fee_accurate`.<br />Cleaning fee values will now be shown alongside other `standard_fees_details` as a `pass_through_cleaning_fee`.
      </td>
    </tr>

    <tr>
      <td>
        Moderate
      </td>

      <td>
        Field Deprecations on Pricing Settings API
      </td>

      <td>
        The following fields are now deprecated on the Pricing Settings API:<br />weekly\_price\_factor and `monthly_price_factor`.<br />The `default_pricing_rules` array can be used to set price factors for seven or 28 day durations.
      </td>
    </tr>

    <tr>
      <td>
        Minor
      </td>

      <td>
        Changes on Listing Photos API
      </td>

      <td>
        Removing the last photo from an active listing will no longer result in the listing being deactivated. Instead, a validation error will be returned.

        The caption field will have a maximum length of 250 characters.
      </td>
    </tr>
  </tbody>
</Table>

***

## Version 2022.12.31

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Impact
      </th>

      <th>
        Update
      </th>

      <th>
        Details
      </th>

      <th>
        Resources
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Major
      </td>

      <td>
        Pricing and availability remodeling
      </td>

      <td>
        Pricing and availability APIs are now in three distinct categories, each mapped to a different model, namely `STANDARD`,`LOS_RECORD` and `RATE_PLAN`.
      </td>

      <td>
        [Migration guide](https://developer.withairbnb.com/homes/docs/pricing-availability-models)
      </td>
    </tr>

    <tr>
      <td>
        Major
      </td>

      <td>
        Listing Permits API
      </td>

      <td>
        Deprecated the POST Permits API, and removed the `capability` parameter from the GET Permits API. To use the PUT Permits API in production, you must [certify](https://developer.withairbnb.com/homes/docs/certify-listing-permits) it again.
      </td>

      <td>
        <p><a href="https://developer.airbnb.com/changelog/enhanced-listing-permits-api">Deprecation notice</a></p>
      </td>
    </tr>

    <tr>
      <td>
        Moderate
      </td>

      <td>
        Listings API
      </td>

      <td>
        Passing `deactivation_reason` is now compulsory to unlist listings.
      </td>

      <td>
        <p><a href="changelog:listing-deactivation-reasons">Changelog notice</a></p>
      </td>
    </tr>

    <tr>
      <td>
        Moderate
      </td>

      <td>
        Booking Settings API
      </td>

      <td>
        `instant_booking_allowed_category` parameter now supports the following values:

        - `everyone`
        - `well_reviewed_guests`
        - `guests_with_verified_identity`
        - `well_reviewed_guests_with_verified_identity`
      </td>

      <td>
        [Changelog notice](https://developer.withairbnb.com/homes/changelog/changes-to-instant-book-guest-requirements)
      </td>
    </tr>

    <tr>
      <td>
        Minor
      </td>

      <td>
        Users API
      </td>

      <td>
        `null` values no longer returned in PUT Users API responses.
      </td>

      <td>
        [Deprecation notice](https://developer.withairbnb.com/homes/changelog/deprecating-api-response-for-update-calls)
      </td>
    </tr>

    <tr>
      <td>
        Minor
      </td>

      <td>
        Photos API
      </td>

      <td>
        Removed `large_url` and `extra_large_url` parameters from the GET Photos API.
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        Minor
      </td>

      <td>
        Calendars API
      </td>

      <td>
        Deprecated `host_id` and `listing_currency` parameters from the Calendars API. You can find the `host_id` on the Listings API, and the `listing_currency` on the Pricing Settings API.
      </td>

      <td>

      </td>
    </tr>

    <tr>
      <td>
        Minor
      </td>

      <td>
        Pricing Settings API
      </td>

      <td>
        Deprecated the `eligible_for_pass_through_taxes` parameter. Use the `pass_through_taxes_collection_type` parameter instead.
      </td>

      <td>

      </td>
    </tr>
  </tbody>
</Table>

<br />
