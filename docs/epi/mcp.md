---
title: sfd
deprecated: false
hidden: false
metadata:
  robots: index
---
> 📘 Note
>
> Some principles outlined here are not yet fully implemented in tooling and supporting processes. Until then, behaviour may vary slightly from what is described.

## Overview

This document defines how EPI APIs evolve over time, balancing the stability of technical integrations with the ability to continuously develop and improve the platform.

Stability is essential in a payment ecosystem. Payments are business-critical services with a low tolerance for failures, and issues in a single integration can affect the wider ecosystem.

At the same time, EPI operates across multiple markets with different regulatory and business requirements. This makes it necessary to evolve the platform quickly and adapt to new needs.

To address this, EPI defines clear principles and procedures for API evolution and integration management.

***

## Introduction

EPI’s API evolution strategy balances two priorities:

- Maintaining **stable integrations across members**.
- Enabling **rapid and flexible product development**.

Each member has its own development processes and release cycles. At the ecosystem level, this requires a consistent approach to managing API changes so that integrations remain reliable while the platform continues to evolve.

***

## Principles

API evolution is guided by the following principles:

- **Backwards compatibility**
  APIs are updated regularly but remain compatible with existing integrations, according to clearly defined rules.

- **Modularity**
  APIs are grouped by functional context, allowing members to focus only on the parts relevant to their integrations.

- **Automation**
  Integrations are tested automatically against API changes to prevent regressions and support scalability.

- **Transparency**
  Changes are clearly documented and communicated so members can assess their impact.

***

## API lifecycle

Each API resource moves through defined lifecycle stages, indicating its maturity and level of support.

### Incubating

APIs in this phase are actively designed and developed.

- Design is iterative and experimental.
- Members are encouraged to provide feedback.
- APIs are typically not available in production.
- Backwards compatibility is not guaranteed.

The primary goal of this phase is to validate and refine API design, including functional adequacy, maintainability, performance, and security.

***

### Available

APIs in this phase are mature and ready for production use.

- Fully versioned and documented.
- Available across all environments.
- Meet functional and non-functional requirements.

EPI ensures that:

- Only non-breaking changes are introduced.
- Existing integrations continue to work without modification.

***

### Deprecated

APIs in this phase are scheduled for eventual removal.

- A deprecation notice is provided in advance.
- APIs are maintained for at least **9 months**.
- Migration guidance is provided.

This phase is only used when APIs are replaced or no longer required.

***

## API compatibility

APIs in the **available** phase may continue to evolve, but all changes must follow strict compatibility rules.

Changes are classified as:

- **Non-breaking changes**
- **Breaking changes**

EPI guarantees that no breaking changes are introduced without coordination. Members must design their integrations to ignore non-breaking changes, as described in [Idempotency](ref:idempotency) and [Error handling](ref:error-handling).&#x20;

This ensures that integrations remain stable without requiring constant updates.

Failure to do so may result in integration instability when APIs evolve.

> 📘 Postel’s Law
>
> Be conservative in what you send, be liberal in what you accept.

***

## Non-breaking changes

Non-breaking changes enable APIs to evolve without impacting existing integrations and may be introduced at any time, including in production.

Integrations must be designed to ignore these changes. Any new functionality they introduce is optional and may be adopted based on member requirements.

### Additive changes

New elements that can be safely ignored:

- Optional request properties
- Response properties
- Optional HTTP headers
- Optional query parameters
- Enum values
- Resources or HTTP methods

***

### Relaxing constraints

Changes that make APIs more flexible:

- A required request property becomes optional.
- An optional response property becomes required.

***

### Safe removals

Changes that do not impact existing integrations:

- Removal of an optional response header.
- Removal of an enum value from responses.

***

### Internal changes

Changes that do not affect how clients interact with the API:

- Changes to the format or length of opaque values.

***

### Example: New property in response

**Original**

```shell
201 Created

{
  "amount": 4900,
  "payerId": "..."
}
```

