---
title: JS判断CSS属性可用性
date: 2018-08-18 23:50:47
tags: Web,JavaScript,CSS
---

Web开发中，因为浏览器的不同，CSS的属性支持情况是有不同的。有时候需要判断CSS属性的支持情况做出不一样的设计，或者需要polyfill这个不支持的属性，这时候就需要判断CSS的支持情况。

<!-- more -->

DOM元素中我们可以通过 [_DOM API_](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/style) 获取样式声明对象 [_CSSStyleDeclaration_](https://developer.mozilla.org/en-US/docs/Web/API/CSSStyleDeclaration)，获取的[_CSSStyleDeclaration_](https://developer.mozilla.org/en-US/docs/Web/API/CSSStyleDeclaration)为内联style的css设置属性。[_CSSStyleDeclaration_](https://developer.mozilla.org/en-US/docs/Web/API/CSSStyleDeclaration)有两个特点：
> 1. 如果我们设置了一个不支持的CSS属性，则CSSStyleDeclaration中也不会出现这个变量名。
> 2. 如果我们设置了一个支持的CSS属性，但是设置了一个不支持的值（如: sticky 定位），则CSSStyleDeclaration中对应的变量值还将保持为空值。

我们可以使用这两个特性来判断CSS属性的支持情况。如：

``` JavaScript
function cssSupport ({attr, value}) {
    let tempElement = document.createElement('div')
    if(attr in tempElement.style ) {
        tempElement.style[attr] = value
        return tempElement.style[attr] === value
    }
    return false
}
```