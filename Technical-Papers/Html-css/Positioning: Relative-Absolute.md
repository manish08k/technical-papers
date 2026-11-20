# CSS Positioning: Relative and Absolute

## 1. Introduction

CSS positioning is used to control where an HTML element appears on a webpage.

By default, elements are placed according to the normal document flow. But sometimes we need to move an element from its original position or place it at a specific location.

CSS provides different positioning values. Two commonly used values are `relative` and `absolute`.

## 2. Position Relative

The `position: relative` property allows us to move an element from its original position.

The element still keeps its original space in the webpage, even after moving.

We can use the following properties to control its position:

- `top`
- `bottom`
- `left`
- `right`

### Example

```html
<div class="box">
    Relative Box
</div>
```

```css
.box {
    position: relative;
    top: 20px;
    left: 30px;
    width: 150px;
    height: 100px;
    background-color: lightblue;
}
```

In this example:

- `position: relative` allows the element to move from its original position.
- `top: 20px` moves it 20 pixels down.
- `left: 30px` moves it 30 pixels to the right.

The element moves, but its original space is still reserved.

## 3. Position Absolute

The `position: absolute` property removes an element from the normal document flow.

It positions the element using the nearest ancestor that has a position other than `static`.

If no such ancestor exists, it uses the initial containing block, usually based on the viewport.

We can use `top`, `bottom`, `left`, and `right` to place the element.

### Example

```html
<div class="container">
    <div class="box">
        Absolute Box
    </div>
</div>
```

```css
.container {
    position: relative;
    width: 300px;
    height: 200px;
    background-color: lightgray;
}

.box {
    position: absolute;
    top: 20px;
    right: 20px;
    width: 100px;
    height: 80px;
    background-color: lightblue;
}
```

In this example:

- The container has `position: relative`.
- The box has `position: absolute`.
- `top: 20px` places the box 20 pixels from the top of the container.
- `right: 20px` places it 20 pixels from the right of the container.

The absolute element is positioned relative to the container instead of its original position in the document.

## 4. Difference Between Relative and Absolute

| Relative | Absolute |
|---|---|
| Moves from its original position. | Positions itself using its containing block. |
| Stays in the normal document flow. | Removed from the normal document flow. |
| Original space is reserved. | Original space is not reserved. |
| Can be used as a positioning reference for absolute children. | Usually positioned relative to the nearest positioned ancestor. |
| Does not overlap other elements unless moved over them. | Can overlap other elements. |

## 5. Practical Usage

Both positioning properties are useful when designing webpages.

**Relative positioning:**
- Moving an element slightly from its original location.
- Creating a positioning reference for child elements.
- Adjusting the placement of small UI elements.

**Absolute positioning:**
- Placing notification badges on icons.
- Positioning text over images.
- Creating dropdown menus.
- Placing close buttons inside cards.

## 6. Conclusion

Relative and absolute positioning help us control where elements appear on a webpage.

Relative positioning moves an element from its original position while keeping its space reserved. Absolute positioning removes the element from the normal document flow and places it relative to its nearest positioned ancestor.

Understanding these two properties makes it easier to create flexible webpage layouts and position elements exactly where they are needed.
