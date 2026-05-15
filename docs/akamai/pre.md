---
title: pre
deprecated: false
hidden: false
metadata:
  robots: index
---
<table>
  <thead>
    <th>Argument</th>
    <th>Required</th>
    <th>Description</th>
  </thead>
  <tbody>
    <tr>
      <td><code>config_id</code></td>
      <td class="rqcent">&#10004;</td>
      <td>A security configuration ID.</td>
    </tr>
    <tr>
      <td><code>security_policy_id</code></td>
      <td class="rqcent">&#10004;</td>
      <td>A security policy ID.</td>
    </tr>
    <tr>
      <td><code>penalty_box_conditions</code></td>
      <td class="rqcent">&#10004;</td>
      <td>A pointer to a JSON file with your penalty box conditions. File contains:<br /><br />
<pre data-lang="json">{
"conditionOperator": "AND",
"conditions": [
{
"type": "filenameMatch",
"filenames": [
"my-json-files"
],
"order": 0,
"positiveMatch": true
}
]
}   

  </tbody>
</table>

<br />

<td>A pointer to a JSON file with your penalty box conditions. File contains:<br /><br />
<pre><code class="language-json">{
  "conditionOperator": "AND",
  "conditions": [
    {
      "type": "filenameMatch",
      "filenames": [
        "my-json-files"
      ],
      "order": 0,
      "positiveMatch": true
    }
  ]
}</code></pre>
</td>

<br />
