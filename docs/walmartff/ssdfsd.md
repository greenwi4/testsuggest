---
title: ssdfsd
deprecated: false
hidden: false
metadata:
  robots: index
---

> 📘 URL: ​POST /api/v1/campaigns

**_Note:_**

- _This API supports batch operations with a max batch size of 10. For bulk operation, the advertiser Id must be the same across all requests in the payload._
- _You must set all of&#x20;_`budgetType`_,&#x20;_`dailyBudget`_,&#x20;_`totalBudget`_,&#x20;_`startDate`_,&#x20;_`endDate`_, and&#x20;_`deliverySpeed`_&#x20;parameters at same level i.e. either at campaign level or ad group level_

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
        The name of the campaign<br />***Note:*** Limit on length of campaign name is 240 characters
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
        Campaign description<br />***Note:*** Limit on length of campaign description is 240 characters
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
        Values:<br />awareness (default value)<br />engagement<br />conversion<br />***Note:*** For video campaigns, the only supported objective is `awareness`
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
        The date to start campaign<br />***Note:*** it must be set either at campaign or ad group level
      </td>

      <td>
        date
      </td>

      <td>
        Conditional.This field is required only if it is not set at ad group level. Cannot be changed to ad group level later.
      </td>

      <td>
        Date should be in format:   yyyy-MM-dd'T'HH:mm:ss.SSSXXX

        ***Note:*** <ul><li>All timestamp values must be in ISO 8601 format (e.g., "2025-07-20T19:10:10-05:00").</li><li>All date-time values are internally converted to Eastern Time (ET) for processing and normalized to the start of the hour. This means minutes and seconds are truncated. Example: "2025-07-20T19:10:10-05:00" becomes "2025-07-20T19:00:00-05:00" in ET</li></ul><br />Kindly take these behaviors into consideration when assigning a value to startDate in your request.
      </td>
    </tr>

    <tr>
      <td>
        endDate
      </td>

      <td>
        The date when campaign ends<br />***Note:*** it must be set either at campaign or ad group level
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

        ***Note:***<ul><li>All timestamp values must be in ISO 8601 format (e.g., "2025-07-20T19:10:10-05:00").</li><li>All date-time values are internally converted to Eastern Time (ET) for processing and normalized to the start of the hour. This means minutes and seconds are truncated. Example: "2025-07-20T19:10:10-05:00" becomes "2025-07-20T19:00:00-05:00" in ET</li><li>The endDate must be set to a time after 12:00 PM ET. If the provided value is before 12:00 PM ET, the system will return an error.</li><li>Special Case: If you set endDate to exactly "00:00:00" ET (e.g., "2025-07-20T00:00:00-05:00"), it will be interpreted as the end of the previous day: "2025-07-19T23:59:59-05:00".</li></ul><br />Kindly take these behaviors into consideration when assigning a value to startDate in your request.
      </td>
    </tr>

    <tr>
      <td>
        budgetType
      </td>

      <td>
        The type of budget allocation you want to choose for your campaign

        ***Note:*** it must be set either at campaign or ad group level<br />Campaigns scheduled to run indefinitely must use a daily budget
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
        The value of daily budget should at least be $0.01<br />***Note:*** This field is required only if budgetType is set to be dailyBudget
      </td>
    </tr>

    <tr>
      <td>
        totalBudget
      </td>

      <td>
        Total budget of campaign<br />***Note:*** it must be set either at campaign or ad group level
      </td>

      <td>
        double
      </td>

      <td>
        Conditional. This field is required only if:<br />-It is not<br />set at ad group level. Cannot be changed to ad group level later.

        -budgetType is set to be total
      </td>

      <td>
        The value of total budget should at least be $0.01<br />***Note:*** This field is required only if budgetType is set to be totalBudget
      </td>
    </tr>

    <tr>
      <td>
        deliverySpeed
      </td>

      <td>
        Determines pacing of ad delivery<br />***Note:*** it must be set either at campaign or ad group level
      </td>

      <td>

      </td>

      <td>
        Conditional. This field is required only if it is not set at ad group level. Cannot be changed to ad group level later.
      </td>

      <td>
        Values:<br />•	frontloaded<br />•	evenly<br />***Note:*** frontloaded pacing is not supported if budgetType is daily
      </td>
    </tr>
  </tbody>
</Table>

### **_Note:_**

