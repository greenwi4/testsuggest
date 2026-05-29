---
title: tbody bug repro (array pattern)
deprecated: false
hidden: false
metadata:
  robots: index
---
## BROKEN: no tbody (rows direct under table) + colspan + b + link

<table>
<thead><tr><td><b>Field API Name</b></td><td><b>Type</b></td><td><b>Label and Description</b></td></tr></thead>
<tr><td>glia__Actor__c</td><td>string (80)</td><td>Actor - Possible values are Visitor, Operator, or Manager.</td></tr>
<tr><td>glia__AnswerText__c</td><td>string (255)</td><td>Answer (Text)</td></tr>
<tr><td colspan="3">Also includes <a href="#standard-salesforce-fields">Standard Salesforce Fields</a></td></tr>
</table>

## CONTROL: same rows wrapped in tbody

<table>
<thead><tr><td><b>Field API Name</b></td><td><b>Type</b></td><td><b>Label and Description</b></td></tr></thead>
<tbody>
<tr><td>glia__Actor__c</td><td>string (80)</td><td>Actor - Possible values are Visitor, Operator, or Manager.</td></tr>
<tr><td>glia__AnswerText__c</td><td>string (255)</td><td>Answer (Text)</td></tr>
<tr><td colspan="3">Also includes <a href="#standard-salesforce-fields">Standard Salesforce Fields</a></td></tr>
</tbody>
</table>

<br />
