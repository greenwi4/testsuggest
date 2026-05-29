---
title: Table tbody repro
deprecated: false
hidden: false
metadata:
  robots: index
---
The Glia Data Bridge (GDB) application enables exporting engagement data from Glia to Salesforce. Depending on your settings, only the default data or additional datasets will be exported (see: <a href="https://docs.glia.com/glia-how-to/docs/gdb-in-salesforce#step-3-configure-engagement-data-import" target="configure-engagement-data-import">Configure Engagement Data Import</a>).


# Standard Salesforce Fields

Standard Salesforce fields are automatically included in all GDB custom objects. Depending on your Salesforce version and configuration, the standard fields may vary. The table below provides an example of the standard fields.

<table>
<thead><tr><td><b>Field API Name</b></td><td><b>Type</b></td><td><b>Label</b></td></tr></thead>
<tbody>
<tr><td>Id</td><td>Lookup()</td><td>Id</td></tr>
<tr><td>IsDeleted</td><td>Checkbox</td><td>IsDeleted</td></tr>
<tr><td>LastModifiedById</td><td>Lookup(User)</td><td>LastModifiedBy</td></tr>
<tr><td>LastModifiedDate</td><td>Date/Time</td><td>LastModifiedDate</td></tr>
<tr><td>LastReferencedDate</td><td>Date/Time</td><td>LastReferencedDate</td></tr>
<tr><td>LastViewedDate</td><td>Date/Time</td><td>LastViewedDate</td></tr>
<tr><td>Name</td><td>Auto Number</td><td>Name</td></tr>
<tr><td>OwnerId</td><td>Lookup(User,Group)</td><td>Owner</td></tr>
<tr><td>SystemModstamp</td><td>Date/Time</td><td>SystemModstamp</td></tr>
<tr><td>UserRecordAccessId</td><td>Lookup(User Record Access)</td><td>UserRecordAccess</td></tr>
</tbody>
</table>


# Default Data

The data in the tables below is pulled into Salesforce by default when you have set up data export using GDB (see: <a href="https://docs.glia.com/glia-how-to/docs/gdb-in-salesforce" target="gdb-in-salesforce">Using Glia Data Bridge to Export Data from Glia to Salesforce</a>).

### glia\_\_GDB_Engagement\_\_c

<table>
<thead><tr><td><b>Field API Name</b></td><td><b>Data Type</b></td><td><b>Label and Description</b></td></tr></thead>
<tr><td>glia__Audio_Used__c</td><td>boolean</td><td>Audio Used</td></tr>
<tr><td>glia__Chat_Transcript__c</td><td>string (255)</td><td>Chat Transcript</td></tr>
<tr><td>glia__Cobrowsing_Used__c</td><td>boolean</td><td>Cobrowsing Used</td></tr>
<tr><td>glia__Created_At__c</td><td>datetime</td><td>Created At</td></tr>
<tr><td>glia__CRM_Forwarded__c</td><td>boolean</td><td>CRM Forwarded - Shows whether an engagement was exported to CRM with GliaHub internal feature. Not related to data pulling process.</td></tr>
<tr><td>glia__Duration__c</td><td>double (18, 0)</td><td>Duration (seconds)</td></tr>
<tr><td>glia__End_Reason__c</td><td>string (100)</td><td>End Reason</td></tr>
<tr><td>glia__Ended_At__c</td><td>datetime</td><td>Ended At</td></tr>
<tr><td>glia__Engagement_Type__c</td><td>string (255)</td><td>Engagement Type</td></tr>
<tr><td>glia__EngagementPullingState__c</td><td>picklist (255), restricted</td><td>Engagement Pulling State - Shows the current state of an engagement during data pulling process. Internal use only.</td></tr>
<tr><td>glia__Enriched__c</td><td>boolean</td><td>Enriched - During the data pulling process, this value is false for a short period of time. If true, it means that Salesforce has pulled all engagement data. Internal use only.</td></tr>
<tr><td>glia__Flagged__c</td><td>boolean</td><td>Flagged - Indicates if the engagement was flagged by the agent for a technical issue.</td></tr>
<tr><td>glia__GDB_Visitor__c</td><td>Lookup (glia__GDB_Visitor__c)</td><td>GDB Visitor - Mapped by pulling process.</td></tr>
<tr><td>glia__Glia_ID_UUID__c</td><td>string (1300), formula</td><td>Glia ID (UUID) - Set automatically.</td></tr>
<tr><td>glia__Id__c</td><td>string (255), external id</td><td>Id</td></tr>
<tr><td>glia__IsNoMatchProcessExecuted__c</td><td>boolean</td><td>Is No Match Process Executed - Shows whether "No Match" event flows were executed after pulling the engagement. Internal use only.</td></tr>
<tr><td>glia__Manager_Survey_Configured__c</td><td>boolean</td><td>Manager Survey Configured</td></tr>
<tr><td>glia__Operator_Survey_Configured__c</td><td>boolean</td><td>Operator Survey Configured</td></tr>
<tr><td>glia__Platform__c</td><td>string (255)</td><td>Platform</td></tr>
<tr><td>glia__Queue_Wait_Time__c</td><td>double (18, 0)</td><td>Queue Wait Time</td></tr>
<tr><td>glia__RequiresNoMatchAutomation__c</td><td>boolean</td><td>Requires No Match Automation - Shows whether there are "No Match" event flows defined for a particular engagement to be executed. Internal use only.</td></tr>
<tr><td>glia__Source__c</td><td>string (255)</td><td>Source</td></tr>
<tr><td>glia__Video_Used__c</td><td>boolean</td><td>Video Used</td></tr>
<tr><td>glia__Visitor__c</td><td>string (255)</td><td>Visitor Link</td></tr>
<tr><td>glia__Visitor_Browser__c</td><td>string (100)</td><td>Visitor Browser</td></tr>
<tr><td>glia__Visitor_Device_Type__c</td><td>string (100)</td><td>Visitor Device Type</td></tr>
<tr><td>glia__Visitor_Id__c</td><td>string (255)</td><td>Visitor Id</td></tr>
<tr><td>glia__Visitor_Name__c</td><td>string (255)</td><td>Visitor Name</td></tr>
<tr><td>glia__Visitor_Survey_Configured__c</td><td>boolean</td><td>Visitor Survey Configured</td></tr>
<tr><td colspan="3">Also includes <a href="#standard-salesforce-fields">Standard Salesforce Fields</a></td></tr>
</table>

