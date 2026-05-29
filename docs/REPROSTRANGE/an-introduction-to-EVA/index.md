---
title: Introduction
deprecated: false
hidden: false
metadata:
  robots: index
---
The **Entity Verification API (EVA)** is an API that allows you to access key entity verification data, streamlining access from a single source.

You can access the following using EVA:

- **Live registry data**: Real-time entity data from a network of commercial registers and financial authorities from over 200 countries.
- **Curated entity data**: Data for over 600 million global companies covering information like firmographics, financials, beneficial ownership, corporate hierarchies, and directors.
- **Curated risk data**: A comprehensive risk database of adverse media, sanctions, watchlists, and <Glossary>PEP</Glossary>s.

This data supports and feeds into key business processes, including:

- Customer Onboarding
- Client Lifecycle Management
- Perpetual Know Your Customer (pKYC)
- Third-Party Risk Management (TPRM)
- Investigation/Enhanced Due Diligence (EDD)
- Data Governance
- Fraud Prevention

Integrating EVA allows you to make informed, data-driven business decisions across a wide range of operational workflows.

## EVA features

The following table outlines EVA’s key features:

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Feature
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        `entitySearch`
      </td>

      <td>
        Search for specific entities across official registers and curated datasets by name, identifiers, and other arbitrary attributes.
      </td>
    </tr>

    <tr>
      <td>
        `entityData`
      </td>

      <td>
        Access in-depth information on entities, offering different degrees of detail.
      </td>
    </tr>

    <tr>
      <td>
        `entityValidation`
      </td>

      <td>
        Validate a combination of company name and Tax Identification Number (TIN) with the Internal Revenue Service (IRS).
      </td>
    </tr>

    <tr>
      <td>
        `managedService`
      </td>

      <td>
        Requesting manual assistance when automated entity searches or entity data retrieval do not yield satisfactory results.
      </td>
    </tr>

    <tr>
      <td>
        `entityMonitor`
      </td>

      <td>
        An automated monitor and change-notification service on the structured entity information.

        > This functionality is built on the `entityData` method. Consequently, this feature shares many attributes with `entityData`.
      </td>
    </tr>

    <tr>
      <td>
        `productRequest`
      </td>

      <td>
        Retrieve the official documentation directly from the registers in PDF format and get information from the business assistant service in cases where a jurisdiction or document is not available via direct access through regular API coverage.
      </td>
    </tr>

    <tr>
      <td>
        `system`
      </td>

      <td>
        Search for a complete list of serviceMessages and look for predefined sandbox pool of test entities, each configured with supported identifiers and associated documents and retrieve the coverage details for supported documents, concierge services, and jurisdiction-specific offerings.
      </td>
    </tr>

    <tr>
      <td>
        `subscription`
      </td>

      <td>
        Subscribe to get notifications about specific changes in Entity Verification API services.
      </td>
    </tr>

    <tr>
      <td>
        `notificationHistory`
      </td>

      <td>
        Get notifications about specific changes in EVA services.
      </td>
    </tr>
  </tbody>
</Table>

<br />