# Common HTML Head Meta Tags

## 1. Introduction

Meta tags are HTML elements used to provide information about a webpage. They are written inside the `<head>` section of an HTML document.

They help browsers understand how to display a webpage and provide information to search engines and other services.

Meta tags are not normally displayed directly on the webpage.

## 2. Common Meta Tags

### 2.1 Charset

The charset meta tag defines the character encoding used by the webpage.

It helps the browser display text and special characters correctly.

```html
<meta charset="UTF-8">
```

UTF-8 is commonly used because it supports many different languages and characters.

### 2.2 Viewport

The viewport meta tag helps websites adjust to different screen sizes, especially mobile devices.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

Here:

- `width=device-width` sets the viewport width to the device width.
- `initial-scale=1.0` sets the initial zoom level to 100%.

### 2.3 Description

The description meta tag provides a short summary of the webpage.

Search engines may use this description in their search results.

```html
<meta name="description" content="Learn HTML, CSS and JavaScript with simple examples.">
```

### 2.4 Keywords

The keywords meta tag contains words related to the webpage.

```html
<meta name="keywords" content="HTML, CSS, JavaScript, Web Development">
```

This tag is supported by HTML, but major search engines like Google do not use it for search rankings.

### 2.5 Author

The author meta tag specifies who created the webpage.

```html
<meta name="author" content="Manish Nalumachu">
```

### 2.6 Robots

The robots meta tag gives instructions to search engine crawlers about indexing and following links on a webpage.

```html
<meta name="robots" content="index, follow">
```

Here:

- `index` allows search engines to index the page.
- `follow` allows crawlers to follow links on the page.

Other commonly used values include `noindex` and `nofollow`.

### 2.7 Theme Color

The theme-color meta tag defines a preferred color for certain browser interface elements on supported devices.

```html
<meta name="theme-color" content="#ffffff">
```

### 2.8 Refresh

The refresh meta tag can automatically reload a webpage or redirect users after a specified number of seconds.

```html
<meta http-equiv="refresh" content="30">
```

This example reloads the webpage after 30 seconds.

It can also be used for redirects, although redirects are generally better handled by the server.

## 3. Common Head Tags Other Than Meta Tags

The `<head>` section also contains other important HTML elements.

### Title

The title tag defines the title of the webpage. It is commonly displayed in the browser tab.

```html
<title>My Website</title>
```

### Favicon

A favicon is the small icon displayed in the browser tab.

```html
<link rel="icon" href="favicon.ico">
```

### External CSS

The link tag is used to connect an external CSS file to the HTML document.

```html
<link rel="stylesheet" href="style.css">
```

### External JavaScript

The script tag is used to connect an external JavaScript file.

```html
<script src="script.js" defer></script>
```

The `defer` attribute tells the browser to execute the script after the HTML document has been parsed.

## 4. Complete Example

Here is an example of a commonly used HTML head section:

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">

    <meta name="viewport"
          content="width=device-width, initial-scale=1.0">

    <meta name="description"
          content="A simple website for learning web development.">

    <meta name="author"
          content="Manish Nalumachu">

    <meta name="robots"
          content="index, follow">

    <meta name="theme-color"
          content="#ffffff">

    <title>My Website</title>

    <link rel="icon" href="favicon.ico">

    <link rel="stylesheet" href="style.css">

    <script src="script.js" defer></script>
</head>

<body>
    <h1>Welcome to My Website</h1>
</body>

</html>
```

## 5. Conclusion

Meta tags provide important information about an HTML webpage. They help browsers handle character encoding, control mobile layouts, and provide information to search engines.

The `<head>` section also contains elements such as title, favicon, CSS links, and JavaScript references.

Understanding these tags helps us create properly structured HTML documents.
