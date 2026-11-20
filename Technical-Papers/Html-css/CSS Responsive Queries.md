# CSS Responsive Queries

## 1. Introduction

CSS responsive queries, commonly called media queries, are used to make websites look good on different screen sizes and devices.

A website may look good on a laptop but its layout might not work properly on a mobile phone. Media queries help us adjust the styles based on the screen size.

For example, we can display three columns on a laptop and change them into a single column on a mobile phone.

## 2. What Are Media Queries?

Media queries allow us to apply CSS styles only when certain conditions are met.

We use the `@media` rule to write media queries in CSS.

**Example:**

```css
@media (max-width: 600px) {
    body {
        background-color: lightblue;
    }
}
```

In this example, the background color changes to light blue when the viewport width is 600 pixels or less.

## 3. Common Media Query Conditions

Some commonly used media query conditions are:

| Condition | Meaning |
|---|---|
| `max-width` | Applies styles when the screen width is below or equal to a given value. |
| `min-width` | Applies styles when the screen width is above or equal to a given value. |
| `max-height` | Applies styles when the viewport height is below or equal to a given value. |
| `min-height` | Applies styles when the viewport height is above or equal to a given value. |
| `orientation: portrait` | Applies styles when the viewport is taller than it is wide. |
| `orientation: landscape` | Applies styles when the viewport is wider than it is tall. |

## 4. Example: Responsive Layout

Consider a webpage with three boxes. On larger screens, they appear next to each other. On smaller screens, they appear one below another.

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
    gap: 15px;
}

.box {
    flex: 1;
    padding: 30px;
    background-color: lightblue;
    text-align: center;
}

@media (max-width: 600px) {
    .container {
        flex-direction: column;
    }
}
```

In this example:

- On larger screens, the boxes appear in a row.
- When the viewport width is 600px or less, the boxes appear in a column.
- The layout automatically adjusts based on the screen size.

## 5. Common Responsive Breakpoints

Breakpoints are screen widths where we change the layout of a website using media queries.

Some commonly used breakpoint values are:

| Device Type | Common Breakpoint |
|---|---|
| Mobile | 600px |
| Tablet | 768px |
| Small Laptop | 992px |
| Desktop | 1200px |

These values are not fixed rules. Developers choose breakpoints based on how their website content behaves.

## 6. Mobile-First Approach

Mobile-first is a common way of designing responsive websites.

In this approach, we first write CSS for smaller screens and then add media queries to adjust the layout for larger screens.

**Example:**

```css
.container {
    display: flex;
    flex-direction: column;
    gap: 15px;
}

@media (min-width: 768px) {
    .container {
        flex-direction: row;
    }
}
```

Here, the boxes appear in a column by default. When the viewport reaches 768px or more, they appear in a row.

This approach helps us build layouts that work well on mobile devices first.

## 7. Viewport Meta Tag

When creating responsive websites, we should also include the viewport meta tag inside the HTML head section.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

It tells the browser to use the device's actual viewport width and sets the initial zoom level.

Without this tag, mobile browsers may display the page using a wider virtual viewport, which can affect responsive layouts.

## 8. Conclusion

CSS media queries help us create responsive websites that work on mobile phones, tablets, and desktop screens.

By using the `@media` rule, we can change layouts, font sizes, spacing, and other styles based on screen conditions.

Understanding media queries is important because websites should provide a good experience on different devices and screen sizes.
