---
title: HTML-CSS-常用标签
type: cheatsheet
tags:
  - 速查
  - 语言/HTML-CSS
  - HTML
---

# HTML-CSS-常用标签

> [!note] 版本说明
> 基于 HTML5。CSS 相关见 [[HTML-CSS-盒模型与选择器]]。

## 页面基本结构

> [!example]+ 最常用写法
> ```html
> <!DOCTYPE html>
> <html lang="zh-CN">
> <head>
>     <meta charset="UTF-8">
>     <title>页面标题</title>
> </head>
> <body>
>     <!-- 页面内容 -->
> </body>
> </html>
> ```

**用途**：一个网页的最小骨架。

**易错点**：
- `<!DOCTYPE html>` 声明是 HTML5，放最前面。
- `<meta charset="UTF-8">` 保证中文不乱码。
- `<title>` 是浏览器标签页显示的标题，不是页面正文。

**版本/平台**：HTML5。

**来源**：MDN · HTML 基础（https://developer.mozilla.org/zh-CN/docs/Learn/HTML ），2026-10-25 访问。

## 标题与段落

> [!example]+ 最常用写法
> ```html
> <h1>一级标题</h1>
> <h2>二级标题</h2>
> <p>这是一个段落。</p>
> ```

**用途**：`<h1>`~`<h6>` 是标题，`<p>` 是段落。

**易错点**：标题是结构语义，不是用来调字号的；一个页面建议只有一个 `<h1>`。

**版本/平台**：HTML5。

**来源**：MDN · Heading elements（https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Heading_Elements ），2026-10-25 访问。

## 链接

> [!example]+ 最常用写法
> ```html
> <a href="https://example.com">链接文字</a>
> <a href="page.html">站内链接</a>
> <a href="#section">页内锚点</a>
> <a href="https://example.com" target="_blank">新窗口打开</a>
> ```

**用途**：超链接跳转。

**易错点**：`target="_blank"` 新窗口打开时建议加 `rel="noopener"` 防安全风险。

**版本/平台**：HTML5。

**来源**：MDN · a（https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/a ），2026-10-25 访问。

## 图片

> [!example]+ 最常用写法
> ```html
> <img src="photo.jpg" alt="照片描述">
> ```

**用途**：插入图片。`src` 是地址，`alt` 是加载失败时的替代文字（也用于无障碍）。

**易错点**：`alt` 不要省略，对 SEO 和无障碍很重要；`<img>` 是自闭合标签。

**版本/平台**：HTML5。

**来源**：MDN · img（https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/img ），2026-10-25 访问。

## 列表

> [!example]+ 最常用写法
> ```html
> <ul>                    <!-- 无序列表 -->
>     <li>项目 1</li>
>     <li>项目 2</li>
> </ul>
> <ol>                    <!-- 有序列表 -->
>     <li>第一步</li>
>     <li>第二步</li>
> </ol>
> ```

**用途**：`<ul>` 无序列表，`<ol>` 有序列表，`<li>` 列表项。

**易错点**：`<li>` 必须放在 `<ul>` 或 `<ol>` 里，不能单独出现。

**版本/平台**：HTML5。

**来源**：MDN · ul / ol（https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/ul ），2026-10-25 访问。

## 区块与行内

> [!example]+ 最常用写法
> ```html
> <div>块级容器</div>
> <span>行内容器</span>
> ```

**用途**：`<div>` 是块级元素（占整行），`<span>` 是行内元素（不换行），常用于配合 CSS 布局。

**易错点**：`div` 和 `span` 本身无语义，只是布局容器；有语义的场景优先用 `header`/`nav`/`section`/`article` 等。

**版本/平台**：HTML5。

**来源**：MDN · div / span（https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/div ），2026-10-25 访问。

## 语义化标签

> [!example]+ 最常用写法
> ```html
> <header>页头</header>
> <nav>导航</nav>
> <main>主内容</main>
> <section>区块</section>
> <article>文章</article>
> <footer>页脚</footer>
> ```

**用途**：用有语义的标签描述页面结构，利于 SEO 和无障碍。

**易错点**：语义标签和 `<div>` 显示效果一样，区别在"含义"；不要为了样式滥用。

**版本/平台**：HTML5。

**来源**：MDN · HTML 结构（https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Introduction_to_HTML ），2026-10-25 访问。

## 相关链接

- [[HTML-CSS-表单]]
- [[HTML-CSS-盒模型与选择器]]
