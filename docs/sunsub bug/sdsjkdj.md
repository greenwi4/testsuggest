---
title: sdsjkdj
deprecated: false
hidden: false
metadata:
  robots: index
---
This section lists a collection of webhooks that you may receive during [transaction monitoring](doc:transaction-monitoring).

| Webhook                                                                                    | Description                                                                                                                                                                                                                           |
| :----------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [applicantKytTxnCreated](transaction-monitoring-webhooks#applicantkyttxncreated)           | Transaction was created successfully by your entity, or by another client as a mirrored transaction (in [Travel Rule](doc:travel-rule) scenarios) on your key.                                                                        |
| [applicantKytTxnApproved](transaction-monitoring-webhooks#applicantkyttxnapproved)         | Transaction was approved, and the transfer or deposition of assets/properties can be expected soon.                                                                                                                                   |
| [applicantKytTxnRejected](transaction-monitoring-webhooks#applicantkyttxnrejected)         | Checks have been completed, and the review result is — **rejected**.                                                                                                                                                                  |
| [applicantKytTxnReviewed](doc:transaction-monitoring-webhooks#applicantkyttxnreviewed)     | Ttransaction that was previously put on hold was reviewed by the officer and removed from the on-hold queue. You can soon expect the webhook to notify you on the review results.                                                     |
| [applicantKytTxnDeleted](doc:transaction-monitoring-webhooks#applicantkyttxndeleted)       | Transaction and all the related information were deleted.                                                                                                                                                                             |
| [applicantKytOnHold](transaction-monitoring-webhooks#applicantkytonhold)                   | Based on the [rules you applied](doc:tm-rules), the transaction was put on hold and queued for manual review by the dedicated expert. As soon as the transaction is reviewed, its status will be set to **applicant reviewed**.       |
| [applicantKytTxnAwaitingUser](transaction-monitoring-webhooks#applicantkyttxnawaitinguser) | Transaction status was set to **awaiting user**. This means that the rule requiring the applicant action, such as passing an additional check, was triggered. The scoring is stopped until the applicant completes the required flow. |
| [applicantKytTxnDataChanged](transaction-monitoring-webhooks#applicantkyttxndatachanged)   | Transaction data was [enriched](ref:enriching-transaction-with-travel-rule) by the service. This means that the wallet ownership was confirmed, and the transaction information is unmasked.                                          |

> 📘 Note
>
> Personal applicant information is not available in the webhook payload. To get this information, use  [this API method](/reference/get-applicant-data).

> 👍 Tip
>
> If you are not receiving webhooks, try to check your endpoints using [SSL Labs](https://www.ssllabs.com/ssltest/) or Docker.

# applicantKytTxnCreated

```json
// applicantKytTxnCreated
{
  "applicantType": "individual",
  "correlationId": "req-9b3a4f51-c0a7-4d3a-9f2c-9d7c1d4f7d22",
  "sandboxMode": false,
  "externalUserId": "customExternalUserId",
  "type": "applicantKytTxnCreated",
  "reviewStatus": "init",
  "createdAt": "2025-11-17 17:26:49+0000",
  "createdAtMs": "2025-11-17 17:26:49.676",
  "clientId": "coolClientId",
  "kytTxnId": "691b5ad93f7d5f23100611ca",
  "kytDataTxnId": "9682adb6-b2cc-429c-acae-f36312c34a95",
  "kytTxnType": "travelRule"
}
```

<Table>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        `applicantType`
      </td>

      <td>
        String
      </td>

      <td>
        Defines the applicant entity type:<ul><li><code>individual</code> — for applicants registered and checked as individuals.</li><li><code>company</code> — for applicants registered and checked as legal entities.</li></ul>
      </td>
    </tr>

    <tr>
      <td>
        `sandboxMode`
      </td>

      <td>
        Boolean
      </td>

      <td>
        Set to `true` if the webhook was sent from [Sandbox](doc:sandbox-mode).
      </td>
    </tr>

    <tr>
      <td>
        `externalUserId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique applicant identifier as registered on your side.

        When [creating an applicant](ref:create-applicants), you can generate and add the `externalUserId` manually, or it will be automatically generated and added to the applicant profile by Sumsub.
      </td>
    </tr>

    <tr>
      <td>
        `type`
      </td>

      <td>
        String
      </td>

      <td>
        Webhook type. In this context, it is `applicantKytTxnCreated`.
      </td>
    </tr>

    <tr>
      <td>
        `reviewStatus`
      </td>

      <td>
        String
      </td>

      <td>
        Indicates the current transaction status (`init`, `onHold`, `completed`).
      </td>
    </tr>

    <tr>
      <td>
        `createdAt`
      </td>

      <td>
        Date
      </td>

      <td>
        Date and time when the webhook was created (format `yyyy-MM-dd HH:mm:ss+0000`, for example, `2021-05-14 16:00:25+0000`) in UTC.
      </td>
    </tr>

    <tr>
      <td>
        `createdAtMs`
      </td>

      <td>
        Date
      </td>

      <td>
        Date and time when the webhook was created, considering milliseconds (format `yyyy-MM-dd HH:mm:ss.fff`, for example, `2021-05-14 16:00:25.032`) in UTC.
      </td>
    </tr>

    <tr>
      <td>
        `clientId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of you as our client in the Sumsub system.

        This identifier is assigned to you when you are registered in and get access to the Sumsub system. It usually resembles your name or your company name. `clientId` is automatically added to the applicant profile when it is created.
      </td>
    </tr>

    <tr>
      <td>
        `kytTxnId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique transaction identifier (`.id`) on the Sumsub side.
      </td>
    </tr>

    <tr>
      <td>
        `kytDataTxnId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique transaction identifier (`data.txnId`) on your side.
      </td>
    </tr>

    <tr>
      <td>
        `kytTxnType`
      </td>

      <td>
        String
      </td>

      <td>
        Transaction type. Expects values:<ul><li><code>finance</code></li><li><code>kyc</code></li><li><code>travelRule</code></li><li><code>userPlatformEvent</code></ul>
      </td>
    </tr>
  </tbody>
</Table>

# applicantKytTxnApproved

```json
{
  "applicantId": "634829375766b80001a40152",
  "applicantType": "individual",
  "correlationId": "f24f6616020245053139a6537303a251",
  "sandboxMode": false,
  "externalUserId": "customExternalUserId",
  "type": "applicantKytTxnApproved",
  "reviewResult": {
    "reviewAnswer": "GREEN"
  },
  "reviewStatus": "completed",
  "createdAt": "2024-04-24 11:15:09+0000",
  "createdAtMs": "2024-04-24 11:15:09.446",
  "clientId": "coolClientId",
  "kytTxnId": "64a7dc05fbf57c624afcb72d",
  "kytDataTxnId": "uauu08x44xexbohyh4lkp9",
  "kytTxnType": "finance"
}
```

<Table>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        `applicantId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of the applicant in the Sumsub system.
      </td>
    </tr>

    <tr>
      <td>
        `applicantType`
      </td>

      <td>
        String
      </td>

      <td>
        Defines the applicant entity type:<ul><li><code>individual</code> — for applicants registered and checked as individuals.</li><li><code>company</code> — for applicants registered and checked as legal entities.</li></ul>
      </td>
    </tr>

    <tr>
      <td>
        `correlationId`
      </td>

      <td>
        String
      </td>

      <td>
        A shared identifier assigned to the originating request and propagated across all related events. Multiple events may share the same `correlationId` when triggered by the same operation.
      </td>
    </tr>

    <tr>
      <td>
        `sandboxMode`
      </td>

      <td>
        Boolean
      </td>

      <td>
        Set to `true` if the webhook was sent from [Sandbox](doc:sandbox-mode).
      </td>
    </tr>

    <tr>
      <td>
        `externalUserId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique applicant identifier as registered on your side.

        When [creating an applicant](ref:create-applicants), you can generate and add the `externalUserId` manually, or it will be automatically generated and added to the applicant profile by Sumsub.
      </td>
    </tr>

    <tr>
      <td>
        `type`
      </td>

      <td>
        String
      </td>

      <td>
        Webhook type. In this context, it is `applicantKytTxnApproved`.
      </td>
    </tr>

    <tr>
      <td>
        `reviewResult`
      </td>

      <td>
        [Object](ref:get-transaction#reviewresult-attributes)
      </td>

      <td>
        Contains extra information on the transaction verification results.
      </td>
    </tr>

    <tr>
      <td>
        `reviewStatus`
      </td>

      <td>
        String
      </td>

      <td>
        Indicates the current transaction status (`init`, `onHold`, `completed`).
      </td>
    </tr>

    <tr>
      <td>
        `createdAt`
      </td>

      <td>
        Date
      </td>

      <td>
        Date and time when the webhook was created (format `yyyy-MM-dd HH:mm:ss+0000`, for example, `2021-05-14 16:00:25+0000`) in UTC.
      </td>
    </tr>

    <tr>
      <td>
        `createdAtMs`
      </td>

      <td>
        Date
      </td>

      <td>
        Date and time when the webhook was created, considering milliseconds (format `yyyy-MM-dd HH:mm:ss.fff`, for example, `2021-05-14 16:00:25.032`) in UTC.
      </td>
    </tr>

    <tr>
      <td>
        `clientId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of you as our client in the Sumsub system.

        This identifier is assigned to you when you are registered in and get access to the Sumsub system. It usually resembles your name or your company name. `clientId` is automatically added to the applicant profile when it is created.
      </td>
    </tr>

    <tr>
      <td>
        `kytTxnId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique transaction identifier (`.id`) on the Sumsub side.
      </td>
    </tr>

    <tr>
      <td>
        `kytDataTxnId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique transaction identifier (`data.txnId`) on your side.
      </td>
    </tr>

    <tr>
      <td>
        `kytTxnType`
      </td>

      <td>
        String
      </td>

      <td>
        Transaction type. Expects values:<ul><li><code>finance</code></li><li><code>kyc</code></li><li><code>travelRule</code></li><li><code>userPlatformEvent</code></ul>
      </td>
    </tr>
  </tbody>
</Table>

# applicantKytTxnRejected

```json
{
  "applicantId": "634829375766b80001a40152",
  "applicantType": "individual",
  "correlationId": "0f5a7c828bab750775564534fc0470a8",
  "sandboxMode": false,
  "externalUserId": "customExternalUserId",
  "type": "applicantKytTxnRejected",
  "reviewResult": {
    "reviewAnswer": "RED",
    "reviewRejectType": "FINAL"
  },
  "reviewStatus": "completed",
  "createdAt": "2024-04-24 11:15:09+0000",
  "createdAtMs": "2024-04-24 11:15:09.446",
  "clientId": "coolClientId",
  "kytTxnId": "64a7dc05fbf57c624afcb72d",
  "kytDataTxnId": "j8bqz29yn491vksi9qfydw",
  "kytTxnType": "finance"
}
```

<Table>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        `applicantId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of the applicant in the Sumsub system.
      </td>
    </tr>

    <tr>
      <td>
        `applicantType`
      </td>

      <td>
        String
      </td>

      <td>
        Defines the applicant entity type:<ul><li><code>individual</code> — for applicants registered and checked as individuals.</li><li><code>company</code> — for applicants registered and checked as legal entities.</li></ul>
      </td>
    </tr>

    <tr>
      <td>
        `correlationId`
      </td>

      <td>
        String
      </td>

      <td>
        A shared identifier assigned to the originating request and propagated across all related events. Multiple events may share the same `correlationId` when triggered by the same operation.
      </td>
    </tr>

    <tr>
      <td>
        `sandboxMode`
      </td>

      <td>
        Boolean
      </td>

      <td>
        Set to `true` if the webhook was sent from [Sandbox](doc:sandbox-mode).
      </td>
    </tr>

    <tr>
      <td>
        `externalUserId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique applicant identifier as registered on your side.

        When [creating an applicant](ref:create-applicants), you can generate and add the `externalUserId` manually, or it will be automatically generated and added to the applicant profile by Sumsub.
      </td>
    </tr>

    <tr>
      <td>
        `type`
      </td>

      <td>
        String
      </td>

      <td>
        Webhook type. In this context, it is `applicantKytTxnRejected`.
      </td>
    </tr>

    <tr>
      <td>
        `reviewResult`
      </td>

      <td>
        [Object](ref:get-transaction#reviewresult-attributes)
      </td>

      <td>
        Contains extra information on the transaction verification results.
      </td>
    </tr>

    <tr>
      <td>
        `reviewStatus`
      </td>

      <td>
        String
      </td>

      <td>
        Indicates the current transaction status (`init`, `onHold`, `completed`).
      </td>
    </tr>

    <tr>
      <td>
        `createdAt`
      </td>

      <td>
        Date
      </td>

      <td>
        Date and time when the webhook was created (format `yyyy-MM-dd HH:mm:ss+0000`, for example, `2021-05-14 16:00:25+0000`) in UTC.
      </td>
    </tr>

    <tr>
      <td>
        `createdAtMs`
      </td>

      <td>
        Date
      </td>

      <td>
        Date and time when the webhook was created, considering milliseconds (format `yyyy-MM-dd HH:mm:ss.fff`, for example, `2021-05-14 16:00:25.032`) in UTC.
      </td>
    </tr>

    <tr>
      <td>
        `clientId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of you as our client in the Sumsub system.

        This identifier is assigned to you when you are registered in and get access to the Sumsub system. It usually resembles your name or your company name. `clientId` is automatically added to the applicant profile when it is created.
      </td>
    </tr>

    <tr>
      <td>
        `kytTxnId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique transaction identifier (`.id`) on the Sumsub side.
      </td>
    </tr>

    <tr>
      <td>
        `kytDataTxnId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique transaction identifier (`data.txnId`) on your side.
      </td>
    </tr>

    <tr>
      <td>
        `kytTxnType`
      </td>

      <td>
        String
      </td>

      <td>
        Transaction type. Expects values:<ul><li><code>finance</code></li><li><code>kyc</code></li><li><code>travelRule</code></li><li><code>userPlatformEvent</code></ul>
      </td>
    </tr>
  </tbody>
</Table>

# applicantKytTxnReviewed

```json
{
  "applicantId": "634829375766b80001a40152",
  "applicantType": "individual",
  "correlationId": "0f5a7c828bab750775564534fc0470a8",
  "sandboxMode": false,
  "externalUserId": "customExternalUserId",
  "type": "applicantKytTxnReviewed",
  "reviewResult": {
    "reviewAnswer": "RED",
    "reviewRejectType": "FINAL"
  },
  "reviewStatus": "completed",
  "createdAt": "2024-04-24 11:15:09+0000",
  "createdAtMs": "2024-04-24 11:15:09.446",
  "clientId": "coolClientId",
  "kytTxnId": "64a7dc05fbf57c624afcb72d",
  "kytDataTxnId": "j8bqz29yn491vksi9qfydw",
  "kytTxnType": "finance"
}
```

<Table>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        `applicantId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of the applicant in the Sumsub system.
      </td>
    </tr>

    <tr>
      <td>
        `applicantType`
      </td>

      <td>
        String
      </td>

      <td>
        Defines the applicant entity type:<ul><li><code>individual</code> — for applicants registered and checked as individuals.</li><li><code>company</code> — for applicants registered and checked as legal entities.</li></ul>
      </td>
    </tr>

    <tr>
      <td>
        `correlationId`
      </td>

      <td>
        String
      </td>

      <td>
        A shared identifier assigned to the originating request and propagated across all related events. Multiple events may share the same `correlationId` when triggered by the same operation.
      </td>
    </tr>

    <tr>
      <td>
        `sandboxMode`
      </td>

      <td>
        Boolean
      </td>

      <td>
        Set to `true` if the webhook was sent from [Sandbox](doc:sandbox-mode).
      </td>
    </tr>

    <tr>
      <td>
        `externalUserId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique applicant identifier as registered on your side.

        When [creating an applicant](ref:create-applicants), you can generate and add the `externalUserId` manually, or it will be automatically generated and added to the applicant profile by Sumsub.
      </td>
    </tr>

    <tr>
      <td>
        `type`
      </td>

      <td>
        String
      </td>

      <td>
        Webhook type. In this context, it is `applicantKytTxnReviewed`.
      </td>
    </tr>

    <tr>
      <td>
        `reviewResult`
      </td>

      <td>
        [Object](ref:get-transaction#reviewresult-attributes)
      </td>

      <td>
        Contains extra information on the transaction verification results.
      </td>
    </tr>

    <tr>
      <td>
        `reviewStatus`
      </td>

      <td>
        String
      </td>

      <td>
        Indicates the current transaction status (`init`, `onHold`, `completed`).
      </td>
    </tr>

    <tr>
      <td>
        `createdAt`
      </td>

      <td>
        Date
      </td>

      <td>
        Date and time when the webhook was created (format `yyyy-MM-dd HH:mm:ss+0000`, for example, `2021-05-14 16:00:25+0000`) in UTC.
      </td>
    </tr>

    <tr>
      <td>
        `createdAtMs`
      </td>

      <td>
        Date
      </td>

      <td>
        Date and time when the webhook was created, considering milliseconds (format `yyyy-MM-dd HH:mm:ss.fff`, for example, `2021-05-14 16:00:25.032`) in UTC.
      </td>
    </tr>

    <tr>
      <td>
        `clientId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of you as our client in the Sumsub system.

        This identifier is assigned to you when you are registered in and get access to the Sumsub system. It usually resembles your name or your company name. `clientId` is automatically added to the applicant profile when it is created.
      </td>
    </tr>

    <tr>
      <td>
        `kytTxnId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique transaction identifier (`.id`) on the Sumsub side.
      </td>
    </tr>

    <tr>
      <td>
        `kytDataTxnId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique transaction identifier (`data.txnId`) on your side.
      </td>
    </tr>

    <tr>
      <td>
        `kytTxnType`
      </td>

      <td>
        String
      </td>

      <td>
        Transaction type. Expects values:<ul><li><code>finance</code></li><li><code>kyc</code></li><li><code>travelRule</code></li><li><code>userPlatformEvent</code></ul>
      </td>
    </tr>
  </tbody>
</Table>

# applicantKytTxnDeleted

```json
{
  "applicantId": "634829375766b80001a40152",
  "applicantType": "individual",
  "correlationId": "0f5a7c828bab750775564534fc0470a8",
  "sandboxMode": false,
  "externalUserId": "customExternalUserId",
  "type": "applicantKytTxnDeleted",
  "reviewStatus": "completed",
  "createdAt": "2024-04-24 11:15:09+0000",
  "createdAtMs": "2024-04-24 11:15:09.446",
  "clientId": "coolClientId",
  "kytTxnId": "64a7dc05fbf57c624afcb72d",
  "kytDataTxnId": "j8bqz29yn491vksi9qfydw",
  "kytTxnType": "finance"
}
```

<Table>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        `applicantId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of the applicant in the Sumsub system.
      </td>
    </tr>

    <tr>
      <td>
        `applicantType`
      </td>

      <td>
        String
      </td>

      <td>
        Defines the applicant entity type:<ul><li><code>individual</code> — for applicants registered and checked as individuals.</li><li><code>company</code> — for applicants registered and checked as legal entities.</li></ul>
      </td>
    </tr>

    <tr>
      <td>
        `correlationId`
      </td>

      <td>
        String
      </td>

      <td>
        A shared identifier assigned to the originating request and propagated across all related events. Multiple events may share the same `correlationId` when triggered by the same operation.
      </td>
    </tr>

    <tr>
      <td>
        `sandboxMode`
      </td>

      <td>
        Boolean
      </td>

      <td>
        Set to `true` if the webhook was sent from [Sandbox](doc:sandbox-mode).
      </td>
    </tr>

    <tr>
      <td>
        `externalUserId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique applicant identifier as registered on your side.

        When [creating an applicant](ref:create-applicants), you can generate and add the `externalUserId` manually, or it will be automatically generated and added to the applicant profile by Sumsub.
      </td>
    </tr>

    <tr>
      <td>
        `type`
      </td>

      <td>
        String
      </td>

      <td>
        Webhook type. In this context, it is `applicantKytTxnDeleted`.
      </td>
    </tr>

    <tr>
      <td>
        `reviewStatus`
      </td>

      <td>
        String
      </td>

      <td>
        Indicates the current transaction status (`init`, `onHold`, `completed`).
      </td>
    </tr>

    <tr>
      <td>
        `createdAt`
      </td>

      <td>
        Date
      </td>

      <td>
        Date and time when the webhook was created (format `yyyy-MM-dd HH:mm:ss+0000`, for example, `2021-05-14 16:00:25+0000`) in UTC.
      </td>
    </tr>

    <tr>
      <td>
        `createdAtMs`
      </td>

      <td>
        Date
      </td>

      <td>
        Date and time when the webhook was created, considering milliseconds (format `yyyy-MM-dd HH:mm:ss.fff`, for example, `2021-05-14 16:00:25.032`) in UTC.
      </td>
    </tr>

    <tr>
      <td>
        `clientId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of you as our client in the Sumsub system.

        This identifier is assigned to you when you are registered in and get access to the Sumsub system. It usually resembles your name or your company name. `clientId` is automatically added to the applicant profile when it is created.
      </td>
    </tr>

    <tr>
      <td>
        `kytTxnId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique transaction identifier (`.id`) on the Sumsub side.
      </td>
    </tr>

    <tr>
      <td>
        `kytDataTxnId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique transaction identifier (`data.txnId`) on your side.
      </td>
    </tr>

    <tr>
      <td>
        `kytTxnType`
      </td>

      <td>
        String
      </td>

      <td>
        Transaction type. Expects values:<ul><li><code>finance</code></li><li><code>kyc</code></li><li><code>travelRule</code></li><li><code>userPlatformEvent</code></ul>
      </td>
    </tr>
  </tbody>
</Table>

# applicantKytOnHold

```json
{
  "applicantId": "634829375766b80001a40152",
  "applicantType": "individual",
  "correlationId": "98d4dac61c977c1b3f81d6ab78d29c3c",
  "sandboxMode": false,
  "externalUserId": "customExternalUserId",
  "type": "applicantKytOnHold",
  "reviewStatus": "onHold",
  "createdAt": "2024-04-24 11:15:09+0000",
  "createdAtMs": "2024-04-24 11:15:09.446",
  "clientId": "coolClientId",
  "kytTxnId": "64a7dc05fbf57c624afcb72d",
  "kytDataTxnId": "j8bqz29yn491vksi9qfydw",
  "kytTxnType": "finance"
}
```

<Table>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        `applicantId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of the applicant in the Sumsub system.
      </td>
    </tr>

    <tr>
      <td>
        `applicantType`
      </td>

      <td>
        String
      </td>

      <td>
        Defines the applicant entity type:<ul><li><code>individual</code> — for applicants registered and checked as individuals.</li><li><code>company</code> — for applicants registered and checked as legal entities.</li></ul>
      </td>
    </tr>

    <tr>
      <td>
        `correlationId`
      </td>

      <td>
        String
      </td>

      <td>
        A shared identifier assigned to the originating request and propagated across all related events. Multiple events may share the same `correlationId` when triggered by the same operation.
      </td>
    </tr>

    <tr>
      <td>
        `sandboxMode`
      </td>

      <td>
        Boolean
      </td>

      <td>
        Set to `true` if the webhook was sent from [Sandbox](doc:sandbox-mode).
      </td>
    </tr>

    <tr>
      <td>
        `externalUserId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique applicant identifier as registered on your side.

        When [creating an applicant](ref:create-applicants), you can generate and add the `externalUserId` manually, or it will be automatically generated and added to the applicant profile by Sumsub.
      </td>
    </tr>

    <tr>
      <td>
        `type`
      </td>

      <td>
        String
      </td>

      <td>
        Webhook type. In this context, it is `applicantKytOnHold`.
      </td>
    </tr>

    <tr>
      <td>
        `reviewStatus`
      </td>

      <td>
        String
      </td>

      <td>
        Indicates the current transaction status (`init`, `onHold`, `completed`).
      </td>
    </tr>

    <tr>
      <td>
        `createdAt`
      </td>

      <td>
        Date
      </td>

      <td>
        Date and time when the webhook was created (format `yyyy-MM-dd HH:mm:ss+0000`, for example, `2021-05-14 16:00:25+0000`) in UTC.
      </td>
    </tr>

    <tr>
      <td>
        `createdAtMs`
      </td>

      <td>
        Date
      </td>

      <td>
        Date and time when the webhook was created, considering milliseconds (format `yyyy-MM-dd HH:mm:ss.fff`, for example, `2021-05-14 16:00:25.032`) in UTC.
      </td>
    </tr>

    <tr>
      <td>
        `clientId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of you as our client in the Sumsub system.

        This identifier is assigned to you when you are registered in and get access to the Sumsub system. It usually resembles your name or your company name. `clientId` is automatically added to the applicant profile when it is created.
      </td>
    </tr>

    <tr>
      <td>
        `kytTxnId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique transaction identifier (`.id`) on the Sumsub side.
      </td>
    </tr>

    <tr>
      <td>
        `kytDataTxnId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique transaction identifier (`data.txnId`) on your side.
      </td>
    </tr>

    <tr>
      <td>
        `kytTxnType`
      </td>

      <td>
        String
      </td>

      <td>
        Transaction type. Expects values:<ul><li><code>finance</code></li><li><code>kyc</code></li><li><code>travelRule</code></li><li><code>userPlatformEvent</code></ul>
      </td>
    </tr>
  </tbody>
</Table>

# applicantKytTxnAwaitingUser

```json
{
  "applicantId": "6447b564728bf40939a7664f",
  "applicantType": "individual",
  "correlationId": "7310f3ffddbff223cdf10221cdf12064",
  "sandboxMode": false,
  "externalUserId": "customExternalUserId",
  "type": "applicantKytTxnAwaitingUser",
  "reviewStatus": "awaitingUser",
  "createdAt": "2023-12-11 10:41:54+0000",
  "createdAtMs": "2023-12-11 10:41:54.431",
  "clientId": "coolClientId",
  "kytTxnId": "6576e772b2f80732714d1de0",
  "kytDataTxnId": "m26m980m9jd7pozq72se4",
  "kytTxnType": "finance"
}
```

<Table>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        `applicantId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of the applicant in the Sumsub system.
      </td>
    </tr>

    <tr>
      <td>
        `applicantType`
      </td>

      <td>
        String
      </td>

      <td>
        Defines the applicant entity type:<ul><li><code>individual</code> — for applicants registered and checked as individuals.</li><li><code>company</code> — for applicants registered and checked as legal entities.</li></ul>
      </td>
    </tr>

    <tr>
      <td>
        `correlationId`
      </td>

      <td>
        String
      </td>

      <td>
        A shared identifier assigned to the originating request and propagated across all related events. Multiple events may share the same `correlationId` when triggered by the same operation.
      </td>
    </tr>

    <tr>
      <td>
        `sandboxMode`
      </td>

      <td>
        Boolean
      </td>

      <td>
        Set to `true` if the webhook was sent from [Sandbox](doc:sandbox-mode).
      </td>
    </tr>

    <tr>
      <td>
        `externalUserId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique applicant identifier as registered on your side.

        When [creating an applicant](ref:create-applicants), you can generate and add the `externalUserId` manually, or it will be automatically generated and added to the applicant profile by Sumsub.
      </td>
    </tr>

    <tr>
      <td>
        `type`
      </td>

      <td>
        String
      </td>

      <td>
        Webhook type. In this context, it is `applicantKytTxnAwaitingUser`.
      </td>
    </tr>

    <tr>
      <td>
        `reviewStatus`
      </td>

      <td>
        String
      </td>

      <td>
        Indicates the current transaction status (`init`, `onHold`, `completed`).
      </td>
    </tr>

    <tr>
      <td>
        `createdAt`
      </td>

      <td>
        Date
      </td>

      <td>
        Date and time when the webhook was created (format `yyyy-MM-dd HH:mm:ss+0000`, for example, `2021-05-14 16:00:25+0000`) in UTC.
      </td>
    </tr>

    <tr>
      <td>
        `createdAtMs`
      </td>

      <td>
        Date
      </td>

      <td>
        Date and time when the webhook was created, considering milliseconds (format `yyyy-MM-dd HH:mm:ss.fff`, for example, `2021-05-14 16:00:25.032`) in UTC.
      </td>
    </tr>

    <tr>
      <td>
        `clientId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of you as our client in the Sumsub system.

        This identifier is assigned to you when you are registered in and get access to the Sumsub system. It usually resembles your name or your company name. `clientId` is automatically added to the applicant profile when it is created.
      </td>
    </tr>

    <tr>
      <td>
        `kytTxnId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique transaction identifier (`.id`) on the Sumsub side.
      </td>
    </tr>

    <tr>
      <td>
        `kytDataTxnId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique transaction identifier (`data.txnId`) on your side.
      </td>
    </tr>

    <tr>
      <td>
        `kytTxnType`
      </td>

      <td>
        String
      </td>

      <td>
        Transaction type. Expects values:<ul><li><code>finance</code></li><li><code>kyc</code></li><li><code>travelRule</code></li><li><code>userPlatformEvent</code></ul>
      </td>
    </tr>
  </tbody>
</Table>

# applicantKytTxnDataChanged

```json
{
  "applicantId": "6447b564728bf40939a7664f",
  "applicantType": "individual",
  "correlationId": "fb36d7a2f2e1ac15773ec9a56f999dde",
  "sandboxMode": false,
  "externalUserId": "customExternalUserId",
  "type": "applicantKytTxnDataChanged",
  "reviewResult": {
    "reviewAnswer": "GREEN"
  },
  "reviewStatus": "completed",
  "createdAt": "2024-01-24 07:38:34+0000",
  "createdAtMs": "2024-01-24 07:38:34.994",
  "clientId": "coolClientId",
  "kytTxnId": "6576e772b2f80732714d1de0",
  "kytDataTxnId": "m26m980m9jd7pozq72se4",
  "kytTxnType": "finance"
}
```

<Table>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        `applicantId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of the applicant in the Sumsub system.
      </td>
    </tr>

    <tr>
      <td>
        `applicantType`
      </td>

      <td>
        String
      </td>

      <td>
        Defines the applicant entity type:<ul><li><code>individual</code> — for applicants registered and checked as individuals.</li><li><code>company</code> — for applicants registered and checked as legal entities.</li></ul>
      </td>
    </tr>

    <tr>
      <td>
        `correlationId`
      </td>

      <td>
        String
      </td>

      <td>
        A shared identifier assigned to the originating request and propagated across all related events. Multiple events may share the same `correlationId` when triggered by the same operation.
      </td>
    </tr>

    <tr>
      <td>
        `sandboxMode`
      </td>

      <td>
        Boolean
      </td>

      <td>
        Set to `true` if the webhook was sent from [Sandbox](doc:sandbox-mode).
      </td>
    </tr>

    <tr>
      <td>
        `externalUserId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique applicant identifier as registered on your side.

        When [creating an applicant](ref:create-applicants) , you can generate and add the `externalUserId` manually, or it will be automatically generated and added to the applicant profile by Sumsub.
      </td>
    </tr>

    <tr>
      <td>
        `type`
      </td>

      <td>
        String
      </td>

      <td>
        Webhook type. In this context, it is `applicantKytTxnDataChanged`.
      </td>
    </tr>

    <tr>
      <td>
        `reviewResult`
      </td>

      <td>
        [Object](ref:get-transaction#reviewresult-attributes)
      </td>

      <td>
        Contains extra information on the transaction verification results.
      </td>
    </tr>

    <tr>
      <td>
        `reviewStatus`
      </td>

      <td>
        String
      </td>

      <td>
        Indicates the current transaction status (`init`, `onHold`, `completed`).
      </td>
    </tr>

    <tr>
      <td>
        `createdAt`
      </td>

      <td>
        Date
      </td>

      <td>
        Date and time when the webhook was created (format `yyyy-MM-dd HH:mm:ss+0000`, for example, `2021-05-14 16:00:25+0000`) in UTC.
      </td>
    </tr>

    <tr>
      <td>
        `createdAtMs`
      </td>

      <td>
        Date
      </td>

      <td>
        Date and time when the webhook was created, considering milliseconds (format `yyyy-MM-dd HH:mm:ss.fff`, for example, `2021-05-14 16:00:25.032`) in UTC.
      </td>
    </tr>

    <tr>
      <td>
        `clientId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of you as our client in the Sumsub system.

        This identifier is assigned to you when you are registered in and get access to the Sumsub system. It usually resembles your name or your company name. `clientId` is automatically added to the applicant profile when it is created.
      </td>
    </tr>

    <tr>
      <td>
        `kytTxnId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique transaction identifier (`.id`) on the Sumsub side.
      </td>
    </tr>

    <tr>
      <td>
        `kytDataTxnId`
      </td>

      <td>
        String
      </td>

      <td>
        Unique transaction identifier (`data.txnId`) on your side.
      </td>
    </tr>

    <tr>
      <td>
        `kytTxnType`
      </td>

      <td>
        String
      </td>

      <td>
        Transaction type. Expects values:<ul><li><code>finance</code></li><li><code>kyc</code></li><li><code>travelRule</code></li><li><code>userPlatformEvent</code></ul>
      </td>
    </tr>
  </tbody>
</Table>

<br />
