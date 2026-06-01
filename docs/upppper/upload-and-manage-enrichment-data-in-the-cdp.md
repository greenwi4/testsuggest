---
title: Upload and Manage Enrichment Data in the CDP
deprecated: false
hidden: false
metadata:
  robots: index
---

The Contextual Data Platform (CDP) is PagerDuty's data storage layer that holds enrichment data used to add context to your events. CDP organizes contextual data into data tables that can be referenced in Event Enrichment rules to automatically inject information like team ownership, runbook links, CMDB details, and more into your alerts.

The CDP consists of: 

**A. Enrichment Schema** - Defines the structure of a data table, including:

- **Column names and types**
- **Query fields** - Columns used to look up rows (match against incoming events)
- **Enriched fields** - Columns that provide contextual data added to matched events

**B. Enrichment Data** - The actual rows in a data table. Each row contains values for the columns defined by the schema. You populate this data by uploading CSV files or through integrations like ServiceNow.

# Upload Data to the Enrichment Service

PagerDuty allows you to upload contextual data via CSV files to enrich your PagerDuty events. This guide covers three common workflows:

- **[Create an Enrichment Schema from a CSV](#create-an-enrichment-schema-from-a-csv)** - Automatically generate a schema and upload data in one step.
- **[Create a Schema Without Data](#create-a-schema-without-data)** - Define your schema structure first, add data later.
- **[Add Data to an Existing Schema](#add-data-to-an-existing-schema)** - Upload additional CSV data to an existing schema.

> 🚧 Prerequisites
> 
> **API Endpoint**: <https://api.pagerduty.com> (or your regional PagerDuty API endpoint)  
> **Authentication**: Include your API token in the Authorization header (see examples [below](#Example:-create-schema-and-upload-initial-data))  
> **CSV File Format**: First row must contain column headers matching your schema fields

# Create an Enrichment Schema from a CSV

When you upload a CSV file, the Enrichment feature automatically generates a schema based on the CSV structure. The API will:

1. Automatically create a schema with the first column as the QUERY field and **all remaining columns** as ENRICHED fields.
2. Derive the schema name from the filename.
3. Set the description to `Auto generated schema from CSV upload`.
4. Accept the CSV file for asynchronous processing.
5. Return immediately with a `202 Accepted` response.

## Example: Create Schema and Upload Initial Data

```json
curl -X POST "https://api.pagerduty.com/enrichment/schemas" \
  -H "Authorization: Token token=YOUR_API_TOKEN" \
  -H "Content-Type: multipart/form-data" \
  -F "file=@team_data.csv"
```

The schema is automatically generated from your CSV headers.

## CSV File Format Example

Your `team_data.csv` must have column headers in the first row. 

```Application,Manager,Team,Runbook Text
Authorization,alice@example.com,Auth Team,https://wiki.example.com/auth
Payment API,bob@example.com,Payments Team,https://wiki.example.com/payments
User Service,carol@example.com,User Platform,https://wiki.example.com/users
```

In this example:

- **Application** (first column) becomes a QUERY field used to match against incoming events.
- **Manager, Team, Runbook URL** (remaining columns) become ENRICHED fields and are added to matched events.

### Response

```json
{
  "schema": {
    "id": "9f194d8d-0f58-4c5c-b1d2-a5adf7171821",
    "type": "enrichment_schema",
    "integration_type": "CSV",
    "name": "team_data",
    "description": "Auto generated schema from CSV upload",
    "fields": [
      {"name": "Application", "type": "query"},
      {"name": "Manager", "type": "enriched"},
      {"name": "Team", "type": "enriched"},
      {"name": "Runbook URL", "type": "enriched"}
    ],
    "created_at": "2026-02-23T15:17:30Z",
    "updated_at": "2026-02-23T15:17:30Z"
  }
}

```

## How Schema Auto-Generation Works

The automatic schema generation follows these conventions:

- **Schema name**: Derived from the uploaded filename without the .csv extension.
- **Schema description**: Set to `Auto generated schema from CSV upload`.
- **First column**: Becomes the QUERY field used to look up enrichment data.
- **All other columns**: Become ENRICHED fields and is the data added to events.

## Updating Schema Name and Description

After creation, you can update the schema name and description:

```json
curl -X PUT "https://api.pagerduty.com/enrichment/schemas/9f194d8d-0f58-4c5c-b1d2-a5adf7171821" \
  -H "Authorization: Token token=YOUR_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
        "schema": {
        "name": "Application Runbooks",
        "description": "Maps applications to team leads and runbook information"
    }
  }'
```

# Create a Schema Without Data

If you need more control over your schema definition, such as multiple query fields, you can create a schema using JSON without uploading data. This is useful when you need to define your schema structure first and add data later.

## Example: Create Schema with JSON

```json
curl -X POST "https://api.pagerduty.com/enrichment/schemas" \
  -H "Authorization: Token token=YOUR_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Application Environment Enrichment",
    "description": "Enriches events with team and runbook information based on application and environment",
    "integration_type": "CSV",
    "fields": [
      {"name": "Application", "type": "query"},
      {"name": "Environment", "type": "query"},
      {"name": "Manager", "type": "enriched"},
      {"name": "Team", "type": "enriched"},
      {"name": "Runbook URL", "type": "enriched"}
    ]
  }'
```

### Response

```json
{
  "schema": {
    "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "type": "enrichment_schema",
    "integration_type": "CSV",
    "name": "Application Environment Enrichment",
    "description": "Enriches events with team and runbook information based on application and environment",
    "fields": [
      {"name": "Application", "type": "query"},
      {"name": "Environment", "type": "query"},
      {"name": "Manager", "type": "enriched"},
      {"name": "Team", "type": "enriched"},
      {"name": "Runbook URL", "type": "enriched"}
    ],
    "created_at": "2026-02-23T15:17:30Z",
    "updated_at": "2026-02-23T15:17:30Z"
  }
}
```

## Benefits of JSON Schema Creation

- **Multiple query fields**: Define multiple fields for matching (e.g., Application + Environment).
- **Custom field order**: Control the exact order of fields.
- **Explicit naming:** Choose meaningful schema names upfront.
- **Field type control:** Explicitly define which fields are QUERY vs ENRICHED fields.

## Field Types

- **`query`**: Fields used to look up enrichment data. You can have 1-3 `query` fields. 
- **`enriched`**: Remaining fields that will be added to matched events. 

> 📘 Note
> 
> After creating the schema, you can upload CSV data using the [Add Data to an Existing Schema method](#add-data-to-an-existing-schema).

# Add Data to an Existing Schema

Once you have created a schema, you can upload additional CSV files to add or update ENRICHMENT data.

## Example: Upload CSV to Existing Schema

```json
curl -X POST "https://api.pagerduty.com/enrichment/schemas/a1b2c3d4-e5f6-7890-abcd-ef1234567890/records" \
  -H "Authorization: Token token=YOUR_API_TOKEN" \
  -H "Content-Type: multipart/form-data" \
  -F "file=@enrichment_data.csv"
```

## CSV File Format for Upload

Your CSV must include all fields defined in the schema (both query and enriched fields):

```
Application,Environment,Manager,Team,Runbook URL
Authorization,production,alice@example.com,Auth Team,https://wiki.example.com/auth
Authorization,staging,alice@example.com,Auth Team,https://wiki.example.com/auth-staging
Payment API,production,bob@example.com,Payments Team,https://wiki.example.com/payments
User Service,production,carol@example.com,User Platform,https://wiki.example.com/users
```

### Response

```json
{
  "upload_id": "605d87a2-c67c-441e-a4cb-dbbbd94a340c",
  "schema_id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "filename": "enrichment_data.csv",
  "size_bytes": 2048,
  "status": "accepted",
  "accepted_at": "2026-02-23T16:30:00Z"
}
```

> 🚧 Important Notes
> 
> - The CSV file must contain columns matching the fields defined in your schema.
> - Missing columns will result in empty values for those fields.
> - Extra columns in the CSV that don't match schema fields will be ignored.
> - Records are identified by the **combination of query field values**(case-insensitive).
> - Uploading the same query field combination again will **update** the existing record (not create a duplicate).

# Verify Your Data

## List All Records in a Schema

You can list all records in a schema to verify your data was uploaded correctly. 

```json
curl -X GET "https://api.pagerduty.com/enrichment/schemas/a1b2c3d4-e5f6-7890-abcd-ef1234567890/records" \
  -H "Authorization: Token token=YOUR_API_TOKEN"
```

### Response

```json
{
  "schema_id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "records": [
    {
      "record_id": "a3b2c1d4e5f6",
      "type": "enrichment_record",
      "created_at": "2026-02-23T15:17:30Z",
      "enrichment_data": {
        "Application": "Authorization",
        "Environment": "production",
        "Manager": "alice@example.com",
        "Team": "Auth Team",
        "Runbook URL": "https://wiki.example.com/auth"
      }
    },
    {
      "record_id": "b4c3d2e1f678",
      "type": "enrichment_record",
      "created_at": "2026-02-23T15:17:30Z",
      "enrichment_data": {
        "Application": "Payment API",
        "Environment": "production",
        "Manager": "bob@example.com",
        "Team": "Payments Team",
        "Runbook URL": "https://wiki.example.com/payments"
      }
    }
  ],
  "next_cursor": null
}
```

The `next_cursor` field contains a pagination token if there are more records. Pass it as a `?cursor=` query parameter to fetch the next page.

## Query a Specific Record

You can also query for a specific record by providing values for all query fields. 

```json
curl -X POST "https://api.pagerduty.com/enrichment/query" \
  -H "Authorization: Token token=YOUR_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "schema_id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "query": [
      {"field": "Application", "value": "Authorization"},
      {"field": "Environment", "value": "production"}
    ]
  }'
```

> 📘 Note
> 
> When querying, you must provide values for **all query fields** defined in your schema.

### Response

```json
{
  "records": [
    {
      "record_id": "a3b2c1d4e5f6",
      "type": "enrichment_record",
      "created_at": "2026-02-23T15:17:30Z",
      "enrichment_data": {
        "Application": "Authorization",
        "Environment": "production",
        "Manager": "alice@example.com",
        "Team": "Auth Team",
        "Runbook URL": "https://wiki.example.com/auth"
      }
    }
  ]
}
```

# Delete a Record

You can permanently delete a single enrichment record by its record ID. This is a hard delete — the record cannot be recovered.

```json
curl -X DELETE "https://api.pagerduty.com/enrichment/schemas/a1b2c3d4-e5f6-7890-abcd-ef1234567890/records/a3b2c1d4e5f6" \
  -H "Authorization: Token token=YOUR_API_TOKEN"
```

# Delete a Schema

You can delete an enrichment schema when it is no longer needed. Only CSV type schemas can be deleted through the API.

```json
curl -X DELETE "https://api.pagerduty.com/enrichment/schemas/a1b2c3d4-e5f6-7890-abcd-ef1234567890" \
  -H "Authorization: Token token=YOUR_API_TOKEN"
```

# ServiceNow CMDB Integration

PagerDuty also provides a first class integration with ServiceNow that provides a managed data source for Enrichment that automatically creates schemas and synchronizes data to them from ServiceNow CMDB tables.  
When using the ServiceNow integration the Enrichment Schemas and data tables used for Event Enrichment are automatically managed for you.

See the [ServiceNow CMDB Integration Guide](doc:servicenow-cmdb-integration-setup-guide) for complete setup instructions.

# Troubleshooting

[block:html]
{
  "html": "<button type=\"button\" id=\"mainLabel\" class=\"expandCollapseAll\" onclick=\"toggleExpand()\">\nExpand/Collapse All\n</button>"
}
[/block]


## 400 Bad Request - When creating schema from CSV

<details class="kb-faq">
  <summary></summary>

- Check that your CSV file size doesn't exceed 10MB (maximum allowed).
- Verify the file has a `.csv` extension.
- Ensure the CSV has at least 2 columns (one query field, one enriched field).
- Check that the Content-Type is set to multipart/form-data or text/csv.
- Check that the CSV filename is unique. Auto-generated schemas derive their name from the uploaded filename and schema names must be unique.

</details>

## 400 Bad Request - When creating schema with JSON

<details class="kb-faq">
  <summary></summary>

- Ensure you have at least one query field and one enriched field. 
- Verify field names are unique within the schema.
- Check that field types are either `query` or `enriched`.
- Ensure schema name is 50 characters or less. 
- Ensure description is 2048 characters or less. 

</details> 

## 400 Bad Request - When adding data to a schema

<details class="kb-faq">
  <summary></summary>

- Check that your CSV file is properly formatted with valid syntax. 
- Verify the file is not corrupted. 
- Ensure CSV headers don't contain special characters that could cause parsing issues. 

</details>

## 404 Not Found - When adding data to a schema

<details class="kb-faq">
  <summary></summary>

- Verify the schema ID exists and hasn't been deleted.
- Check that you're using the correct endpoint URL.
- Ensure you have access to the schema in your account.

</details>

## Additional Resources

<details class="kb-faq">
<summary></summary>

- To list all your schemas:  
  `GET https://api.pagerduty.com/enrichment/schemas`
- To view schema details:  
  `GET https://api.pagerduty.com/enrichment/schemas/{schemaId}`
- To list records in a schema:  
  `GET https://api.pagerduty.com/enrichment/schemas/{schema_id}/records`
- To delete a schema:  
  `DELETE https://api.pagerduty.com/enrichment/schemas/{schema_id}`

</details>