---
title: JavaScript-DOM
type: cheatsheet
tags:
  - 速查
  - 语言/JavaScript
---

# JavaScript-DOM

> [!note] 版本说明
> DOM（文档对象模型）让 JS 操作网页元素。这是 JS 在浏览器里最核心的用途。

## 获取元素

> [!example]+ 最常用写法
> ```js
> document.getElementById("id");              // 按 id 取单个
> document.querySelector(".class");          // CSS 选择器，取第一个
> document.querySelectorAll("div");          // 取所有，返回 NodeList
> ```

**用途**：找到要操作的页面元素。

**易错点**：
- `querySelector` 只返回**第一个**匹配；要全部用 `querySelectorAll`。
- `querySelector` 返回 `null` 表示没找到，操作前要判空。

**版本/平台**：浏览器 DOM。

**来源**：MDN · Document.querySelector（https://developer.mozilla.org/zh-CN/docs/Web/API/Document/querySelector ），2026-10-25 访问。

## 修改内容与样式

> [!example]+ 最常用写法
> ```js
> const el = document.querySelector("#box");
> el.textContent = "新文字";          // 改文本（安全，推荐）
> el.innerHTML = "<b>加粗</b>";       // 改 HTML（注意 XSS）
> el.style.color = "red";             // 改样式
> el.classList.add("active");         // 加 class
> el.classList.remove("active");      // 删 class
> el.classList.toggle("active");      // 切换 class
> ```

**用途**：改元素的文字、HTML、样式和 class。

**易错点**：
- 纯文本用 `textContent`；`innerHTML` 拼接用户输入有 **XSS 风险**。
- 改样式优先操作 class（`classList`），别一个个写内联 `style`。

**版本/平台**：浏览器 DOM。

**来源**：MDN · Element（https://developer.mozilla.org/zh-CN/docs/Web/API/Element ），2026-10-25 访问。

## 创建与增删元素

> [!example]+ 最常用写法
> ```js
> const li = document.createElement("li");  // 创建
> li.textContent = "新项";
> document.querySelector("ul").appendChild(li);   // 追加
> li.remove();                               // 删除自身
> ```

**用途**：动态创建、添加、删除页面元素。

**易错点**：创建元素后要 `appendChild`（或 `append`）才会出现在页面上。

**版本/平台**：浏览器 DOM。

**来源**：MDN · document.createElement（https://developer.mozilla.org/zh-CN/docs/Web/API/Document/createElement ），2026-10-25 访问。

## 事件监听

> [!example]+ 最常用写法
> ```js
> const btn = document.querySelector("button");
> btn.addEventListener("click", () => {
>     console.log("被点击了");
> });
> ```

**用途**：给元素绑定事件（点击、输入等）。

**易错点**：
- 事件名不带 `on` 前缀（是 `"click"` 不是 `"onclick"`）。
- 脚本要放在元素之后，或用 `DOMContentLoaded` 包裹，否则元素还没加载就找不到。

**版本/平台**：浏览器 DOM。

**来源**：MDN · addEventListener（https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/addEventListener ），2026-10-25 访问。

## 相关链接

- [[JavaScript-基础语法]]
- [[JavaScript-对象与数组]]
- [[HTML-CSS-常用标签]]
