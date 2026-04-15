---
title: widget
deprecated: false
hidden: false
metadata:
  robots: index
---
<!-- WARNING: DO NOT MODIFY THIS TOPIC! IT IS GENERATED FROM ELSEWHERE! -->

<!-- See https://techdocs.akamai.com/internal-ux-writing/docs/papi-feature-catalog -->

<!-- Generated on 2026-01-14T20:32:41Z -->

<ul>
<li><strong>Property Manager name</strong>: <a href="doc:aggd-rpt">Aggregated Reporting</a></li>

<li><strong>Behavior version</strong>: The <code>v2026-01-09</code> rule format supports the <code>aggregatedReporting</code> behavior v1.2.</li>

<li><strong>Rule format status</strong>: <a href="ref:api-versioning">GA, stable</a></li>

<li><strong>Access</strong>: <a href="ref:advanced-and-locked-features">Read/Write</a></li>

<li><strong>Allowed in includes</strong>: <a href="ref:includes">No (temporarily)</a></li>
</ul><hr />
<p>Configure a custom report that collects traffic data. The data is based on one to four variables, such as <code>sum</code>, <code>average</code>, <code>min</code>, and <code>max</code>. These aggregation attributes help compile traffic data summaries. </p>
<p>This behavior is part of <a href="https://techdocs.akamai.com/iot-ota-updates/docs/welcome-ota-updates">Internet of Things OTA Update</a>, which allows users to securely download firmware to vehicle head units over cellular networks. Use this system to create statistical reports by defining <a href="https://techdocs.akamai.com/property-mgr/reference/variables">PAPI variables</a>, such as sum of requests sent by a specific car model. For example, you can send the sum of data in bytes, number of requests, and number of completed downloads based on the selected car model, campaign, and year. </p>
<p>To configure the behavior, see <a href="https://techdocs.akamai.com/iot-ota-updates/docs/config-aggd-rpt-beh">Configure the aggregated reporting behavior</a> in the Io​T OTA Updates documentation. For more information including accessing the report, see <a href="https://techdocs.akamai.com/property-mgr/docs/aggd-rpt">Aggregated Reporting</a>. Also, you can configure variables with the <a href="ref:ga-set-variable"><code>set​Variable</code></a>, <a href="ref:ga-request-type-marker"><code>request​Type​Marker</code></a>, and <a href="ref:ga-download-complete-marker"><code>download​Complete​Marker</code></a> behaviors. To learn more about the combinations of OTA Updates behaviors, see <a href="https://techdocs.akamai.com/iot-ota-updates/docs/behaviors-reports">Behaviors in reports</a>. </p>
<p>Akamai also offers the <a href="ref:ga-report"><code>report</code></a> behavior to specify the HTTP request headers or cookies to include in your <a href="https://techdocs.akamai.com/log-delivery/docs">Log Delivery Service</a> reports.</p>

<table class="xdep">
<thead class="xdep">
<tr class="row_head">
<th>Option</th>
<th>Type</th>
<th>Description</th>
<th><a href="ref:ga-behaviors#object-requirements">Requires</a></th>
</tr>
</thead>
<tbody class="xdep">
<tr class="row_option enabled" id="enabled" >
<td class><code>enabled</code></td>
<td>boolean </td>
<td><p>Enables aggregated reporting.</p></td>
<td></td>
<th><pre class="input">{"displayType":"boolean","tag":"input","type":"checkbox"}</pre><pre class="visible"></pre></th></tr>
<tr class="row_option reportName" id="report-name" data-visible='{"if":{"attribute":"enabled","op":"eq","value":true}}'>
<td class><code>report​Name</code></td>
<td>string </td>
<td><p>The unique name of the aggregated report within the property. If you reconfigure any attributes or variables in the aggregated reporting behavior, update this field to a unique value to enable logging data in a new instance of the report.</p></td>
<td></td>
<th><pre class="input">{"displayType":"string","tag":"input","type":"text"}</pre><pre class="visible">{"if":{"attribute":"enabled","op":"eq","value":true}}</pre></th></tr>
<tr class="row_option attributesCount" id="attributes-count" data-visible='{"if":{"attribute":"enabled","op":"eq","value":true}}'>
<td class><code>attributes​Count</code></td>
<td>number (1-4)</td>
<td><p>The number of attributes to include in the report, ranging from 1 to 4.</p></td>
<td></td>
<th><pre class="input">{"displayType":"number","max":[4],"min":[1],"tag":"input","type":"range"}</pre><pre class="visible">{"if":{"attribute":"enabled","op":"eq","value":true}}</pre></th></tr>
<tr class="row_option attribute1" id="attribute1" data-visible='{"if":{"attribute":"enabled","op":"eq","value":true}}'>
<td class><code>attribute1</code></td>
<td>string (allows&nbsp;<a href="ref:variables">variables</a>)</td>
<td><p>Specify a previously user-defined variable name as a report attribute. The values extracted for all attributes range from 0 to 20 characters.</p></td>
<td></td>
<th><pre class="input">{"displayType":"string","tag":"input","type":"text"}</pre><pre class="visible">{"if":{"attribute":"enabled","op":"eq","value":true}}</pre></th></tr>
<tr class="row_option attribute2" id="attribute2" data-visible='{"if":{"op":"and","params":[{"attribute":"enabled","op":"eq","value":true},{"attribute":"attributesCount","op":"gte","value":2}]}}'>
<td class><code>attribute2</code></td>
<td>string (allows&nbsp;<a href="ref:variables">variables</a>)</td>
<td><p>Specify a previously user-defined variable name as a report attribute. The values extracted for all attributes range from 0 to 20 characters.</p></td>
<td><code>attributes​Count</code> &#8805; <code>2</code></td>
<th><pre class="input">{"displayType":"string","tag":"input","type":"text"}</pre><pre class="visible">{"if":{"op":"and","params":[{"attribute":"enabled","op":"eq","value":true},{"attribute":"attributesCount","op":"gte","value":2}]}}</pre></th></tr>
<tr class="row_option attribute3" id="attribute3" data-visible='{"if":{"op":"and","params":[{"attribute":"enabled","op":"eq","value":true},{"attribute":"attributesCount","op":"gte","value":3}]}}'>
<td class><code>attribute3</code></td>
<td>string (allows&nbsp;<a href="ref:variables">variables</a>)</td>
<td><p>Specify a previously user-defined variable name as a report attribute. The values extracted for all attributes range from 0 to 20 characters.</p></td>
<td><code>attributes​Count</code> &#8805; <code>3</code></td>
<th><pre class="input">{"displayType":"string","tag":"input","type":"text"}</pre><pre class="visible">{"if":{"op":"and","params":[{"attribute":"enabled","op":"eq","value":true},{"attribute":"attributesCount","op":"gte","value":3}]}}</pre></th></tr>
<tr class="row_option attribute4" id="attribute4" data-visible='{"if":{"op":"and","params":[{"attribute":"enabled","op":"eq","value":true},{"attribute":"attributesCount","op":"eq","value":4}]}}'>
<td class><code>attribute4</code></td>
<td>string (allows&nbsp;<a href="ref:variables">variables</a>)</td>
<td><p>Specify a previously user-defined variable name as a report attribute. The values extracted for all attributes range from 0 to 20 characters.</p></td>
<td><code>attributes​Count</code> is <code>4</code></td>
<th><pre class="input">{"displayType":"string","tag":"input","type":"text"}</pre><pre class="visible">{"if":{"op":"and","params":[{"attribute":"enabled","op":"eq","value":true},{"attribute":"attributesCount","op":"eq","value":4}]}}</pre></th></tr>
</tbody>
</table>