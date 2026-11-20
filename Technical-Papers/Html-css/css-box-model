# CSS Box Model

## 1. Introduction

The CSS Box Model is one of the basic concepts in CSS. Every HTML element on a webpage is treated as a rectangular box. CSS uses this model to control the space an element takes up and the space around it.

Understanding the Box Model helps us arrange elements properly and control the layout of a webpage.

## 2. Parts of the Box Model

The CSS Box Model has four main parts:

### 2.1 Content

Content is the actual information inside an HTML element, such as text, images, or other elements.

We can control its size using `width` and `height`.

### 2.2 Padding

Padding is the space between the content and the border.

It creates some space inside the element, so the content does not touch the border directly.

### 2.3 Border

The border is the line that surrounds the content and padding.

We can change its width, style, and color using CSS.

### 2.4 Margin

Margin is the space outside the border. It creates distance between one element and other elements on the page.

## 3. Example

Here is a simple example to understand the Box Model:

```html
<div class="box">
    Hello World
</div>
```

```css
.box {
    width: 200px;
    height: 100px;
    padding: 20px;
    border: 5px solid black;
    margin: 15px;
}
```

In this example:

- Content width is 200px.
- Content height is 100px.
- Padding is 20px on each side.
- Border is 5px on each side.
- Margin is 15px on each side.

The total width of the element, including padding and border, is:

`200 + 40 + 10 = 250px`

The total height is:

`100 + 40 + 10 = 150px`

Margin adds extra space outside these dimensions.

## 4. Box-Sizing Property

CSS provides a property called `box-sizing` that changes how the width and height of an element are calculated.

There are two commonly used values.

### 4.1 content-box

This is the default value in CSS.

When we set the width and height, they apply only to the content. Padding and border are added separately.

```css
.box {
    width: 200px;
    padding: 20px;
    border: 5px solid black;
    box-sizing: content-box;
}
```

The total width becomes 250px.

### 4.2 border-box

With `border-box`, the width and height include the content, padding, and border.

```css
.box {
    width: 200px;
    padding: 20px;
    border: 5px solid black;
    box-sizing: border-box;
}
```

The total width remains 200px.

This makes it easier to manage element sizes while designing layouts.

## 5. Practical Usage

The Box Model is used whenever we design a webpage.

For example:
- Padding helps create space inside buttons and cards.
- Margin helps maintain distance between different sections.
- Borders help separate or highlight elements.
- Width and height help control the size of elements.

## 6. Conclusion

The CSS Box Model explains how space is calculated around every HTML element. It consists of content, padding, border, and margin.

Once we understand these four parts, it becomes easier to control spacing, element sizes, and webpage layouts using CSS.
