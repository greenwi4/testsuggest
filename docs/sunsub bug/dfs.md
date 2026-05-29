---
title: dfs
deprecated: false
hidden: false
metadata:
  robots: index
---
table in an HTML block:

<HTMLBlock>{`
<table>
  <thead>
    <tr>
      <th><p>Name</p></th>
      <th><p>Description</p></th>
    </tr>
  </thead>
  <tbody>
    <tr class="tablesubhead">
      <td colspan="2"><p>Address</p></td>
    </tr>
    <tr>
      <td><p><code>address</code></p></td>
      <td><p>An object that describes the customer's physical address. The <code>address</code> object is optional; if provided, the only required property is <code>country</code>.</p></td>
    </tr>
    <tr>
      <td><p><code>address.street</code></p></td>
      <td><p>The customer's street address, including apartment number or other designation.</p></td>
    </tr>
    <tr>
      <td><p><code>address.city</code></p></td>
      <td><p>The name of the customer's city.</p></td>
    </tr>
    <tr>
      <td><p><code>address.state</code></p></td>
      <td><p>The customer's two-character state abbreviation. US territories and armed forces codes are supported.</p></td>
    </tr>
    <tr>
      <td><p><code>address.zip</code></p></td>
      <td><p>The customer's five- or nine-digit US ZIP code.</p></td>
    </tr>
    <tr>
      <td><p><code>address.country</code></p></td>
      <td><p><code>US</code></p></td>
    </tr>
    <tr class="tablesubhead">
      <td colspan="2"><p>Phone</p></td>
    </tr>
    <tr>
      <td><p><code>phoneNumber</code></p></td>
      <td><p>Optional leading <code>1</code> followed by the area code and phone number, digits only. As examples: <code>18005154321</code>, <code>8005154321</code>.</p></td>
    </tr>
    <tr class="tablesubhead">
      <td colspan="2"><p>Language</p></td>
    </tr>
    <tr>
      <td><p><code>language</code></p></td>
      <td><p><code>language</code> can be <code>en-US</code> (English) or <code>es-US</code> (Spanish). The default is <code>en-US</code>.</p></td>
    </tr>
    <tr class="tablesubhead">
      <td colspan="2"><p>Tax Identifier</p></td>
    </tr>
    <tr>
      <td><p><code>ssn</code></p></td>
      <td><p>The customer's full-nine or last-four US tax identifier, digits only. See [Tax Identifiers](#tax-identifiers) for more information.</p></td>
    </tr>
  </tbody>
</table>
`}</HTMLBlock>

Just an HTML table. colspan and custom styling are missing

<table>
  <thead>
    <tr>
      <th><p>Name</p></th>
      <th><p>Description</p></th>
    </tr>
  </thead>

  <tbody>
    <tr class="tablesubhead">
      <td colspan="2"><p>Address</p></td>
    </tr>

    <tr>
      <td><p><code>address</code></p></td>
      <td><p>An object that describes the customer's physical address. The <code>address</code> object is optional; if provided, the only required property is <code>country</code>.</p></td>
    </tr>

    <tr>
      <td><p><code>address.street</code></p></td>
      <td><p>The customer's street address, including apartment number or other designation.</p></td>
    </tr>

    <tr>
      <td><p><code>address.city</code></p></td>
      <td><p>The name of the customer's city.</p></td>
    </tr>

    <tr>
      <td><p><code>address.state</code></p></td>
      <td><p>The customer's two-character state abbreviation. US territories and armed forces codes are supported.</p></td>
    </tr>

    <tr>
      <td><p><code>address.zip</code></p></td>
      <td><p>The customer's five- or nine-digit US ZIP code.</p></td>
    </tr>

    <tr>
      <td><p><code>address.country</code></p></td>
      <td><p><code>US</code></p></td>
    </tr>

    <tr class="tablesubhead">
      <td colspan="2"><p>Phone</p></td>
    </tr>

    <tr>
      <td><p><code>phoneNumber</code></p></td>
      <td><p>Optional leading <code>1</code> followed by the area code and phone number, digits only. As examples: <code>18005154321</code>, <code>8005154321</code>.</p></td>
    </tr>

    <tr class="tablesubhead">
      <td colspan="2"><p>Language</p></td>
    </tr>

    <tr>
      <td><p><code>language</code></p></td>
      <td><p><code>language</code> can be <code>en-US</code> (English) or <code>es-US</code> (Spanish). The default is <code>en-US</code>.</p></td>
    </tr>

    <tr class="tablesubhead">
      <td colspan="2"><p>Tax Identifier</p></td>
    </tr>

    <tr>
      <td><p><code>ssn</code></p></td>
      <td><p>The customer's full-nine or last-four US tax identifier, digits only. See [Tax Identifiers](#tax-identifiers) for more information.</p></td>
    </tr>
  </tbody>
</table>

<br />
