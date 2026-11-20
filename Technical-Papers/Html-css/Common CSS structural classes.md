# Common CSS Structural Classes

## 1. Introduction

CSS structural classes are commonly used to organize and style different parts of a webpage.

When building a website, we usually divide the page into different sections, such as a header, navigation bar, main content, sidebar, and footer.

We can use CSS classes to apply styles to these sections and maintain a consistent layout throughout the website.

## 2. Common Structural Classes

Some commonly used CSS class names are explained below.

### 2.1 Container

A container is used to group related elements together and control the width of the content.

It also helps keep the content properly aligned on the page.

```html
<div class="container">
    <h1>Welcome</h1>
    <p>This is the main content.</p>
</div>
```

```css
.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 20px;
}
```

### 2.2 Header

The header is usually placed at the top of a webpage.

It commonly contains the website logo, title, and other important information.

```html
<header class="header">
    <h1>My Website</h1>
</header>
```

```css
.header {
    background-color: lightblue;
    padding: 20px;
}
```

### 2.3 Navbar

A navbar (navigation bar) contains links that help users move between different pages or sections of a website.

```html
<nav class="navbar">
    <a href="#">Home</a>
    <a href="#">About</a>
    <a href="#">Contact</a>
</nav>
```

```css
.navbar {
    display: flex;
    gap: 20px;
    padding: 15px;
}
```

### 2.4 Main

The main section contains the primary content of the webpage.

It is generally used for information that is directly related to the purpose of the page.

```html
<main class="main">
    <h2>Main Content</h2>
    <p>This is the main section of the website.</p>
</main>
```

### 2.5 Sidebar

A sidebar is a section placed beside the main content.

It usually contains additional information, links, categories, or menus.

```html
<aside class="sidebar">
    <h3>Categories</h3>
    <p>Technology</p>
    <p>Education</p>
</aside>
```

### 2.6 Content

The content class is commonly used to group the information displayed inside a particular section.

```html
<div class="content">
    <h2>About Us</h2>
    <p>We build simple and useful websites.</p>
</div>
```

### 2.7 Footer

The footer is generally placed at the bottom of a webpage.

It commonly contains copyright information, contact details, and useful links.

```html
<footer class="footer">
    <p>Copyright 2026 My Website</p>
</footer>
```

## 3. Complete Example

The following example shows how these structural classes can be used together to create a simple webpage.

```html
<div class="container">

    <header class="header">
        <h1>My Website</h1>
    </header>

    <nav class="navbar">
        <a href="#">Home</a>
        <a href="#">About</a>
        <a href="#">Contact</a>
    </nav>

    <div class="layout">

        <main class="main">
            <h2>Main Content</h2>
            <p>Welcome to my website.</p>
        </main>

        <aside class="sidebar">
            <h3>Sidebar</h3>
            <p>Additional information.</p>
        </aside>

    </div>

    <footer class="footer">
        <p>Copyright 2026</p>
    </footer>

</div>
```

```css
.container {
    max-width: 1200px;
    margin: 0 auto;
}

.header {
    background: lightblue;
    padding: 20px;
}

.navbar {
    background: lightgray;
    padding: 15px;
    display: flex;
    gap: 20px;
}

.layout {
    display: flex;
    gap: 20px;
    padding: 20px 0;
}

.main {
    flex: 3;
    background: #eeeeee;
    padding: 20px;
}

.sidebar {
    flex: 1;
    background: #dddddd;
    padding: 20px;
}

.footer {
    background: lightblue;
    padding: 20px;
    text-align: center;
}
```

## 4. Important Points

- CSS class names are created by developers. They are not predefined HTML elements.
- We can give any valid class name to an HTML element.
- A class can be reused on multiple elements.
- We use a dot (`.`) before a class name when selecting it in CSS.
- Structural classes help organize code and make styles easier to maintain.

## 5. Conclusion

Common CSS structural classes help us divide a webpage into meaningful sections and style each section separately.

Classes such as `container`, `header`, `navbar`, `main`, `sidebar`, and `footer` are commonly used when developing websites.

Using these classes makes the HTML structure easier to understand and the CSS easier to manage.