- You must set all of budgetType, dailyBudget, totalBudget, startDate, endDate, and deliverySpeed parameters at same level i.e. either at campaign level or ad group level, not both
- If startDate, endDate, budgetType, dailyBudget, totalBudget, deliverySpeed are omitted, they must be defined at the ad group level
- You can only set either dailyBudget or totalBudget
- To set daily budget, you must choose value of budgetType as “daily” and then define dailyBudget.
- To set total budget, you must choose value of budgetType as “total” and then define totalBudget.
- When mediaType is set to VIDEO, the allowed objective field is AWARENESS. If nothing is passed the default value will be set to AWARENESS.
- During the campaign auto-setup flow, line items will be created asynchronously. The process may take up to 2 minutes to complete.
- Only BANNER mediaType is allowed in campaign auto setup

<Headers />

## Sample Request

```curl
curl -X POST \
 'https://developer.api.us.stg.walmart.com/api-proxy/service/display/api/v1/api/v1/campaigns' \ 

--header 'Content-Type:  application/json'  \ 
--header 'Authorization: Bearer <auth_token>'
--header 'WM_SEC.AUTH_SIGNATURE: **************'  \ 
--header 'WM_SEC.KEY_VERSION: 1'  \ 
--header 'WM_CONSUMER.ID: adfwe-v23-faasd2r-afs-asdfqeff'  \ 
--header 'WM_CONSUMER.intimestamp: 1565309779'

--data 
            '[ 
               {
                "advertiserId": 1,
                "name": "string",
                "description":  "string",
                "objective":  "string",
                "campaignType": "ngd", 
                "startDate": "string",
                "endDate": "string",
                "budgetType": "daily",    
                "dailyBudget": 1.0,                    
                "deliverySpeed": "evenly"  
              }
           ]'

```

## Sample Request (Batch Operation)

```curl
curl -X POST \
 'https://developer.api.us.stg.walmart.com/api-proxy/service/display/api/v1/api/v1/campaigns' \ 

--header 'Content-Type:  application/json'  \ 
--header 'Authorization: Bearer <auth_token>'
--header 'WM_SEC.AUTH_SIGNATURE: **************'  \ 
--header 'WM_SEC.KEY_VERSION: 1'  \ 
--header 'WM_CONSUMER.ID: adfwe-v23-faasd2r-afs-asdfqeff'  \ 
--header 'WM_CONSUMER.intimestamp: 1565309779'

--data ' [ 
             {
               "advertiserId": 1,
               "name": "string",
               "description":  "string",
               "objective": "string",
               "campaignType": "ngd",
               "startDate": "string",
               "endDate": "string",
               "budgetType": "string",       
               "totalBudget": 10.0,     
               "deliverySpeed": "evenly"  
             },
              {
                "advertiserId": 1,
                "name": "string",
                "description": "string",
                "objective": "string",     
                "campaignType": "ngd", 
                "startDate": "string",
                "endDate":  "string",
                "budgetType": "string",               
                "totalBudget": 10.0,             
                "deliverySpeed": "frontloaded"  
         }
]'
```

## Sample Request: Create campaign with `mediaType` as `VIDEO`

```curl
curl -X POST \ 'https://developer.api.us.walmart.com/api-proxy/service/display/api/v1/api/v1/campaigns' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <auth_token>' \
--header 'WM_SEC.AUTH_SIGNATURE: ***********' \
--header 'WM_CONSUMER.ID: abcde-v123-fa2r-a1fs-asd45f6qef' \
--header 'WM_SEC.KEY_VERSION: 1' \
--header 'WM_CONSUMER.intimestamp: 1565309779' \
--data '[{     "advertiserId": 1,
    "name": "string",
    "description": "string",
    "objective": "AWARENESS",
    "campaignType": "NGD",
    "startDate": "2025-01-01T12:00:00.000Z",
    "endDate": "2025-01-31T12:00:00.000Z",
    "budgetType": "TOTAL",
    "totalBudget": 10000.0,
    "deliverySpeed": "EVENLY",
    "mediaType": "VIDEO"
  }
]'
```

<br />

# Response

| Element    | Description                                                                                                                                                                                                        | Type    |
| :--------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------ |
| code       | The response code can have following values:<ul><li>success</li><li>failure</li></ul><br />Click [here](/advertising-partners/docs/api-status-codes-and-errors) for more information about Status Codes and Errors | string  |
| details    | Details will populate success or error message depending upon value of code                                                                                                                                        | string  |
| campaignId | ID of the campaign. This will be returned only when code=success                                                                                                                                                   | integer |
| name       | Name of the campaign                                                                                                                                                                                               | string  |

## Sample Response

```json json
[ 
  {
    "code": "success",
    "details": ["string"],
    "name": "string1",
    "campaignId": 1
   }

]

```

## Sample Response (Batch Operation)

```json json
[ 
  {
    "code": "success",
    "details": ["string"],
    "name": "string1",
    "campaignId": 1
   },
   
  {
    "code": "failure",
    "details": ["stringA", "stringB"],
    "name": "string1"
   }

]

```

<br />
