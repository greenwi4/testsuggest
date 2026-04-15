---
title: adaptiveAcceleration
deprecated: false
hidden: false
metadata:
  robots: index
---
{/* WARNING: DO NOT MODIFY THIS TOPIC! IT IS GENERATED FROM ELSEWHERE! */}

{/* See https://techdocs.akamai.com/internal-ux-writing/docs/papi-feature-catalog */}

{/* Generated on 2026-04-08T12:47:46Z */}

<ul>
<li><strong>Property Manager name</strong>: <a href="doc:adaptive-accel">Adaptive Acceleration</a></li>

<li><strong>Behavior version</strong>: The <code>latest</code> rule format supports the <code>adaptiveAcceleration</code> behavior v2.4.</li>

<li><strong>Rule format status</strong>: <a href="ref:api-versioning">Beta, possible breaking changes</a></li>

<li><strong>Access</strong>: <a href="ref:advanced-and-locked-features">Read/Write</a></li>

<li><strong>Allowed in includes</strong>: <a href="ref:includes#relationship-with-parent-properties">Not available for <code>latest</code> rule format</a></li>
</ul><hr />
<p>Adaptive Acceleration uses HTTP/2 server push functionality with Ion properties to pre-position content and improve the performance of HTML page loading based on real user monitoring (RUM) timing data. It also helps browsers to preconnect to content that’s likely needed for upcoming requests. To use this behavior, make sure you enable the <a href="ref:latest-http2"><code>http2</code></a> behavior. Use the <a href="https://techdocs.akamai.com/adaptive-acceleration/reference">Adaptive Acceleration API</a> to report on the set of assets this feature optimizes.</p>
<p>Note that the <a href="ref:latest-edge-side-includes"><code>edge​Side​Includes</code></a> and <a href="ref:latest-akamaizer"><code>akamaizer</code></a> behaviors are not compatible with the <code>enable​Ro</code> and <code>enable​Brotli​Compression</code> options in the <a href="ref:latest-adaptive-acceleration"><code>adaptive​Acceleration</code></a> behavior for Ion products. </p>

