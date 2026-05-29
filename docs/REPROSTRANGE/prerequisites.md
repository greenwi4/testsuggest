---
title: Prerequisites
deprecated: false
hidden: false
metadata:
  robots: index
next:
  pages:
    - slug: about-evas-sandbox
      title: About EVA's sandbox
      type: basic
---
There are several API requests, cURL commands, and response snippets throughout this documentation. Make a note of the following before you get started.

## Annotation

* Strings are displayed in curly brackets within the documentation. For example, `{entityDataId}`. Substitute the strings for actual values as per your requirement.
* Potential lists of values are displayed in curly brackets divided with a pipe symbol. For example, `{in progress|completed|failed|partially failed}`.
* Truncated content is represented by three dots in curly brackets: `{...}`. The truncated content is treated as a string to ensure the validity of the JSON files displayed as examples.

## Request and response audit fields

The following table outlines the information about the request and response audit fields available across the API:

| Field name       | Description                                                                                                                                           |
| :--------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------- |
| `requestTime`    | The time at which the `POST` request reaches the EVA server.                                                                                          |
| `responseTime`   | The time at which the `POST` response departs from the EVA server.                                                                                    |
| `completionTime` | The time at which the `POST` response is prepared, or when the status field value transitions to either `completed`, `partially failed`, or `failed`. |

## Case sensitivity of API parameters

All of the API endpoints are case-insensitive, so all the parameters in a request can be provided in lowercase, uppercase, or any combination of cases. For example:

* gilkndrrdkophbjihg
* GILKNDRRDKOPHBJIHG
* GilkNdrRDkoPHbjiHg

## API call limits

There are some limitations with regard to the number of times you can call the API. The following table outlines those limits:

| Frequency  | Maximum number of API calls allowed |
| :--------- | :---------------------------------- |
| Per minute | 120                                 |
| Per day    | 25,000                              |
| Per month  | 500,000                             |

<Callout icon="ℹ️" theme="info">
  These limits prevent misuse or overload of the national register sources, ensuring a stable and reliable API experience for all users.
</Callout>
