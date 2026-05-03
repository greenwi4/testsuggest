---
title: Test tables new editor
deprecated: false
hidden: false
metadata:
  robots: index
---
# Simple markdown table > stays markdown

| Basic | Basic | Basic |
| ----- | ----- | ----- |
| test  | test  | test  |
| test  | test  | test  |

# Markdown table with line breaks  > stays markdown

Shift+Return adds `</br>` to markup.

| Title | Title                          | Title |
| ----- | ------------------------------ | ----- |
| test  | test<br />test<br />test<br /> | test  |
| test  | test                           | test  |

# Markdown with markdown lists > changes to \<Table>

Changes to an `<Table>` element.  Is this different from the \<html> \<table> element  table element or a custom JSX table element?

<Table>
  <thead>
    <tr>
      <th>
        Title
      </th>

      <th>
        Title
      </th>

      <th>
        Title
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Test
      </td>

      <td>
        test
      </td>

      <td>
        This is a list

        - list
        - list
        - list
      </td>
    </tr>

    <tr>
      <td>
        test
      </td>

      <td>
        test
      </td>

      <td>
        This is a list

        1. list
        2. list
        3. list
        4. list
      </td>
    </tr>
  </tbody>
</Table>

# Markdown with inline markdown elements > stays markdown

| Test                   | Test | Test |
| ---------------------- | ---- | ---- |
| This is _italic_ text. | test | test |
| This is **bold** text. | test | test |

# Markdown with images > changes to \<Table>

When add image, converts to `<Table>`.  Have to go into Raw mode to add the Image URL because it escapes the !. It also turns the image URL to a link instead.