### glia\_\_GDB_Sub_Engagement\_\_c

<table>
<thead><tr><td><b>Field API Name</b></td><td><b>Type</b></td><td><b>Label and Description</b></td></tr></thead>
<tr><td>glia__Accepted_At__c</td><td>datetime</td><td>Accepted At</td></tr>
<tr><td>glia__Accepted_Media_Type__c</td><td>string (80)</td><td>Accepted Media Type</td></tr>
<tr><td>glia__Duration__c</td><td>double (14, 0)</td><td>Duration</td></tr>
<tr><td>glia__End_Reason__c</td><td>string (100)</td><td>End Reason</td></tr>
<tr><td>glia__Ended_At__c</td><td>datetime</td><td>Ended At</td></tr>
<tr><td>glia__Engagement__c</td><td>Master-detail (glia__GDB_Engagement__c)</td><td>Engagement - Mapped by pulling process.</td></tr>
<tr><td>glia__GBD_Operator_Link__c</td><td>string (1300), formula</td><td>GBD Operator - Set automatically.</td></tr>
<tr><td>glia__Highest_Operator_Media_Type__c</td><td>string (100)</td><td>Highest Operator Media Type</td></tr>
<tr><td>glia__Highest_Visitor_Media_Type__c</td><td>string (100)</td><td>Highest Visitor Media Type</td></tr>
<tr><td>glia__Id__c</td><td>string (80), external id</td><td>Id</td></tr>
<tr><td>glia__Offered_Media_Type__c</td><td>string (100)</td><td>Offered Media Type</td></tr>
<tr><td>glia__Operator__c</td><td>string (80)</td><td>Operator</td></tr>
<tr><td>glia__Parent_Engagement_UUID__c</td><td>string (255)</td><td>Parent Engagement UUID</td></tr>
<tr><td>glia__Request_Type__c</td><td>string (100)</td><td>Request Type - Engagement type can be reactive or proactive.</td></tr>
<tr><td>glia__Requested_At__c</td><td>datetime</td><td>Requested At</td></tr>
<tr><td>glia__Site__c</td><td>string (80)</td><td>Site</td></tr>
<tr><td>glia__Used_Cobrowsing__c</td><td>boolean</td><td>Used Cobrowsing</td></tr>
<tr><td colspan="3">Also includes <a href="#standard-salesforce-fields">Standard Salesforce Fields</a></td></tr>
</table>

