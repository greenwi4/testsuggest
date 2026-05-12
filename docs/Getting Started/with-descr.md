---
title: with descr
excerpt: test repro branch merge 2
deprecated: false
hidden: false
metadata:
  robots: index
next:
  description: Repro step next action 233
  pages:
    - slug: without-descr
      title: without descr
      type: basic
---
<br />

<HTMLBlock>{`
https://placehold.co/320x120.png?text=Codex+No+Enter
`}</HTMLBlock>

```text
sdfsdfsd
```

<br />

```text
dsfdsf
```

```text
```
```text
```

![](https://placehold.co/320x120.png?text=Codex+Enter)

> 📘 test
>
> message

> ✅ test
>
> message

> ⚠️ test
>
> message

> 🛑 test
>
> message

# Image Lightbox Stress Test

## 1. Plain markdown

![plain](https://placehold.co/320x120/blue/white?text=plain)

## 2. Inside a callout

> 📘 **Info callout**
>
> ![in-callout](https://placehold.co/320x120/green/white?text=callout)

## 3. Inside a table

| Col 1 | Image                                                          | Col 3 |
| ----- | -------------------------------------------------------------- | ----- |
| Text  | ![in-table](https://placehold.co/200x100/red/white?text=table) | Text  |

## 4. Inside a list

- List item 1
- ![in-list](https://placehold.co/300x100/orange/white?text=list)
- List item 3

## 5. Nested in numbered list

1. Step one
2. ![in-nl](https://placehold.co/280x110/purple/white?text=numbered)
3. Step three

## 6. Inside accordion/details

<details>
<summary>Click to expand</summary>

![in-details](https://placehold.co/320x120/teal/white?text=accordion)

</details>

## 7. Wide image (triggers wide-image branch)

![wide](https://placehold.co/1600x300/grey/white?text=wide-image-2000-wide)

## 8. Two images side by side in same callout

> ⚠️ **Warning callout**
>
> ![cb1](https://placehold.co/200x100/red/white?text=img1)
>
> ![cb2](https://placehold.co/200x100/red/white?text=img2)

## 9. Image inside blockquote

> Regular blockquote (not callout)
>
> ![in-bq](https://placehold.co/300x120/navy/white?text=blockquote)

## 10. Image in tab block (if your project uses .tabs)

<Tabs>
  <Tab title="First Tab">
    <img src='https://placehold.co/300x120/teal/white?text=in-tab' />
  </Tab>

  <Tab title="Second Tab">
    Here's content that's only inside the second Tab.
  </Tab>

  <Tab title="Third Tab">
    Here's content that's only inside the third Tab.
  </Tab>
</Tabs>

<br />
