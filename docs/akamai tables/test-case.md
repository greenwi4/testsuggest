---
title: Test tables new editor
deprecated: false
hidden: false
metadata:
  robots: index
---



This is text&#x20;


<Image src="https://techdocs.akamai.com/control-ctr/img/cc-overview-v3.png" alt="test test" align="right" width="500px" />


This is text

## Using HTML tag \<img> 

Must add in / Custom HTML component for the border to work. This turns it into an \<HTMLBlock> tag.

<HTMLBlock>{`
<img 
src="https://techdocs.akamai.com/control-ctr/img/cc-overview-v3.png" 
alt="this is alt text" 
width="420" 
height="420" 
style="border: 5px solid black;"
/>
`}</HTMLBlock>

<br />

# Tables

## Markdown

| Test | Test | Test |
| ---- | ---- | ---- |
| Test | Test | Test |
| Test | Test | Test |

<HTMLBlock>{`
<table>
  <thead>
    <tr>
      <th>Header 1</th>
      <th>Header 2</th>
      <th>Header 3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Test</td>
      <td>Test</td>
      <td>Test</td>
    </tr>
    <tr>
      <td>Test</td>
      <td>Test</td>
      <td>Test</td>
    </tr>
    <tr>
      <td>Test</td>
      <td>Test</td>
      <td>Test</td>
    </tr>
  </tbody>
</table>
`}</HTMLBlock>

<br />

# A header

This is some text.


<Image src="https://techdocs.akamai.com/control-ctr/img/cc-overview-v3.png" alt="test" align="right" width="400px" />




# Another header

Text