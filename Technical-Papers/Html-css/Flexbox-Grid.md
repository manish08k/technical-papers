# CSS Flexbox and Grid

## 1. Introduction

Flexbox and Grid are two CSS layout systems used to arrange elements on a webpage.

When building a website, we often need to place elements next to each other, create rows and columns, or align content properly.

Flexbox and Grid make these tasks easier without using complicated positioning.

The main difference is that Flexbox is designed mainly for one-dimensional layouts, while Grid is designed for two-dimensional layouts.

## 2. CSS Flexbox

Flexbox is a CSS layout system used to arrange elements in a row or column.

It is useful when we want to align items, distribute available space, and control the direction of elements inside a container.

To use Flexbox, we set `display: flex` on the parent element.

### Example

**HTML:**

```html
<div class="container">
    <div class="box">Box 1</div>
    <div class="box">Box 2</div>
    <div class="box">Box 3</div>
</div>
```

**CSS:**

```css
.container {
    display: flex;
    gap: 10px;
}

.box {
    background-color: lightblue;
    padding: 20px;
}
```

In this example, all three boxes appear next to each other in a row.

### 2.1 Common Flexbox Properties

Some commonly used Flexbox properties are:

**1. flex-direction**

Controls the direction in which items are arranged.

```css
.container {
    display: flex;
    flex-direction: row;
}
```

Common values:

- `row` – Arranges items horizontally.
- `column` – Arranges items vertically.
- `row-reverse` – Arranges items in the reverse horizontal direction.
- `column-reverse` – Arranges items in the reverse vertical direction.

**2. justify-content**

Controls how items are distributed along the main axis.

```css
.container {
    display: flex;
    justify-content: center;
}
```

Common values:

- `flex-start`
- `flex-end`
- `center`
- `space-between`
- `space-around`
- `space-evenly`

**3. align-items**

Controls how items are aligned along the cross axis.

```css
.container {
    display: flex;
    align-items: center;
}
```

Common values:

- `flex-start`
- `flex-end`
- `center`
- `stretch`
- `baseline`

**4. flex-wrap**

Controls whether items should move to the next line when there is not enough space.

```css
.container {
    display: flex;
    flex-wrap: wrap;
}
```

**5. gap**

Adds space between flex items.

```css
.container {
    display: flex;
    gap: 20px;
}
```

## 3. CSS Grid

CSS Grid is a layout system used to arrange elements in rows and columns.

It is useful when we need to create more complex layouts, such as dashboards, image galleries, and webpage structures.

To use Grid, we set `display: grid` on the parent element.

### Example

**HTML:**

```html
<div class="container">
    <div class="box">Box 1</div>
    <div class="box">Box 2</div>
    <div class="box">Box 3</div>
    <div class="box">Box 4</div>
</div>
```

**CSS:**

```css
.container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
}

.box {
    background-color: lightblue;
    padding: 20px;
}
```

In this example, the boxes are arranged in two columns. The `1fr` value divides the available space equally between the columns.

### 3.1 Common Grid Properties

**1. grid-template-columns**

Defines the number and size of columns.

```css
.container {
    display: grid;
    grid-template-columns: 200px 200px;
}
```

This creates two columns, each with a width of 200px.

**2. grid-template-rows**

Defines the size of rows.

```css
.container {
    display: grid;
    grid-template-rows: 100px 150px;
}
```

This creates two rows with heights of 100px and 150px.

**3. gap**

Adds space between rows and columns.

```css
.container {
    display: grid;
    gap: 20px;
}
```

**4. grid-column**

Controls how many columns an item occupies.

```css
.box1 {
    grid-column: span 2;
}
```

This makes the element occupy two columns.

**5. grid-row**

Controls how many rows an item occupies.

```css
.box1 {
    grid-row: span 2;
}
```

This makes the element occupy two rows.

## 4. Difference Between Flexbox and Grid

| Flexbox | Grid |
|---|---|
| Mainly one-dimensional layout. | Two-dimensional layout. |
| Works with a row or column at a time. | Works with rows and columns together. |
| Useful for navigation bars and buttons. | Useful for dashboards and page layouts. |
| Items are arranged along a main axis. | Items are placed inside rows and columns. |
| Uses `display: flex`. | Uses `display: grid`. |

## 5. When Should We Use Flexbox and Grid?

**Use Flexbox when:**
- Creating navigation bars.
- Aligning buttons.
- Arranging items in a row or column.
- Centering content.
- Creating simple component layouts.

**Use Grid when:**
- Creating multiple rows and columns.
- Building image galleries.
- Designing dashboards.
- Creating complex page layouts.
- Controlling the size and position of items in a grid.

Both Flexbox and Grid can also be used together in the same webpage.

## 6. Conclusion

Flexbox and Grid are important CSS layout systems that make it easier to arrange elements on a webpage.

Flexbox is mainly used for arranging items in one direction, while Grid is useful for creating layouts with rows and columns.

Understanding both helps us build clean, organized, and responsive websites.