<Table>
  <thead>
    <tr>
      <th>
        Title
      </th>

      <th>
        Title
      </th>

      <th>
        Title
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        test
      </td>

      <td>
        test
      </td>

      <td>
        [test link](https://techdocs.akamai.com/cps/reference/api)
      </td>
    </tr>

    <tr>
      <td>
        test
      </td>

      <td>
        test
      </td>

      <td>
        test image.  had to add this in Raw mode

        ![image test](https://techdocs.akamai.com/ddi/img/dummy.png)
      </td>
    </tr>

    <tr>
      <td>
        test
      </td>

      <td>
        test
      </td>

      <td>
        !\[test]\([https://techdocs.akamai.com/ddi/img/dummy.png](https://techdocs.akamai.com/ddi/img/dummy.png))
      </td>
    </tr>
  </tbody>
</Table>

# Markdown with links

Stays markdown in Raw mode.  

| Title | Title                               | Title                                                 |
| ----- | ----------------------------------- | ----------------------------------------------------- |
| test  | test                                | [test](https://techdocs.akamai.com/cps/reference/api) |
| test  | test                                | test                                                  |
| test  | [test](https://techdocs.akamai.com) | test                                                  |

> 📘
>
> test callout

# Markdown with callouts > changes to \<Table>

Changes to a `<Table>` element.

<Table>
  <thead>
    <tr>
      <th>
        test
      </th>

      <th>
        test
      </th>

      <th>
        test
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        test
      </td>

      <td>
        test
      </td>

      <td>
        Test
      </td>
    </tr>

    <tr>
      <td>
        test
      </td>

      <td>
        test
      </td>

      <td>
        > 📘
        >
        > test callout.  Needed to paste it in.&#x20;
      </td>
    </tr>
  </tbody>
</Table>

# Markdown with HTML elements > stays Markdown

Keeps as markdown, but need to keep all HTML elements on the same line.  

| Title                                                            | Title | Title |
| ---------------------------------------------------------------- | ----- | ----- |
| Here is some text:</br><ol><li>list</li><li>list</li></ol><br /> | Test  | Test  |
| Here is some text                                                | Test  | Test  |

# Basic HTML table 

<table>
  <thead>
    <tr>
      <th>Project Name</th>
      <th>Lead Developer</th>
      <th>Status</th>
      <th>Deadline</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Alpha Redesign</td>
      <td>Sarah Jenkins</td>
      <td>In Progress</td>
      <td>Oct 15, 2026</td>
    </tr>
    <tr>
      <td>Beta API Integration</td>
      <td>Marcus Chen</td>
      <td>Completed</td>
      <td>Sept 01, 2026</td>
    </tr>
    <tr>
      <td>Security Patch v2.0</td>
      <td>Elena Rodriguez</td>
      <td>Pending</td>
      <td>Nov 20, 2026</td>
    </tr>
    <tr>
      <td>User Dashboard</td>
      <td>Sarah Jenkins</td>
      <td>In Progress</td>
      <td>Dec 05, 2026</td>
    </tr>
  </tbody>
</table>

# HTML table, plus markdown

No longer need to add line breaks between the `<td>` elements.  This still works, but is non standard.

<table>
<thead>
<tr>
<th style="text-align:left">What is it?</th>
<th style="text-align:center">Quantity</th>
<th style="text-align:left">Example</th>
</tr>
</thead>
<tbody>
<tr>
<td>

**List example**

</td>
<td style="text-align:center">

37

</td>
<td>

Here are the options you'll see when you click the **Additional features** button:

- **I want emojis**. Enable this to support [emojis](https://en.wikipedia.org/wiki/Emoji).
- **Enable YouTube**. Click this to enable _support_ for [YouTube](#https://www.youtube.com).
- **Add Images**. Enable this to add [images](doc:c-images) to your document.

</td>
</tr>
<tr>
<td>

**Code snippet**

</td>
<td style="text-align:center">

12

</td>
<td>

```text
{
    "name": "http2",
    "options": {
       "enabled": ""
    }
},
```

</td>
</tr>
<tr>
<td>

This is a test

</td>
<td>

This is a test

</td>
<td>

> 📘 Adding a callout
>
> You can also insert a callout into an HTML table cell by typing `/callout` .

</td>
</tr>
</tbody>
</table>

# Pure HTML table

This is pure HTML.  Only thing that doesn't transfer is callouts. 

<table>
  <thead>
    <tr>
      <th style="text-align:left">What is it?</th>
      <th style="text-align:center">Quantity</th>
      <th style="text-align:left">Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <strong>List example</strong>
      </td>
      <td style="text-align:center">
        37
      </td>
      <td>
        Here are the options you'll see when you click the <strong>Additional features</strong> button:
        <ul>
          <li><strong>I want emojis</strong>. Enable this to support <a href="https://en.wikipedia.org/wiki/Emoji">emojis</a>.</li>
          <li><strong>Enable YouTube</strong>. Click this to enable support for <a href="https://www.youtube.com">YouTube</a>.</li>
          <li><strong>Add Images</strong>. Enable this to add <a href="doc:c-images">images</a> to your document.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>
        <strong>Code snippet</strong>
      </td>
      <td style="text-align:center">
        12
      </td>
      <td>
<pre><code>{
    "name": "http2",
    "options": {
       "enabled": ""
    }
}</code></pre>
      </td>
    </tr>
    <tr>
      <td>
        This is a test
      </td>
      <td>
        This is a test
      </td>
     <tr>
      <td>
        This is a test
      </td>
      <td>
        This is a test
      </td>
      <td>
        Adding a note using the aside element.
        <aside>
          <strong>Note:</strong> You can also insert a callout into an HTML table cell by typing <code>/callout</code>.
        </aside>
      </td>
    </tr>
    </tr>
  </tbody>
</table>

# HTML table with straddled column

<table>
  <thead>
    <tr>
      <th>What is it?</th>
      <th>Quantity</th>
      <th>Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>List example</strong></td>
      <td>37</td>
      <td>
        <ul>
          <li><strong>I want emojis</strong>.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td><strong>Code snippet</strong></td>
      <td>12</td>
      <td>
<pre><code>{"name": "http2"}</code></pre>
      </td>
    </tr>
<tr>
  <td colspan="3">
  The following rows contain testing data and internal notes.
  </td>
</tr>
<tr>
  <td>This is a test</td>
  <td>Test Data</td>
  <td>
    Adding a callout
    <aside>
      <strong>Note:</strong> You can also insert a callout into an HTML table cell by typing <code>/callout</code>.
    </aside>
  </td>
</tr>
<tr>
  <td>Final Audit</td>
  <td>Pending</td>
  <td>Review scheduled for Friday.</td>
</tr>
 </tbody>
</table>

<br />