---
title: test case
deprecated: false
hidden: false
metadata:
  robots: index
---
# test case

## Simple markdown table

| Column A | Column B |
| --- | --- |
| Plain text | Plain text |
| `inline code` | [ReadMe](https://readme.com) |

## Markdown with images

| Item | Image |
| --- | --- |
| Markdown image syntax | ![ReadMe logo](https://files.readme.io/37a23dc-small-readme-blue.png) |

## Markdown with lists

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Item
      </th>

      <th>
        Details
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        List inside a table cell
      </td>

      <td>
        - First item
        - Second item
        - Third item
      </td>
    </tr>
  </tbody>
</Table>

## Markdown with callouts

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Item
      </th>

      <th>
        Details
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Callout inside a table cell
      </td>

      <td>
        <Callout icon="📘" theme="info">
        This callout is nested inside a ReadMe `<Table>` cell.
        </Callout>
      </td>
    </tr>
  </tbody>
</Table>

## Markdown with HTML elements - stays markdown

| Item | Inline HTML |
| --- | --- |
| One-line HTML | <span class="table-repro-inline">This span is on one line.</span> |
| HTML with attributes | <kbd>Command</kbd> + <kbd>K</kbd> |

## HTML table plus markdown

<table>
  <thead>
    <tr>
      <th>Item</th>
      <th>Markdown in HTML table</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Bold text</td>
      <td>**This markdown bold text is inside lowercase HTML `<table>`.**</td>
    </tr>
    <tr>
      <td>List text</td>
      <td>
        - First markdown list item
        - Second markdown list item
      </td>
    </tr>
  </tbody>
</table>