### glia\_\_GDB_Operator\_\_c

<table>
<thead><tr><td><b>Field API Name</b></td><td><b>Type</b></td><td><b>Label and Description</b></td></tr></thead>
<tr><td>glia__Audio_Source__c</td><td>string (100)</td><td>Audio Source</td></tr>
<tr><td>glia__Email__c</td><td>email (80)</td><td>Email</td></tr>
<tr><td>glia__Enabled__c</td><td>boolean</td><td>Enabled</td></tr>
<tr><td>glia__Enriched__c</td><td>boolean</td><td>Enriched - During the data pulling process, this value is false for a short period of time. If true, it means that Salesforce has pulled all operator data, such as name, email, role, etc. Internal use only.</td></tr>
<tr><td>glia__External__c</td><td>boolean</td><td>External</td></tr>
<tr><td>glia__Glia_ID_UUID__c</td><td>string (1300), formula</td><td>Glia ID (UUID) - Set automatically.</td></tr>
<tr><td>glia__href__c</td><td>string (255), external id</td><td>href</td></tr>
<tr><td>glia__Id__c</td><td>string (100), external id</td><td>Id</td></tr>
<tr><td>glia__Industry__c</td><td>double (2, 0)</td><td>Industry</td></tr>
<tr><td>glia__Locale__c</td><td>string (50)</td><td>Locale</td></tr>
<tr><td>glia__Max_Engagement_Count__c</td><td>double (18, 0)</td><td>Max Engagement Count</td></tr>
<tr><td>glia__Name__c</td><td>string (255)</td><td>Name</td></tr>
<tr><td>glia__Observation_Enabled__c</td><td>boolean</td><td>Observation Enabled</td></tr>
<tr><td>glia__Phone__c</td><td>string (255)</td><td>Phone</td></tr>
<tr><td>glia__Phone_Extension__c</td><td>string (255)</td><td>Phone Extension</td></tr>
<tr><td>glia__Phone_Number_Verified__c</td><td>boolean</td><td>Phone Number Verified</td></tr>
<tr><td>glia__Proactive_Enabled__c</td><td>boolean</td><td>Proactive Enabled</td></tr>
<tr><td>glia__Reactive_Enabled__c</td><td>boolean</td><td>Reactive Enabled</td></tr>
<tr><td>glia__Role__c</td><td>string (255)</td><td>Role</td></tr>
<tr><td>glia__SIP_Domain_extension__c</td><td>string (100)</td><td>SIP Domain extension</td></tr>
<tr><td>glia__SIP_Domain_Id__c</td><td>string (100)</td><td>SIP Domain Id</td></tr>
<tr><td colspan="3">Also includes <a href="#standard-salesforce-fields">Standard Salesforce Fields</a></td></tr>
</table>

### glia\_\_GDB_Operator_Engagement\_\_c

<table>
<thead><tr><td><b>Field API Name</b></td><td><b>Type</b></td><td><b>Label and Description</b></td></tr></thead>
<tr><td>glia__Engagement__c</td><td>Master-detail (glia__GDB_Engagement__c)</td><td>Engagement - Mapped by pulling process.</td></tr>
<tr><td>glia__Engagement_UUID__c</td><td>string (255)</td><td>Engagement UUID</td></tr>
<tr><td>glia__Id__c</td><td>string (255), external id</td><td>Id - Internal use only.</td></tr>
<tr><td>glia__Operator__c</td><td>Master-detail (glia__GDB_Operator__c)</td><td>Operator - Mapped by pulling process.</td></tr>
<tr><td>glia__Operator_Email__c</td><td>string (1300), formula</td><td>Operator Email - Set automatically.</td></tr>
<tr><td>glia__Operator_Name__c</td><td>string (1300), formula</td><td>Operator Name - Set automatically.</td></tr>
<tr><td>glia__Operator_UUID__c</td><td>string (255)</td><td>Operator UUID</td></tr>
<tr><td colspan="3">Also includes <a href="#standard-salesforce-fields">Standard Salesforce Fields</a></td></tr>
</table>

### glia\_\_GDB_Visitor\_\_c

