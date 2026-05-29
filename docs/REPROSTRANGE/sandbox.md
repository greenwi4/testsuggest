---
title: Sandbox
deprecated: false
hidden: false
metadata:
  robots: index
---
The Entity Verification API (EVA) provides a sandbox environment designed to support safe and effective integration testing across key services: `entitySearch`, `entityData`,  `productRequest` and `managedService`

> ℹ️
>
> The sandbox environment provides a realistic simulation of data retrieval workflows without interacting with external registers or consuming live resources, therefore it won't cause related costs on the client side.

The sandbox replicates the structural and behavioral aspects of the live API while using a predefined set of test data.

## Sandbox catalog

The sandbox operates on a predefined pool of test entities, each configured with supported identifiers and associated documents. Users can search for these entities using the same methods as in production (by name, number, or arbitrary conditions), and retrieve data or initiate document orders accordingly. To select valid test cases, use the dedicated <Anchor target="_blank" href="doc:get-sandboxcatalog">GET system/sandboxCatalog&#x20;</Anchor>. This returns a catalog of available sandbox entity records, including:

- valid entityIds for use with entityData and productRequest
- supported productRequestNames (documents) and optional productOptionIds
- available businessConciergeNames for fallback concierge document ordering
- assigned sources such as register, curated, or both per entity
- whether the entity is processed asynchronously (async)

> ℹ️
>
> The async method is configured per entity, not per jurisdiction. This allows testing both synchronous and asynchronous flows using different entities from the same country.

## Supported sandbox endpoints

### entitySearch in sandbox

The entitySearch endpoint is fully supported in the sandbox environment. It allows testing of all supported search methods:

- name or number with countryCode
- arbitrary with or without countryCode

Results are returned from a fixed pool of test entities and simulate realistic match scoring, result hinting, and metadata structure. Search results reflect the assigned sources for each entity (register, curated, or both). entityData in sandbox

### entityData in sandbox

The entityData endpoint is supported in sandbox and enables testing of entity detail retrieval using valid sandbox entityIds. The sandbox covers core functionality, including:

- requesting entity data by ID
- use of parameters like namedConfiguration and outputStructure
- different status outcomes depending on request processing
- more advanced or non-core features available in production may not be represented.
- asynchronous behavior is simulated for certain entities as specified in the sandboxCatalog.

> ℹ️
>
> If a user submits an entityId that is not part of the sandbox environment, the API returns: “The requested sandbox result is not found or not available yet.”

### productRequest in sandbox

The sandbox supports realistic testing of document ordering through the productRequest endpoint. Each entity may expose:

- one or more productRequestNames (for example, “Register Report” or “Annual Accounts”)
- productOptionIds for multi-version documents (for example, by year)
- concierge documents via businessConciergeNames

Simulated behavior includes:

- status transitions
- document readiness checks using follow-up GET requests
- asynchronous processing where configured per entity

### UBO discovery in sandbox

In the sandbox environment, UBO discovery is only available for a predefined example entity and does not support the full dynamic sandbox entity pool.

### managedService in sandbox

The sandbox supports functional testing of managedService endpoints.

For each sandbox entity, the following use cases are available using the managedServiceRequestType parameter:

- entitySearchSuboptimal
- entitySearchNoMatches
- expandEntityData

> ℹ️
>
> For the entitySearchNoMatches use case, a predefined sandbox entity data set is used.

<br />

<br />
