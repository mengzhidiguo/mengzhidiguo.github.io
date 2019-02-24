---
title: Web Components
date: 2019-02-24 16:36:45
categories:
- html5
tags:
- service worker
- 博客
---

# Web Components

## Web Components 的四大主要技术

- Custom elements（自定义元素）：一组JavaScript API，允许您定义custom elements及其行为，然后可以在您的用户界面中按照需要使用它们。
- Shadow DOM（影子DOM）：一组JavaScript API，用于将封装的“影子”DOM树附加到元素（与主文档DOM分开呈现）并控制其关联的功能。通过这种方式，您可以保持元素的功能私有，这样它们就可以被脚本化和样式化，而不用担心与文档的其他部分发生冲突。
- HTML templates（HTML模板）：`<template>` 和 `<slot>` 元素使您可以编写不在呈现页面中显示的标记模板。然后它们可以作为自定义元素结构的基础被多次重用。
- HTML Imports（HTML导入）：一旦定义了自定义组件，最简单的重用它的方法就是使其定义细节保存在一个单独的文件中，然后使用导入机制将其导入到想要实际使用它的页面中。HTML 导入就是这样一种机制，尽管存在争议 — Mozilla 根本不同意这种方法，并打算在将来实现更合适的。

## 实现 Web Components 的基本方法

1. 使用 ECMAScript 2015 类语法创建一个类，来指定 web 组件的功能。
2. 使用 CustomElementRegistry.define() 方法注册您的新自定义元素 ，并向其传递要定义的元素名称、指定元素功能的类以及可选的，其所继承自的元素。
3. 如果需要的话，使用 Element.attachShadow() 方法将一个 shadow DOM 附加到自定义元素上。使用通常的 DOM 方法向 shadow DOM 中添加子元素、事件监听器等等。
4. 如果需要的话，使用 `<template>` 和 `<slot>` 方法定义一个 HTML 模板。再次使用常规 DOM 方法克隆模板并将其附加到您的shadow DOM 中。
5. 在页面任何您喜欢的位置使用自定义元素，就像使用常规 HTML 元素那样。

### Custom Elements

#### 两种形式

- Autonomous custom elements 是独立的元素，它不继承其他内建的HTML元素。你可以直接把它们写成HTML标签的形式，来在页面上使用。例如 `<popup-info>`，或者是 `document.createElement("popup-info")` 这样。
- Customized built-in elements 继承自基本的 HTML 元素。在创建时，你必须指定所需扩展的元素（正如上面例子所示），使用时，需要先写出基本的元素标签，并通过 is 属性指定 custom element 的名称。例如 `<p is="word-count">` , 或者 `document.createElement("p", { is: "word-count" })` 。

#### 实例

- Autonomous custom elements 实例: <https://github.com/mdn/web-components-examples/blob/master/popup-info-box-web-component/main.js>
- Customized built-in elements 实例： <https://github.com/mdn/web-components-examples/blob/master/expanding-list-web-component/main.js>

#### 生命周期函数

- `connectedCallback`：当 custom element 首次被插入文档 DOM 时，被调用。
- `disconnectedCallback`：当 custom element 从文档 DOM 中删除时，被调用。
- `adoptedCallback`：当 custom element 被移动到新的文档时，被调用。
- `attributeChangedCallback`: 当 custom element 增加、删除、修改自身属性时，被调用。

### Shadow DOM

#### 相关技术

- Shadow host： 一个常规 DOM节点，Shadow DOM会被添加到这个节点上。
- Shadow tree：Shadow DOM内部的DOM树。
- Shadow boundary：Shadow DOM结束的地方，也是常规 DOM开始的地方。
- Shadow root: Shadow tree的根节点。

## 相关框架上的实现

### angular

- angular 普通组件可以使用 shadow dom 的方式组装组件 <https://angular.cn/api/core/Component#encapsulation>
- angular elements 可以把组件导出为 web components <https://nitayneeman.com/posts/a-practical-guide-to-angular-elements/>