<table>
<thead><tr><td><b>Field API Name</b></td><td><b>Type</b></td><td><b>Label and Description</b></td></tr></thead>
<tr><td>glia__Banned__c</td><td>boolean</td><td>Banned</td></tr>
<tr><td>glia__Email__c</td><td>email (80)</td><td>Email</td></tr>
<tr><td>glia__Enriched__c</td><td>boolean</td><td>Enriched - During the data pulling process, this value is false for a short period of time. If true, it means that Salesforce has pulled all visitor data, such as name, phone, email, attributes, etc. Internal use only.</td></tr>
<tr><td>glia__Generated_Name__c</td><td>string (255)</td><td>Generated Name</td></tr>
<tr><td>glia__Glia_ID_UUID__c</td><td>string (1300), formula</td><td>Glia ID (UUID) - Set automatically.</td></tr>
<tr><td>glia__Id__c</td><td>string (255), external id</td><td>Id</td></tr>
<tr><td>glia__Name__c</td><td>string (255)</td><td>Name</td></tr>
<tr><td>glia__Note__c</td><td>string (255)</td><td>Note - Stores notes about the visitor, but if it is longer than 255 characters, the remaining text will be truncated. To store the full text, use glia__NoteFull__c. Will be deprecated soon.</td></tr>
<tr><td>glia__NoteFull__c</td><td>textarea (32768)</td><td>Note</td></tr>
<tr><td>glia__Phone__c</td><td>string (255)</td><td>Phone</td></tr>
<tr><td>glia__URL__c</td><td>url (255)</td><td>URL</td></tr>
<tr><td colspan="3">Also includes <a href="#standard-salesforce-fields">Standard Salesforce Fields</a></td></tr>
</table>


# Audio Recording Data

The data in the table below is pulled to Salesforce if the **Synchronize Engagement Audio Recordings** setting is enabled under **Glia Data Bridge > Configuration > Engagement Settings > Feature Settings**.

### glia\_\_GDB_Audio_Recording\_\_c

<table>
<thead><tr><td><b>Field API Name</b></td><td><b>Type</b></td><td><b>Label and Description</b></td></tr></thead>
<tr><td>glia__Engagement__c</td><td>Master-detail (glia__GDB_Engagement__c)</td><td>Engagement - Mapped by pulling process.</td></tr>
<tr><td>glia__Engagement_UUID__c</td><td>string (255)</td><td>Engagement UUID</td></tr>
<tr><td>glia__Glia_ID_UUID__c</td><td>string (1300), formula</td><td>Glia ID (UUID) - Set automatically.</td></tr>
<tr><td>glia__ID__c</td><td>string (255), external id</td><td>ID</td></tr>
<tr><td>glia__Listen_Download__c</td><td>string (1300), formula</td><td>Listen/Download - Set automatically.</td></tr>
<tr><td>glia__URL__c</td><td>url (255)</td><td>URL</td></tr>
<tr><td>glia__View_Download__c</td><td>string (1300), formula</td><td>View/Download - Set automatically.</td></tr>
<tr><td colspan="3">Also includes <a href="#standard-salesforce-fields">Standard Salesforce Fields</a></td></tr>
</table>


# Visitor Data

The data in the table below is pulled to Salesforce if the **Synchronize Visitor Information** setting is enabled under **Glia Data Bridge > Configuration > Engagement Settings > Feature Settings**.

### glia\_\_GDB_Visitor_Custom_Attribute\_\_c

<table>
<thead><tr><td><b>Field API Name</b></td><td><b>Type</b></td><td><b>Label and Description</b></td></tr></thead>
<tr><td>glia__GDB_Visitor__c</td><td>Master-detail (glia__GDB_Visitor__c)</td><td>GDB Visitor - Mapped by pulling process.</td></tr>
<tr><td>glia__Key__c</td><td>Text(100)</td><td>Key</td></tr>
<tr><td>glia__Value__c</td><td>Text(100)</td><td>Value</td></tr>
<tr><td colspan="3">Also includes <a href="#standard-salesforce-fields">Standard Salesforce Fields</a></td></tr>
</table>


# Chat Transcript Data

The data in the tables below is pulled to Salesforce if the **Synchronize Chat Transcripts** setting is enabled under **Glia Data Bridge > Configuration > Engagement Settings > Feature Settings**.

### glia\_\_GDB_Chat_Message\_\_c

