---
title: ssdfsd
deprecated: false
hidden: false
metadata:
  robots: index
---
# Request Parameters

<Table align={["left","left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Parameters
      </th>

      <th>
        Notes
      </th>

      <th>
        Type
      </th>

      <th>
        Required
      </th>

      <th>
        Possible Values
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        advertiserId
      </td>

      <td>
        ID of advertiser whose campaign is to be scheduled
      </td>

      <td>
        integer
      </td>

      <td>
        Y
      </td>

      <td>
        Advertiser ID for which the campaign is to be created
      </td>
    </tr>

    <tr>
      <td>
        name
      </td>

      <td>
        The name of the campaign<br />**_Note_**_: Limit on length of campaign name is 240 characters_
      </td>

      <td>
        string
      </td>

      <td>
        Y
      </td>

      <td>
        The campaign name should be unique
      </td>
    </tr>

    <tr>
      <td>
        description
      </td>

      <td>
        Campaign description<br />**_Note_**_: Limit on length of campaign description is 240 characters_
      </td>

      <td>
        string
      </td>

      <td>
        N
      </td>

      <td>
        Provide valid description corresponding to campaign type
      </td>
    </tr>

    <tr>
      <td>
        objective
      </td>

      <td>
        Campaign objective
      </td>

      <td>
        string
      </td>

      <td>
        N
      </td>

      <td>
        Values:<br />awareness (default value)<br />engagement<br />conversion<br />**_Note:_** For video campaigns, the only supported objective is `awareness`
      </td>
    </tr>

    <tr>
      <td>
        campaignType
      </td>

      <td>
        The type of the campaign
      </td>

      <td>
        string
      </td>

      <td>
        N
      </td>

      <td>
        Values of campaignType: ngd
      </td>
    </tr>

    <tr>
      <td>
        mediaType
      </td>

      <td>
        Specifies the campaign's creative format.
      </td>

      <td>
        string
      </td>

      <td>
        N
      </td>

      <td>
        Values:<br />banner (default value)<br />video
      </td>
    </tr>

    <tr>
      <td>
        startDate
      </td>

      <td>
        The date to start campaign<br />**_Note_**_: it must be set either at campaign or ad group level_
      </td>

      <td>
        date
      </td>

      <td>
        Conditional.This field is required only if it is not set at ad group level. Cannot be changed to ad group level later.
      </td>

      <td>
        Date should be in format:   yyyy-MM-dd'T'HH:mm:ss.SSSXXX

        **_Note_**_:_ <ul><li>_All timestamp values must be in ISO 8601 format (e.g., "2025-07-20T19:10:10-05:00").</li><li>All date-time values are internally converted to Eastern Time (ET) for processing and normalized to the start of the hour. This means minutes and seconds are truncated. Example: "2025-07-20T19:10:10-05:00" becomes "2025-07-20T19:00:00-05:00" in ET</li></ul><br />Kindly take these behaviors into consideration when assigning a value to startDate in your request._
      </td>
    </tr>

    <tr>
      <td>
        endDate
      </td>

      <td>
        The date when campaign ends<br />**_Note_**_: it must be set either at campaign or ad group level_
      </td>

      <td>
        date
      </td>

      <td>
        Conditional.This field is required only if it is not set at ad group level. Cannot be changed to ad group level later.
      </td>

      <td>
        Date should be in format:   yyyy-MM-dd'T'HH:mm:ss.SSSXXX

        To run campaign indefinitely, set its value as ‘9999-12-30T00:00:00Z’

        **_Note_**_:_<ul><li>_All timestamp values must be in ISO 8601 format (e.g., "2025-07-20T19:10:10-05:00").</li><li>All date-time values are internally converted to Eastern Time (ET) for processing and normalized to the start of the hour. This means minutes and seconds are truncated. Example: "2025-07-20T19:10:10-05:00" becomes "2025-07-20T19:00:00-05:00" in ET</li><li>The endDate must be set to a time after 12:00 PM ET. If the provided value is before 12:00 PM ET, the system will return an error.</li><li>Special Case: If you set endDate to exactly "00:00:00" ET (e.g., "2025-07-20T00:00:00-05:00"), it will be interpreted as the end of the previous day: "2025-07-19T23:59:59-05:00".</li></ul><br />Kindly take these behaviors into consideration when assigning a value to startDate in your request._
      </td>
    </tr>

    <tr>
      <td>
        budgetType
      </td>

      <td>
        The type of budget allocation you want to choose for your campaign

        **_Note_**_: it must be set either at campaign or ad group level_<br />_Campaigns scheduled to run indefinitely must use a daily budget_
      </td>

      <td>
        string
      </td>

      <td>
        Conditional.This field is required only if it is not set at ad group level. Cannot be changed to ad group level later.
      </td>

      <td>
        Values:

        - daily
        - total
      </td>
    </tr>

    <tr>
      <td>
        dailyBudget
      </td>

      <td>
        Daily budget of campaign<br />Note:<br />•	Daily budget cannot exceed your total budget amount<br />•	Up to 20% of the unspent budget will be rolled over to the next day<br />•	It must be set either at campaign or ad group level<br />•      Campaigns scheduled to run indefinitely must use a daily budget
      </td>

      <td>
        double
      </td>

      <td>
        Conditional. This field is required only if:<br />-It is not<br />set at ad group level. Cannot be changed to ad group level later.

        -budgetType is set to be daily
      </td>

      <td>
        The value of daily budget should at least be $0.01<br />**_Note:_**_&#x20;This field is required only if budgetType is set to be dailyBudget_
      </td>
    </tr>

    <tr>
      <td>
        totalBudget
      </td>

      <td>
        Total budget of campaign<br />\_ **Note**: it must be set either at campaign or ad group level\_
      </td>

      <td>
        double
      </td>

      <td>
        Conditional. This field is required only if:<br />-It is not<br />set at ad group level. Cannot be changed to ad group level later.

        -budgetType is set to be total
      </td>

      <td>
        The value of total budget should at least be $0.01<br />**_Note_**_: This field is required only if budgetType is set to be totalBudget_
      </td>
    </tr>

    <tr>
      <td>
        deliverySpeed
      </td>

      <td>
        Determines pacing of ad delivery<br />**_Note_**_: it must be set either at campaign or ad group level_
      </td>

      <td>

      </td>

      <td>
        Conditional. This field is required only if it is not set at ad group level. Cannot be changed to ad group level later.
      </td>

      <td>
        Values:<br />•	frontloaded<br />•	evenly<br />**_Note_**_: frontloaded pacing is not supported if budgetType is daily_
      </td>
    </tr>
  </tbody>
</Table>

###

<br />
