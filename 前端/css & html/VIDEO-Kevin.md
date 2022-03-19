[TOC]

[Youtube-Kevin powell]()

# 1. HTML & CSS Core Concepts

## 1.1 CSS Specificity

参考：[CSS specificity explained](https://www.youtube.com/watch?v=c0kfcP_nD9E&list=PL4-IK0AVhVjP27yZLwW-gkPggRps0CCnP)。

工具：[specificity calculator](https://specificity.keegan.st/)，

- [x] inline styles > IDs > classes|pseudo classes|attributes > elements|pseudo elements
- [x] (internal - external) the last rule always wins

```html
>>>> depends on the order of definition (cascading)
internal win
<style>
  body { }
</style>
<link rel="stylesheet" href="style.css">

external win
<link rel="stylesheet" href="style.css">
<style>
  body { }
</style>
```

```html
>>>> more specific
div p { // win }
p { // lose }
```

- [x] a thousand `element` will still lose against one `class`

```scss
// win
.class-for-p {}

// 21-element still lose
p p p p p p p p p p p p p p p p p p p p p {}
```

****

## 1.2 @Media

参考：[Tutorial: Learn how to use CSS Media Queries in less than 5 minutes](youtube.com/watch?v=2KL-z9A56SQ&list=PL4-IK0AVhVjP27yZLwW-gkPggRps0CCnP&index=3).

- [x] `@media` should be put at last (the last rule always wins)

- [x] use `min-width` in mobile, use `max-width` in desktop.

```scss
p {
  // some css
}

// use min-width for mobile first
@media(min-width: 600px) {
  p { 
    // some css for 600px
  }
}

@media(min-width: 800px) {
  p {
    // some css when width is changed to 800px
  }
}

@media(max-width: 800px) {
  // use max-width for desktop first
}
```

- [ ] `@media(orientation: landscape|portrait){ }`
- [ ] `@media screen|print and (...){ }`

****

## 1.3 CSS Positioning

[CSS Positioning: Positiona absolute and relative explained](https://www.youtube.com/watch?v=P6UgYq3J3Qs&list=PL4-IK0AVhVjP27yZLwW-gkPggRps0CCnP&index=3)

- [x] 1. position `absolute` will set the position upon the closest `relative` parent (`body` will be the root)

- [x] 2. use `top bottom left right` can set the size of the element

```scss
// the size will show a half of the total "relative" parent 
.child {
  top: 0;
  bottom: 0;
  left: 0;
  right: 50%; // 50em, 50px
}
```

- [x] 3. :exclamation: when the `z-index` doesn't work, remember to set the `position` for that specific element

```scss
.parent {
  position: relative;
}

.parent .child {
  position: absolute; // this may overlay on the p
  z-index: -1; // set this element a background
}

.parent p {
  position: relative; // z-index won't work without position set
  z-index: 10;
}
```

****

## 1.4 em and rem

参考：[CSS em and rem explained](https://www.youtube.com/watch?v=_-aDOAMmDHI&list=PL4-IK0AVhVjP27yZLwW-gkPggRps0CCnP&index=4)。

- [x] 1. font-size: `em` depends on the direct father `font-size`，`rem` depends on the root `font-size` (generally the font-size of `html` element)。
- [x] 2. Except font-size properties: when use `em` to set the not-font-size properties (such as margin or padding), `em` depends on the font-size of itself, not its father's font-size. But `rem` always depends on the `root font-size`

- [x] use `::root` or `html` to set the root font-size

```scss
::root {
  font-size: 10px;
}

html {
  font-size: 10px;
}
```

:exclamation: using `em` to set properties **responsive** (like padding), because use `em` will depends on its own font-size, so the padding will responsively scale when the font-size change. But use `rem` to set properties like margin, because sometime margin should not depends on the element itself but a absolutely fixed spacing.

****

## 1.5 Keep the code DRY

参考：[Improve your CSS by Keepin' it DRY](https://www.youtube.com/watch?v=0px6YH-cauQ&list=PL4-IK0AVhVjP27yZLwW-gkPggRps0CCnP&index=5)。

DON'T REPEAT YOURSELF!

****

## 1.6 vh, vw, vmin, vmax

参考：[CSS Units: vh, vw, vmin, vmax](https://www.youtube.com/watch?v=IWFqGsXxJ1E&list=PL4-IK0AVhVjP27yZLwW-gkPggRps0CCnP&index=6)。

`vh` means `Viewport Height` , and will always match the size of the viewport height.

`vw` means `Viewport Width` 。

`vmin = Math.min(vh, vw)` 。

`vmax = Math.max(vh, vw)` 。

:exclamation: percentage `%` is always based on the parent element. While vh and vw  will always match the viewport.

****

## 1.7 outline & outline-offset

参考：[CSS Tutorial: Outline and Outline Offset](https://www.youtube.com/watch?v=OmfgB1vGd88&list=PL4-IK0AVhVjP27yZLwW-gkPggRps0CCnP&index=7)

​	`outline` is a lot like the `border` property but it has a few big differences.

1. `border-top` but no outline-top

```scss
// border can be splited to top/right/bottom/left
.example {
  border: 1px solid black;
  border-top: 2px;
}

// outline cannot be splited
.example {
  outline: 1px solid red;
  
  // set the gap of the border & outline,
  // also can be nagetive(inside outline)
  outline-offset: -10px;
}

```

2. `outline` will not be counted to the size of element (it won't occupy places)
3. `outline` needs to be specified both in the element and the pseudo class like `:hover` 。

```scss
.button {
  outline: 3px solid steelblue;
}

.button:hover {
  outline: 3px solid steelblue; // specify again
  outline-offset: 3px;
}
```

****

## 1.8 transition

`ease-in` : start slowly and fasten the speed.

- [x] set the `transition-timing-function` and `check` on the google browser, you can find an effect you want.

```scss
// use , to set multiple properties
.exa {
  transition: background 1s ease-in,
    transform .5s ease-out 1s;
}
```

****

## 1.9 selectors

参考：[Step up your CSS game using these selectors and combinators](https://www.youtube.com/watch?v=Bcr70LIJcOk&list=PL4-IK0AVhVjP27yZLwW-gkPggRps0CCnP&index=9)。

`*` ：universal selector

` ` ：children selector

`>` ：direct children selector

`+` ：adjacent-sibling selector

`~` ：general-sibling selector

`[]` ：attribute selector