<table class="xdep">
<thead class="xdep">
<tr class="row_head">
<th>Option</th>
<th>Type</th>
<th>Description</th>
<th><a href="ref:latest-behaviors#object-requirements">Requires</a></th>
</tr>
</thead>
<tbody class="xdep">
<tr class="row_option source" id="source" >
<td class><code>source</code></td>
<td>enum </td>
<td><p>The source Adaptive Acceleration uses to gather the real user monitoring timing data, either <code>MPULSE</code> or <code>REAL_​USER_​MONITORING</code>.</p></td>
<td></td>
<th><pre class="input">{"displayType":"enum","options":["REAL_USER_MONITORING","MPULSE"],"tag":"select"}</pre><pre class="visible"></pre></th></tr>
<tr class="row_enum source">
<td></td>
<td><code>REAL_​USER_​MONITORING</code></td>
<td><p>Injects Java​Script into HTML pages served to end-user clients that monitors page-load performance and reports on various data, such as browser type and geographic location. The <a href="ref:latest-report"><code>report</code></a> behavior allows you to configure logs.</p></td>
<td></td>
</tr>
<tr class="row_enum source">
<td></td>
<td><code>MPULSE</code></td>
<td><p>Supports all optimizations and requires the <a href="ref:latest-m-pulse"><code>m​Pulse</code></a> behavior added by default to new Ion properties.</p></td>
<td></td>
</tr>
<tr class="row_option enablePush" id="enable-push" data-visible='{"if":{"expression":{"op":"or","params":[{"attribute":"modulesOnContract","op":"contains","scope":"global","value":"RUA_IEH"},{"attribute":"property.modulesOnContract","op":"contains","scope":"global","value":"RUA_IEH"}]},"op":"not"}}'>
<td class><code>enable​Push</code></td>
<td>boolean </td>
<td><p>Recognizes resources like Java​Script, CSS, and images  based on gathered timing data and sends these resources to a browser as it's waiting for a response to the initial request for your website or app. See <a href="https://techdocs.akamai.com/ion/docs/set-up-adaptive-acceleration#about-automatic-server-push">Automatic Server Push</a> for more information.</p></td>
<td></td>
<th><pre class="input">{"displayType":"boolean","tag":"input","type":"checkbox"}</pre><pre class="visible">{"if":{"expression":{"op":"or","params":[{"attribute":"modulesOnContract","op":"contains","scope":"global","value":"RUA_IEH"},{"attribute":"property.modulesOnContract","op":"contains","scope":"global","value":"RUA_IEH"}]},"op":"not"}}</pre></th></tr>
<tr class="row_option enablePreconnect" id="enable-preconnect" >
<td class><code>enable​Preconnect</code></td>
<td>boolean </td>
<td><p>Allows browsers to anticipate what connections your site needs, and establishes those connections ahead of time. See <a href="https://techdocs.akamai.com/ion/docs/set-up-adaptive-acceleration#about-automatic-preconnect">Automatic Preconnect</a> for more information.</p></td>
<td></td>
<th><pre class="input">{"displayType":"boolean","tag":"input","type":"checkbox"}</pre><pre class="visible"></pre></th></tr>
<tr class="row_option preloadEnable" id="preload-enable" >
<td class><code>preload​Enable</code></td>
<td>boolean </td>
<td><p>Allows browsers to preload necessary fonts before they fetch and process other resources. See <a href="https://techdocs.akamai.com/ion/docs/set-up-adaptive-acceleration#about-automatic-font-preload">Automatic Font Preload</a> for more information.</p></td>
<td></td>
<th><pre class="input">{"displayType":"boolean","tag":"input","type":"checkbox"}</pre><pre class="visible"></pre></th></tr>
<tr class="row_option abLogic" id="ab-logic" >
<td class><code>ab​Logic</code></td>
<td>enum </td>
<td><p>Specifies whether to use Adaptive Acceleration in an A/B testing environment. To include Adaptive Acceleration data in your A/B testing, specify the mode you want to apply. Otherwise, <code>DISABLED</code> by default. See <a href="https://techdocs.akamai.com/ion/reference/enable-ab-testing">Add A/B testing to A2</a> for details.</p></td>
<td></td>
<th><pre class="input">{"displayType":"enum","options":["DISABLED","CLOUDLETS","MANUAL"],"tag":"select"}</pre><pre class="visible"></pre></th></tr>
<tr class="row_enum abLogic">
<td></td>
<td><code>DISABLED</code></td>
<td><p>Disables the use of Adaptive Acceleration in the A/B testing environment. This is the default value.</p></td>
<td></td>
</tr>
<tr class="row_enum abLogic">
<td></td>
<td><code>CLOUDLETS</code></td>
<td><p>Applies A/B testing using Cloudlets.</p></td>
<td></td>
</tr>
<tr class="row_enum abLogic">
<td></td>
<td><code>MANUAL</code></td>
<td><p>Applies A/B testing by redirecting a request to one of two origin servers, based on the cookie included with the request.</p></td>
<td></td>
</tr>
<tr class="row_option cookieName" id="cookie-name" data-visible='{"if":{"attribute":"abLogic","op":"eq","value":"MANUAL"}}'>
<td class><code>cookie​Name</code></td>
<td>string </td>
<td><p>This specifies the name of the cookie file used for redirecting the requests in the A/B testing environment.</p></td>
<td><code>ab​Logic</code> is <code>MANUAL</code></td>
<th><pre class="input">{"displayType":"string","tag":"input","type":"text"}</pre><pre class="visible">{"if":{"attribute":"abLogic","op":"eq","value":"MANUAL"}}</pre></th></tr>
<tr class="row_option enableRo" id="enable-ro" >
<td class><code>enable​Ro</code></td>
<td>boolean </td>
<td><p>Enables the Resource Optimizer, which automates the compression and delivery of your <code>.css</code>, <code>.js</code>, and <code>.svg</code> content using a combination of Brotli and Zopfli compressions. The compression is performed offline, during a time to live that the feature automatically sets. See the <a href="ref:latest-resource-optimizer"><code>resource​Optimizer</code></a> and <a href="ref:latest-resource-optimizer-extended-compatibility"><code>resource​Optimizer​Extended​Compatibility</code></a> behaviors for more details.</p></td>
<td></td>
<th><pre class="input">{"displayType":"boolean","tag":"input","type":"checkbox"}</pre><pre class="visible"></pre></th></tr>
<tr class="row_option enableBrotliCompression" id="enable-brotli-compression" >
<td class><code>enable​Brotli​Compression</code></td>
<td>boolean </td>
<td><p>Applies Brotli compression, converting your origin content to cache on edge servers.</p></td>
<td></td>
<th><pre class="input">{"displayType":"boolean","tag":"input","type":"checkbox"}</pre><pre class="visible"></pre></th></tr>
<tr class="row_option enableForNoncacheable" id="enable-for-noncacheable" data-visible='{"if":{"attribute":"enableBrotliCompression","op":"eq","value":true}}'>
<td class><code>enable​For​Noncacheable</code></td>
<td>boolean </td>
<td><p>Applies Brotli compression to non-cacheable content.</p></td>
<td><code>enable​Brotli​Compression</code> is <code>true</code></td>
<th><pre class="input">{"displayType":"boolean","tag":"input","type":"checkbox"}</pre><pre class="visible">{"if":{"attribute":"enableBrotliCompression","op":"eq","value":true}}</pre></th></tr>
</tbody>
</table>

<br />