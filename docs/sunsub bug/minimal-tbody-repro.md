---
title: Minimal tbody repro
deprecated: false
hidden: false
metadata:
  robots: index
---
A) original-style (b in cells, colspan, link, no tbody):

<table>
<thead><tr><td><b>Field API Name</b></td><td><b>Type</b></td><td><b>Label and Description</b></td></tr></thead>
<tr><td>glia__Actor__c</td><td>string (80)</td><td>Actor - Possible values are Visitor, Operator, or Manager.</td></tr>
<tr><td>glia__AnswerText__c</td><td>string (255)</td><td>Answer (Text)</td></tr>
<tr><td colspan="3">Also includes <a href="#standard-salesforce-fields">Standard Salesforce Fields</a></td></tr>
</table>

<br />

B) only <b> in cells, no colspan/link, no tbody:

| <b>Field</b> | <b>Type</b> |
| ------------ | ----------- |

C) colspan row, no <b>/link, no tbody:

<table>
<thead><tr><td>Field</td><td>Type</td></tr></thead>
<tr><td>glia__Actor__c</td><td>string (80)</td></tr>
<tr><td colspan="2">Also includes more</td></tr>
</table>

<br />
