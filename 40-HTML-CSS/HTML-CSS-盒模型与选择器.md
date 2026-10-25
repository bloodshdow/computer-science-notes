---
title: HTML-CSS-盒模型与选择器
type: cheatsheet
tags:
  - 速查
  - 语言/HTML-CSS
  - CSS
---

# HTML-CSS-盒模型与选择器

> [!note] 版本说明
> 基于 CSS3。CSS 的引入方式：`<link rel="stylesheet" href="style.css">`（外部，推荐）、`<style>`（内部）、`style="..."`（内联）。

## 选择器

> [!example]+ 最常用写法
> ```css
> p { color: red; }          /* 元素选择器：所有 p */
> .title { font-size: 20px; } /* 类选择器：class="title" */
> #header { }                /* ID 选择器：id="header" */
> a:hover { }                /* 伪类：鼠标悬停 */
> p, .title { }              /* 组合：逗号分隔多个 */
> ```

**用途**：选中要加样式的元素。

**易错点**：
- 类选择器是 `.`，ID 选择器是 `#`，别混。
- 类可重复用，ID 应唯一。
- 冒号 `:` 是伪类（如 `:hover`），别和 `::` 伪元素搞混。

**版本/平台**：CSS3。

**来源**：MDN · CSS selectors（https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_selectors ），2026-10-25 访问。

> [!note]- 进阶：后代与子代选择器
> ```css
> div p { }    /* 后代：div 内所有 p（含嵌套） */
> div > p { }  /* 子代：div 直接子元素 p */
> ```

## 盒模型

> [!example]+ 最常用写法
> ```css
> .box {
>     width: 200px;
>     padding: 10px;      /* 内边距 */
>     border: 1px solid #000;  /* 边框 */
>     margin: 20px;       /* 外边距 */
> }
> ```

**用途**：理解元素占位 = content + padding + border + margin。

**易错点**：
- `width` 默认只指内容区宽度，加 padding/border 后实际占位会变大。
- 用 `box-sizing: border-box` 让 `width` 包含 padding 和 border，布局更直观。

**版本/平台**：CSS3。

**来源**：MDN · CSS box model（https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_box_model ），2026-10-25 访问。

## box-sizing

> [!example]+ 最常用写法
> ```css
> * { box-sizing: border-box; }   /* 全局统一，推荐 */
> ```

**用途**：让 `width`/`height` 包含 padding 和 border，避免尺寸计算混乱。

**易错点**：很多 CSS 框架会默认设 `border-box`；自己写建议一开始就全局设。

**版本/平台**：CSS3。

**来源**：MDN · box-sizing（https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-sizing ），2026-10-25 访问。

## 常用文字与颜色样式

> [!example]+ 最常用写法
> ```css
> p {
>     color: #333;              /* 文字颜色 */
>     font-size: 16px;          /* 字号 */
>     font-weight: bold;        /* 加粗 */
>     text-align: center;       /* 对齐：left/center/right */
>     line-height: 1.5;         /* 行高 */
>     text-decoration: none;    /* 去下划线（常用于 a） */
> }
> ```

**用途**：文字外观与颜色。

**易错点**：颜色可用 `#hex`、`rgb()`、`rgba()`（带透明）；去掉链接下划线用 `text-decoration: none`。

**版本/平台**：CSS3。

**来源**：MDN · color / font（https://developer.mozilla.org/zh-CN/docs/Web/CSS/color ），2026-10-25 访问。

## 布局：display 基础

> [!example]+ 最常用写法
> ```css
> .a { display: block; }      /* 块级：占整行 */
> .b { display: inline; }     /* 行内：不换行 */
> .c { display: flex; }       /* 弹性布局（最常用） */
> .d { display: none; }       /* 隐藏，不占位 */
> ```

**用途**：控制元素显示方式和布局。现代布局主要用 `flex`（和 `grid`）。

**易错点**：
- `display: none` 彻底隐藏且不占位；只想占位隐藏用 `visibility: hidden`。
- 现代布局优先 `flex`/`grid`，别再用 `float` 做整体布局。

**版本/平台**：CSS3。

**来源**：MDN · display（https://developer.mozilla.org/zh-CN/docs/Web/CSS/display ），2026-10-25 访问。

## 布局：Flexbox

> [!example]+ 最常用写法
> ```css
> .container {
>     display: flex;
>     justify-content: center;   /* 主轴对齐：center/space-between */
>     align-items: center;       /* 交叉轴对齐 */
>     gap: 10px;                 /* 子项间距 */
> }
> ```

**用途**：一维弹性布局，水平/垂直居中、等分排列非常好用。

**易错点**：
- `justify-content` 控制主轴，`align-items` 控制交叉轴，方向随 `flex-direction` 变。
- 居中三件套常用：`display:flex + justify-content:center + align-items:center`。

**版本/平台**：CSS3。

**来源**：MDN · Flexbox（https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_flexible_box_layout ），2026-10-25 访问。

## 相关链接

- [[HTML-CSS-常用标签]]
- [[HTML-CSS-表单]]
