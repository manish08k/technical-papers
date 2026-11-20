# CSS Specificity

## 1. Introduction

CSS specificity is a rule that browsers use to decide which CSS style should be applied when multiple CSS rules target the same HTML element.

Sometimes we write different styles for the same element. In that situation, the browser checks the specificity of each selector and applies the style with higher priority.

Understanding specificity helps us avoid confusion when CSS styles conflict with each other.

## 2. Types of CSS Selectors and Their Priority

CSS selectors have different levels of specificity.

The common order of priority, from highest to lowest, is:

1. Inline styles
2. ID selectors
3. Class, attribute, and pseudo-class selectors
4. Element and pseudo-element selectors

### 2.1 Inline Styles

Inline styles are written directly inside an HTML element using the `style` attribute.

They have higher specificity than normal ID, class, and element selectors.

**Example:**

```html
<p style="color: red;">Hello World</p>
```

Here, the text appears red because the style is written directly inside the element.

### 2.2 ID Selectors

ID selectors are used to target an element with a specific ID.

In CSS, we use the `#` symbol to select an ID.

**Example:**

```html
<p id="message">Hello World</p>
```

```css
#message {
    color: blue;
}
```

### 2.3 Class Selectors

Class selectors are used to apply styles to one or more HTML elements.

In CSS, we use the `.` symbol to select a class.

**Example:**

```html
<p class="text">Hello World</p>
```

```css
.text {
    color: green;
}
```

### 2.4 Element Selectors

Element selectors target HTML elements directly using their tag names.

**Example:**

```html
<p>Hello World</p>
```

```css
p {
    color: orange;
}
```

## 3. Understanding Specificity with an Example

Consider the following HTML and CSS:

```html
<p id="message" class="text">
    Hello World
</p>
```

```css
p {
    color: orange;
}

.text {
    color: green;
}

#message {
    color: blue;
}
```

All three CSS rules target the same paragraph.

However, the text appears blue because the ID selector has higher specificity than the class and element selectors.

## 4. Specificity Calculation

CSS specificity can be represented using four values:

`(a, b, c, d)`

- `a` – Inline styles.
- `b` – Number of ID selectors.
- `c` – Number of class, attribute, and pseudo-class selectors.
- `d` – Number of element and pseudo-element selectors.

Let's look at some examples.

| Selector | Specificity |
|---|---|
| `p` | (0, 0, 0, 1) |
| `.text` | (0, 0, 1, 0) |
| `#message` | (0, 1, 0, 0) |
| `div p` | (0, 0, 0, 2) |
| `#message .text` | (0, 1, 1, 0) |

The browser compares these values from left to right.

For example:

```css
.text {
    color: green;
}

#message {
    color: blue;
}
```

The ID selector wins because its specificity is higher than the class selector.

## 5. What Happens When Specificity Is the Same?

When two selectors have the same specificity, the browser generally applies the rule that comes later in the CSS.

**Example:**

```css
.text {
    color: red;
}

.text {
    color: blue;
}
```

The text appears blue because the second rule comes after the first one.

This is called the source order or cascade order.

## 6. The !important Rule

CSS provides an `!important` declaration to give a style priority over normal declarations.

**Example:**

```css
p {
    color: red !important;
}

#message {
    color: blue;
}
```

The paragraph appears red because the `!important` declaration takes priority over the normal declaration.

However, using `!important` too often can make CSS difficult to maintain.

## 7. Conclusion

CSS specificity determines which style is applied when multiple CSS rules target the same element.

Inline styles, IDs, classes, and element selectors have different specificity levels.

Understanding specificity helps us write better CSS, resolve styling conflicts, and maintain our code more easily.