<table>
<thead><tr><td><b>Field API Name</b></td><td><b>Type</b></td><td><b>Label and Description</b></td></tr></thead>
<tr><td>glia__Chat_Transcript__c</td><td>Master-detail (glia__GDB_Chat_Transcript__c)</td><td>Chat Transcript - Mapped by pulling process.</td></tr>
<tr><td>glia__Created_At__c</td><td>datetime</td><td>Created At</td></tr>
<tr><td>glia__Delivered_At__c</td><td>datetime</td><td>Delivered At</td></tr>
<tr><td>glia__Glia_ID_UUID__c</td><td>string (1300), formula</td><td>Glia ID (UUID) - Set automatically.</td></tr>
<tr><td>glia__Id__c</td><td>string (80), external id</td><td>Id</td></tr>
<tr><td>glia__Message__c</td><td>string (255)</td><td>Message</td></tr>
<tr><td>glia__Speech_to_Text__c</td><td>boolean</td><td>Speech to Text</td></tr>
<tr><td>glia__Target__c</td><td>string (255)</td><td>Target</td></tr>
<tr><td>glia__Type__c</td><td>string (80)</td><td>Type</td></tr>
<tr><td>glia__Attachment_Data__c</td><td>textarea (32768)</td><td>Attachment Data - JSON of attachment data associated with the chat message.</td></tr>
<tr><td colspan="3">Also includes <a href="#standard-salesforce-fields">Standard Salesforce Fields</a></td></tr>
</table>

### glia\_\_GDB_Chat_Transcript\_\_c

<table>
<thead><tr><td><b>Field API Name</b></td><td><b>Type</b></td><td><b>Label and Description</b></td></tr></thead>
<tr><td>glia__Engagement__c</td><td>Master-detail (glia__GDB_Engagement__c)</td><td>Engagement - Mapped by pulling process.</td></tr>
<tr><td>glia__Engagement_UUID__c</td><td>string (255)</td><td>Engagement UUID</td></tr>
<tr><td>glia__enriched__c</td><td>boolean</td><td>enriched - During the data pulling process, this value is false for a short period of time. If true, it means that Salesforce has pulled all operator data, such as name, email, role, etc. Internal use only.</td></tr>
<tr><td>glia__Glia_ID_UUID__c</td><td>string (1300), formula</td><td>Glia ID (UUID) - Set automatically.</td></tr>
<tr><td>glia__href__c</td><td>url (255)</td><td>href</td></tr>
<tr><td>glia__Id__c</td><td>string (255), external id</td><td>Id</td></tr>
<tr><td>glia__Number_of_Messages__c</td><td>double (18, 0), formula</td><td>Number of Messages - Set automatically.</td></tr>
<tr><td colspan="3">Also includes <a href="#standard-salesforce-fields">Standard Salesforce Fields</a></td></tr>
</table>


# Survey Data

The data in the table below is pulled to Salesforce if the **Synchronize Survey Answers** setting is enabled under **Glia Data Bridge > Configuration > Engagement Settings > Feature Settings**.

### glia\_\_GDB_Survey_Answer\_\_c

<table>
<thead><tr><td><b>Field API Name</b></td><td><b>Type</b></td><td><b>Label and Description</b></td></tr></thead>
<tr><td>glia__Actor__c</td><td>string (80)</td><td>Actor - Possible values are Visitor, Operator, or Manager. The value Manager indicates that the answers were generated by AI.</td></tr>
<tr><td>glia__AnswerText__c</td><td>string (255)</td><td>Answer (Text)</td></tr>
<tr><td>glia__Engagement__c</td><td>Master-detail (glia__GDB_Engagement__c)</td><td>Engagement - Mapped by pulling process.</td></tr>
<tr><td>glia__Glia_ID_UUID__c</td><td>string (1300), formula</td><td>Glia ID (UUID) - Set automatically.</td></tr>
<tr><td>glia__Id__c</td><td>string (255), external id</td><td>Id</td></tr>
<tr><td>glia__Position__c</td><td>double (3, 0)</td><td>Position</td></tr>
<tr><td>glia__Question_Id__c</td><td>string (255)</td><td>Question Id</td></tr>
<tr><td>glia__Question_ID_Link__c</td><td>string (1300), formula</td><td>Question ID - Set automatically.</td></tr>
<tr><td>glia__Title__c</td><td>string (255)</td><td>Title</td></tr>
<tr><td>glia__Type__c</td><td>string (100)</td><td>Type</td></tr>
<tr><td colspan="3">Also includes <a href="#standard-salesforce-fields">Standard Salesforce Fields</a></td></tr>
</table>


# Related Articles

- <a href="https://docs.glia.com/glia-how-to/docs/gdb-in-salesforce" target="gdb-in-salesforce">Using Glia Data Bridge to Export Data from Glia to Salesforce</a>