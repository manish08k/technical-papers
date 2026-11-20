# Common CSS Styling Classes

## 1. Introduction

CSS styling classes are used to apply different styles to HTML elements. They help us control how text, buttons, backgrounds, spacing, and other elements look on a webpage.

Instead of writing the same styles repeatedly, we can create a CSS class and reuse it wherever needed.

For example, we can create a class for a button and use the same class on multiple buttons.

## 2. Common CSS Styling Classes

### 2.1 Text Styling

Text styling classes are used to change the appearance of text.

Common properties include:

- `color` – Changes the text color.
- `font-size` – Changes the text size.
- `font-weight` – Controls how bold the text appears.
- `text-align` – Aligns text to the left, right, or center.
- `text-decoration` – Adds or removes decorations such as underlines.

**Example:**

```html
<h1 class="heading">Welcome</h1>
<p class="description">This is a simple website.</p>
```

```css
.heading {
    color: blue;
    font-size: 30px;
    text-align: center;
}

.description {
    color: gray;
    font-size: 16px;
}
```

### 2.2 Background Styling

Background classes are used to change the background color or appearance of an element.

Common properties include:

- `background-color`
- `background-image`
- `background-size`
- `background-position`

**Example:**

```html
<div class="card">
    <h2>Welcome</h2>
</div>
```

```css
.card {
    background-color: lightblue;
    padding: 20px;
}
```

### 2.3 Spacing Classes

Spacing classes help us control the space inside and outside elements.

The two main properties are:

- `margin` – Creates space outside an element.
- `padding` – Creates space inside an element.

**Example:**

```html
<div class="box">
    Hello World
</div>
```

```css
.box {
    margin: 20px;
    padding: 15px;
    background-color: lightgray;
}
```

### 2.4 Button Styling

Button classes are used to make buttons look attractive and consistent.

We can change their background color, text color, size, border, and other properties.

**Example:**

```html
<button class="btn">Click Me</button>
```

```css
.btn {
    background-color: blue;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}
```

### 2.5 Border Styling

Border classes are used to add outlines around elements.

Common properties include:

- `border-width`
- `border-style`
- `border-color`
- `border-radius`

**Example:**

```html
<div class="box">
    Sample Box
</div>
```

```css
.box {
    border: 2px solid black;
    border-radius: 10px;
    padding: 20px;
}
```

### 2.6 Display and Layout Styling

Display and layout properties help us arrange elements on a webpage.

Some commonly used properties are:

- `display: flex` – Arranges elements using Flexbox.
- `display: grid` – Arranges elements using CSS Grid.
- `display: none` – Hides an element and removes it from the layout.
- `display: block` – Makes an element behave like a block element.
- `display: inline-block` – Allows elements to stay in the same line while supporting width and height.

**Example:**

```html
<div class="items">
    <div>Item 1</div>
    <div>Item 2</div>
    <div>Item 3</div>
</div>
```

```css
.items {
    display: flex;
    gap: 15px;
}
```

### 2.7 Hover Effects

Hover effects are used to change the appearance of an element when the mouse pointer moves over it.

They are commonly used for buttons, links, and navigation menus.

**Example:**

```html
<button class="btn">Submit</button>
```

```css
.btn {
    background-color: blue;
    color: white;
    padding: 10px 20px;
    border: none;
}

.btn:hover {
    background-color: darkblue;
}
```

When the user moves the mouse over the button, its background color changes.

## 3. Commonly Used Styling Class Names

The following are some common class names developers use while styling websites.

| Class Name | Purpose |
|---|---|
| `text-center` | Centers the text. |
| `text-bold` | Makes text bold. |
| `text-muted` | Displays less prominent text. |
| `bg-primary` | Applies a primary background color. |
| `bg-light` | Applies a light background. |
| `btn` | Styles a button. |
| `btn-primary` | Styles a primary button. |
| `card` | Styles a content card. |
| `rounded` | Adds rounded corners. |
| `shadow` | Adds a shadow effect. |
| `d-flex` | Applies Flexbox display. |
| `hidden` | Hides an element. |

These are common naming conventions, not built-in CSS classes. Developers or CSS frameworks such as Bootstrap define their actual styles.

## 4. Conclusion

CSS styling classes make it easier to control the appearance of a webpage. They help us apply consistent styles to text, backgrounds, buttons, borders, and layouts.

By creating reusable classes, we can avoid repeating CSS code and make our websites easier to maintain.
