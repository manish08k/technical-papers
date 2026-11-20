# Inline and Block Elements in HTML

## 1. Introduction

In HTML, elements are generally displayed in two common ways: inline and block.

The main difference between them is how they occupy space on a webpage.

Block elements usually start on a new line and take up the available width, whereas inline elements stay in the same line and take up only the space they need.

## 2. Block Elements

Block elements always start on a new line by default. They usually take up the full available width of their parent container.

If we place two block elements one after another, they appear on separate lines.

**Examples of block elements:**

- `<div>`
- `<p>`
- `<h1>` to `<h6>`
- `<section>`
- `<article>`
- `<header>`
- `<footer>`
- `<ul>`
- `<li>`

### Example

```html
<div>Hello</div>
<div>Welcome</div>

<p>This is a paragraph.</p>
<p>This is another paragraph.</p>
```

**Output:**

```text
Hello
Welcome

This is a paragraph.

This is another paragraph.
```

Each element starts on a new line.

## 3. Inline Elements

Inline elements do not start on a new line. They appear next to other content and take up only the space required by their content.

They are commonly used inside paragraphs or other elements to style or highlight specific content.

**Examples of inline elements:**

- `<span>`
- `<a>`
- `<strong>`
- `<b>`
- `<i>`
- `<em>`
- `<label>`
- `<img>`

### Example

```html
<p>
    This is a <strong>simple</strong> example
    of <span>inline elements</span>.
</p>

<a href="#">Google</a>
<a href="#">YouTube</a>
```

**Output:**

```text
This is a simple example of inline elements.

Google YouTube
```

The inline elements stay in the same line as long as there is enough space.

## 4. Difference Between Inline and Block Elements

| Block Elements | Inline Elements |
|---|---|
| Start on a new line. | Do not start on a new line. |
| Usually take the full available width. | Take only the required width. |
| Width and height can be set. | Width and height generally do not apply. |
| Can have margin and padding on all sides. | Vertical margins do not affect surrounding layout in the same way. |
| Examples: `div`, `p`, `h1`. | Examples: `span`, `a`, `strong`. |

## 5. Changing Display Using CSS

CSS provides a `display` property that allows us to change how an element behaves.

For example, we can make an inline element behave like a block element or a block element behave like an inline element.

### Inline to Block

```html
<span>Hello</span>
<span>Welcome</span>
```

```css
span {
    display: block;
}
```

Now both span elements appear on separate lines.

### Block to Inline

```html
<div>Hello</div>
<div>Welcome</div>
```

```css
div {
    display: inline;
}
```

Now both div elements appear on the same line.

### Inline-Block

There is also a value called `inline-block`.

It behaves like an inline element because it stays in the same line, but we can set its width and height like a block element.

```html
<span class="box">Box 1</span>
<span class="box">Box 2</span>
```

```css
.box {
    display: inline-block;
    width: 100px;
    height: 50px;
    background-color: lightblue;
}
```

Both boxes appear next to each other, and we can control their width and height.

## 6. Conclusion

Inline and block elements are important concepts in HTML because they control how elements appear on a webpage.

Block elements start on a new line and usually occupy the available width, while inline elements stay within the same line and take only the space they need.

We can also use the CSS `display` property to change their default behavior and create layouts according to our requirements.