**With change**

```shell
201 Created

{
  "amount": 4900,
  "payerId": "...",
  "message": ""
}
```

***

> 📘 Note
>
> The following examples illustrate non-breaking changes that existing integrations must ignore.

### Example: Optional header in request

**Original**

```shell
POST /api/payment-requests

{
  "amount": 4900,
  "payerId": "...",
  "message": "Thanks!"
}
```

**With change**

```shell
POST /api/payment-requests

X-Context-ID: 4b5abf4a-...

{
  "amount": 4900,
  "payerId": "...",
  "message": "Thanks!"
}
```

### Example: Optional query parameter

**Original**

```shell
POST /api/payment-requests

{
  "amount": 4900,
  "payerId": "...",
  "message": "Thanks!"
}

```

**With change**

```shell
POST /api/payment-requests?appId=...

{
  "amount": 4900,
  "payerId": "...",
  "message": "Thanks!"
}
```

### Example: Enum value added

**Original**

```shell
{
  "status": "Created"
}
```

**With change**

```shell
{
  "status": "PreIdentified"
}
```

## Breaking changes

Breaking changes must not be introduced for APIs in the **available** phase.

In exceptional cases:

- Changes must be agreed with affected members
- A minimum of **9 months’ notice** is required
- Changes are announced via the changelog and<br />[upcoming breaking changes](ref:upcoming-breaking-changes)

> 🚧 Handling breaking changes
>
> Do not attempt to synchronise deployments with EPI.
>
> It is not possible to switch systems simultaneously without risk.
>
> Instead, integrations should be designed to tolerate change.

***

### Types of breaking changes

| Category           | Description                                                                | Impact on clients                                               |
| :----------------- | :------------------------------------------------------------------------- | :-------------------------------------------------------------- |
| Request structure  | Adding required properties or making optional properties required.         | Clients must update requests to include new or required fields. |
| Response structure | Removing a required property, or making a required property optional.      | Clients must handle missing or optional fields.                 |
| Data type          | Changing the type or constraints of a property.                            | Previously valid values may no longer be accepted.              |
| Behaviour          | Changing endpoint behaviour in a way that affects clients.                 | Client flow and expectations may no longer be valid.            |
| Protocol           | Changing return codes (except generic errors such as `401`, `403`, `5xx`). | Clients must update error handling logic.                       |
| Resource lifecycle | Removing an existing endpoint.                                             | Integrations depending on the endpoint stop working.            |

***

> 📘 Note
>
> All examples below illustrate changes that require updates to existing integrations.

### Example: Required property added to request

**Original**

```shell
POST /api/payment-requests

{
  "amount": 4900,
  "payerId": "...",
  "message": "Thanks!"
}
```

**Breaking change**

```shell
POST /api/payment-requests

{
  "amount": 4900,
  "payerId": "...",
  "message": "Thanks!",
  "icon": ":smile:"
}
```

***

### Example: Required response property removed

**Original**

```shell
201 Created

{
  "id": "abc",
  "status": "failed"
}
```

**Breaking change**

```shell
201 Created

{
  "id": "abc"
}
```

***

### Example: Data type changed

**Original**

```shell
{
  "payerId": "{string}"
}
```

**Breaking change**

```shell
{
  "payerId": "{uuid}"
}
```

***

### Example: Behaviour change (synchronous to asynchronous)

An endpoint that previously guaranteed completion within the response must not be changed to process asynchronously.

Such a change alters when results are available and requires updates to client flow and error handling.

***

### Example: Return code change

If an endpoint changes its expected return codes, clients must update how they interpret and handle responses.

(This does not apply to generic errors such as `401`, `403`, or `5xx`.)

***

### Example: Resource removal

Removing an endpoint invalidates all integrations that depend on it and requires clients to migrate to an alternative.

***

## API categories and versions

EPI provides a wide range of APIs that reflect the full set of products and capabilities offered by the platform. These products evolve over time, with new features introduced iteratively.

