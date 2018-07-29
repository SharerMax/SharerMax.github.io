---
title: Sticky Footer
date: 2018-07-29 22:54:34
tags: Web,Footer
---

Sticky Footer 是一种网页效果：如果内容不够长时，页脚固定在浏览器底部；如果内容足够长，页脚固定在页面的最底部。

<!--more-->

## 1. 使用absolute

HTML
``` html
<body>
    <div class="wrapper">
        <div class="content">
        <div class="footer">
    </div>
</body>
```
CSS 
``` css
body {
    height: 100%;
    margin: 0;
}
.wrapper {
    position: relative;
    min-height: 100%;
}
.content {
    padding-bottom: 50px;
}
.footer {
    position: absolute;
    bottom: 0;
    height: 50px;
}
```

## 2. 使用margin-bottom 负值
HTML
```html
<body>
    <div class="wrapper">
        content
        <div class="push"></div>
    </div>
    <footer class="footer"></footer>
</body>
```
CSS
``` css
html, body {
    height: 100%;
    margin: 0;
}
.wrapper {
    min-height: 100%;

    /* Equal to height of footer */
    /* But also accounting for potential margin-bottom of last child */
    margin-bottom: -50px;
}
.footer,
.push {
    height: 50px;
}
```

## 3. 使用calc() 
HTML
```html
<body>
    <div class="content">
        content
    </div>
    <footer class="footer"></footer>
</body>
```
CSS
```css
.content {
    min-height: calc(100vh - 50px);
}
.footer {
    height: 50px;
}
```
<div class="tip">
假如content中的最后一个元素有 *margin-bottom* 属性，这将导致 *content* 的高增加，这是需要调整*calc(100vh - footerHeight - marginBottom)*
</div>

## 4. 使用 flex 布局
HTML
```html
<body>
    <div class="content">
        content
    </div>
    <footer class="footer"></footer>
</body>
```
CSS
```css
html, body {
    height: 100%;
}
body {
    display: flex;
    flex-direction: column;
}
.content {
    flex: 1 0 auto;
}
.footer {
    flex-shrink: 0;
}
```