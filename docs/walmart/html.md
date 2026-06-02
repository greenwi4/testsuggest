---
title: htmlpageeee
deprecated: false
hidden: false
metadata:
  robots: index
---
<table>
  <thead>
    <tr>
      <th>Parameter</th>
      <th>Description</th>
      <th>Type</th>
      <th>Required</th>
      <th>Possible Values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>advertiserId</td>
      <td>The ID of the advertiser</td>
      <td>integer</td>
      <td>Y</td>
      <td>Unique numeric identifier</td>
    </tr>
    <tr>
      <td>startDate</td>
      <td>
        The first day to be considered in the performance report snapshot. It cannot be the current date.<br />
        <strong><em>Note:</em></strong> <em>The reports encompass data starting from midnight (00:00:00 hrs ET) on this particular date.</em>
      </td>
      <td>date</td>
      <td>Y</td>
      <td>Date should be in format: <code>yyyy-MM-dd</code></td>
    </tr>
    <tr>
      <td>endDate</td>
      <td>
        The last day to be considered in the performance report snapshot. It cannot be the current date.<br />
        <strong><em>Note:</em></strong>
        <ul>
          <li>The reports encompass data until the end of the day (23:59:59 hrs ET) for this particular date.</li>
          <li><em>If report data is not available for the requested end date, the request will fail, and the response will contain the endDate until which the performance report is available.</em></li>
        </ul>
      </td>
      <td>date</td>
      <td>Y</td>
      <td>Date should be in format: <code>yyyy-MM-dd</code></td>
    </tr>
    <tr>
      <td>attributionWindow</td>
      <td>
        Window for attribution.<br />
        <strong><em>Note:</em></strong> <em>attributionWindow is applicable only when reportType = sku.</em>
      </td>
      <td>string</td>
      <td>Optional and applicable only for <code>sku</code> report</td>
      <td>
        Allowed Values:
        <ul>
          <li><code>days14</code>: Report will include 14-day attribution columns if a user selects this value</li>
          <li><code>days30</code>: Report will include 30-day attribution columns if a user selects this value</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>salesChannel</td>
      <td>
        Sales channel for the transaction.<br />
        <strong><em>Note:</em></strong> <em>salesChannel is applicable only when reportType = sku.</em>
      </td>
      <td>string</td>
      <td>Optional and applicable only for <code>sku</code> report</td>
      <td>
        If specified, the metrics applicable for the specified sales channel are returned.<br />
        Allowed Values: <code>stores</code>, <code>online</code>, <code>acc</code>
        <ul>
          <li><code>stores</code>: If specified, only metrics prefixed with <code>storeAttributed</code> are returned</li>
          <li><code>online</code>: If specified, only metrics prefixed with <code>pickupAttributed</code>, <code>deliveryAttributed</code> are returned</li>
          <li><code>acc</code>: If specified, only metrics prefixed with <code>accAttributed</code> are returned</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>itemsetType</td>
      <td>
        Type of item set.<br />
        <strong><em>Note:</em></strong> <em>itemsetType is applicable only when reportType = sku.</em>
      </td>
      <td>string</td>
      <td>Optional and applicable only for <code>sku</code> report</td>
      <td>
        If specified, the metrics applicable for the specified itemsetType are returned.<br />
        Allowed Values: <code>halo</code>, <code>featured</code>, <code>total</code>
        <ul>
          <li><code>halo</code>: if specified, only metrics that have "Halo" in them are returned</li>
          <li><code>featured</code>: if specified, only metrics that have "Featured" in them are returned</li>
          <li><code>total</code>: if specified, only metrics that have "Halo" or "Featured" in them are returned</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>reportType</td>
      <td>Type of report to be retrieved</td>
      <td>string</td>
      <td>Y</td>
      <td>Types of Report: <code>campaign</code>, <code>lineItem</code>, <code>tactic</code>, <code>sku</code>, <code>bid</code>, <code>newBuyer</code>, <code>creative</code></td>
    </tr>
    <tr>
      <td>reportMetrics</td>
      <td>
        Choose the metrics type for your snapshot.<br />
        <strong><em>Note:</em></strong> <em>If you omit this parameter in your request, you will receive all the metrics that are relevant to the selected report type.</em>
      </td>
      <td>string</td>
      <td>N</td>
      <td>
        Please refer to the table "<a href="/advertising-partners/docs/definition-of-various-parameters-generated-across-the-snapshot-reports"><strong>Definition of Various Parameters Generated Across the Snapshot Reports</strong></a>" for detailed information on report metrics.
      </td>
    </tr>
    <tr>
      <td>scope</td>
      <td>Controls the aggregation level at which report metrics are returned.</td>
      <td>string</td>
      <td>N</td>
      <td>
        Possible values: <code>CAMPAIGN</code>, <code>CAMPAIGN_GROUP</code>
        <ul>
          <li>When <code>reportType</code> is set to <code>campaign</code>, <code>lineItem</code>, <code>sku</code>, or <code>newBuyer</code>, the default value of <code>scope</code> = <code>CAMPAIGN</code>.</li>
          <li>When <code>reportType</code> is set to <code>creative</code>, <code>tactic</code>, or <code>bid</code>: <code>scope</code> = <code>CAMPAIGN_GROUP</code> is not supported and will return an error.</li>
          <li>When <code>scope</code> = <code>CAMPAIGN_GROUP</code>, the <code>campaign</code>, <code>lineItem</code>, <code>sku</code>, and <code>newBuyer</code> reports will have 2 additional fields: <code>campaignGroupId</code> and <code>campaignGroupName</code>.</li>
          <li>If <code>scope</code> isn't defined in the request, it will be set to <code>CAMPAIGN</code> by default.</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>