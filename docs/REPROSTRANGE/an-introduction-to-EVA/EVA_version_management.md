---
title: Version management
hidden: false
---
As the Entity Verification API (EVA) evolves, we prioritize backward compatibility. We are implementing URI-based and semantic versioning to ensure clarity for breaking down the changes as the API grows.

<Callout icon="ℹ️" theme="info">
  The URI only contains the primary version number.
</Callout>

## Key characteristics

The following table outlines the key characteristics of EVA's versioning:

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Characteristic
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        URI versioning
      </td>

      <td>
        All API requests specify the major version in the URI path.
        For example: `https://api.kyc.moodys.com/eva/api/v1/`

        > Note that in the API URI, only the main version is referenced.
      </td>
    </tr>

    <tr>
      <td>
        Authentication
      </td>

      <td>
        You are able to access different versions using the same credentials.

        > Note that each version of the API has a different URI.
      </td>
    </tr>

    <tr>
      <td>
        Semantic versioning
      </td>

      <td>
        The API versions follow `MAJOR.MINOR.PATCH` notation where:

        * `MAJOR` denotes the incremental breaking changes.
        * `MINOR` denotes the addition of backward-compatible features.
        * `PATCH` denotes the fix bugs without altering functionality.

        For example, v1.2.0 implies major version 1, minor version 2, patch 0.

        > Note that:
        >
        > * Backward-incompatible changes to the API increment the major version.
        > * Backward-compatible additions or changes to the API increment the minor version.
        > * Bug fixes that do not affect the API increment the patch version.
      </td>
    </tr>

    <tr>
      <td>
        Deprecation warnings
      </td>

      <td>
        Responses from deprecated endpoints include `Deprecation` headers.
      </td>
    </tr>

    <tr>
      <td>
        Version discovery
      </td>

      <td>
        The current version in headers

        * HTTP/1.1 200 OK
        * API-Version: 1.2.0.
        * Deprecation: sunset="2025-12-01" (if announced)
      </td>
    </tr>

    <tr>
      <td>
        Sunset period
      </td>

      <td>
        Minimum 3 months between deprecation notice and version retirement.
      </td>
    </tr>
  </tbody>
</Table>

<Callout icon="ℹ️" theme="info">
  Adding new endpoints or endpoint families does not require increment in versioning. New endpoints can be added to a stable version as well.
</Callout>

### Additional information for the GET endpoints

The response structure obtained through `GET`methods corresponds to the version specified in the URI. For instance, a request made to `https://api.kyc.moodys.com/eva/api/v1/entityData/{entityDataId}` yields a response structure that aligns with version 1, while a request to `https://api.kyc.moodys.com/eva/api/v2/entityData/{entityDataId}` returns a structure that matches version 2.

A response, represented by an `entityDataId` that has been made with a certain version, is available to retrieve with later versions.

<Callout icon="❗️" theme="error">
  There is a possibility of data loss for certain data points within the response if trying to retrieve a response with later versions.
</Callout>

Similarly, an `entityDataId` that represents a request made with a certain version, is available to retrieve with an earlier version's `GET`, but as a major change may contain breaking changes.

<Callout icon="ℹ️" theme="info">
  There is no assurance of backward compatibility.
</Callout>

## Version change

The following table outlines the process of version change in EVA:

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Process stage
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Stable period
      </td>

      <td>
        The current stable version, which may already have an announced deprecation date.

        > Note that during the stable period, only minor and patch-type changes are permitted for a version.
      </td>
    </tr>

    <tr>
      <td>
        Transitioning period
      </td>

      <td>
        The version that is transitioning to stable as the feature and change period comes to an end.
      </td>
    </tr>

    <tr>
      <td>
        Major version release
      </td>

      <td>
        The version that incorporates all the breaking changes after the previous version has become stable.
      </td>
    </tr>
  </tbody>
</Table>

<Callout icon="ℹ️" theme="info">
  At any given time, at least one major version must be available and a maximum of three major versions may be available.
</Callout>

## Visual explanation of EVA versions

<Image align="left" border={true} src="https://files.readme.io/f4e018ef8a7cf1616ca8f516ce49a764f8b97d8c121bee71f84d3490800a9d0b-EVA_versioning_flow.jpg" className="border" />

<br />

<br />

<br />

<br />

<br />

The following table outlines the key points from the image above:

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Points
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        A
      </td>

      <td>
        There should be a minimum of three months between the announcement of the deprecation date and the actual deprecation date.
      </td>
    </tr>

    <tr>
      <td>
        B
      </td>

      <td>
        Announcement of the deprecation date.
      </td>
    </tr>

    <tr>
      <td>
        C
      </td>

      <td>
        At least six weeks should elapse between the announcement of the final feature list for the new version and the deprecation date of the previous version.
      </td>
    </tr>

    <tr>
      <td>
        D
      </td>

      <td>
        Announcement of the final change log between two major versions.

        > Note that there is no guarantee that B and D will occur simultaneously; however, D must take place either before or concurrently with B.
      </td>
    </tr>

    <tr>
      <td>
        E
      </td>

      <td>
        A new, non-stable, version may be released either before or after the previous version has stabilized.
      </td>
    </tr>
  </tbody>
</Table>

## Communication

The future communication channels will consist of EVA portal articles and service messages. Until these platforms and features are available, communication occurs through direct emails.

## Resources

Resources are available for each version:

* A separate OpenAPI version provides details for each version.

* The EVA portal console should support reaching the different versions.

* The EVA portal should support reaching the different versions of the openAPI.

* The Postman collection reflects if any features work differently in any version.

* An example of the `outputStructure` is also provided per version.

## References

* [Semantic Versioning (SemVer)](https://semver.org/)

* [IETF RFC 2119](https://tools.ietf.org/html/rfc2119) (Key terms: MUST, SHOULD, MAY)