At the same time, not all members implement all products, and some may adopt features at different stages. As a result, members typically focus only on the APIs relevant to their specific integrations.

To support this, EPI organises APIs into **feature groups** and **versions**.

### Feature groups

A feature group is a collection of related API resources that enable a specific capability.

Feature groups may represent:

- Product features, such as "P2P Send Money"
- Supporting capabilities, such as authentication or wallet provisioning

Most APIs belong to a single feature group, although some may be shared across multiple groups.

Feature groups evolve over time as the products they represent are extended. Each evolution is captured through a series of feature group releases, representing different generations of functionality.

***

### API versions

Each API resource maintains its own version history, independent of the feature group releases it belongs to.

Versions follow semantic versioning (for example, `1.0.0`), with each component indicating the impact of changes:

- **Major version**<br />Introduces breaking changes and is not backwards compatible with previous major versions

- **Minor version**<br />Introduces non-breaking changes and remains backwards compatible

- **Patch version**<br />Contains bug fixes that do not affect existing integrations

Feature group releases and API resource versions are independent of the underlying platform software. The internal implementation of the platform may evolve without affecting the external API contract.

EPI ensures that changes to internal systems do not impact the stability of the functional and technical contract with members.

***

## API documentation

EPI API documentation reflects the structure and evolution model defined in this document.

Documentation is:

- Organised by feature group
- Versioned by release
- Accompanied by a detailed change history

This allows members to select the specific feature scope and version relevant to their integration.

***

### API structure

The structure of an API includes:

- Resources and endpoints
- Supported HTTP methods
- Payload formats and schemas

This information is provided through:

- Documentation in the developer portal
- OpenAPI specifications

***

### API behaviour

API behaviour describes how the system responds to requests under specific conditions.

This includes:

- Request and response interactions
- Dependencies on system state
- Expected error scenarios

Behaviour is documented using representative examples of request and response pairs for defined system states.

These examples also serve as test cases for functional certification of member implementations.

***

Documentation of API structure, behaviour, and changes between versions is generated automatically from EPI’s internal build and release processes. This ensures that the documentation remains accurate and aligned with the platform implementation.

The documentation is delivered through a web portal that organises all content by feature group and release, and provides a searchable change history.

***

## Testing

> 📘 Note
>
> The concepts and tooling for automated regression testing are currently in development and will be made available in the near future.

Automated testing is fundamental to maintaining stability across the ecosystem.

***

### Validation of API evolution rules

The compatibility rules defined in this document are automatically validated during the build process. This ensures that APIs in the **available** phase comply with the defined evolution principles.

***

### Regression testing

EPI provides tooling for automated regression testing in test environments.

For each API change:

- Predefined test suites are executed against member integrations
- Regressions are identified early
- Compatibility across implementations is maintained

This approach removes the need for manual validation of individual changes and enables EPI’s development processes to scale with the number of integrations.

***

## Deployment process

EPI is introducing deployment strategies to minimise the impact of changes on member integrations.

***

### Canary deployments

Canary deployments allow new software versions to run alongside existing versions within the same environment for a limited period.

Initially, a small percentage of incoming API requests is routed to the new version, while the majority continues to be handled by the existing stable version. Requests are distributed randomly based on defined traffic percentages.

This strategy:

- Limits the impact of potential issues
- Enables early detection of integration problems
- Supports rapid rollback by redirecting traffic to the stable version

If breaking changes accidentally pass internal quality checks, canary deployments provide an additional safeguard and mitigation mechanism.

***

## UNSTABLE APIs (incubation phase)

APIs in the incubation phase may be marked as **UNSTABLE**.

- Subject to frequent change
- Not backwards compatible
- Intended for experimentation and feedback
- Not suitable for production use

Members are encouraged to provide feedback on these APIs, particularly regarding functional adequacy, maintainability, performance, and security, to support validation and refinement of the API design.