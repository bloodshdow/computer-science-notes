---
title: JavaScript-基础语法
type: cheatsheet
tags:
  - 速查
  - 语言/JavaScript
---

# JavaScript-基础语法

> [!note] 版本说明
> 基于现代 JavaScript（ES2022+）。JS 是网页端的脚本语言，也能通过 Node.js 在服务器/本地运行。动态类型、弱类型。

## 变量声明

> [!example]+ 最常用写法
> ```js
> let x = 10;          // 可变的变量（推荐）
> const y = 20;        // 常量，声明后不能改（推荐）
> // var 是老写法，有作用域问题，避免使用
> ```

**用途**：`let` 声明可变变量，`const` 声明常量，都推荐，别再用 `var`。

**易错点**：
- `const` 声明后不能重新赋值，但对象/数组内部可以改（`const arr = []; arr.push(1)` 合法）。
- 用 `var` 会有变量提升和函数作用域问题，现代代码统一用 `let`/`const`。

**版本/平台**：ES6+。

**来源**：MDN · let / const（https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/let ），2026-10-25 访问。

## 数据类型

> [!example]+ 最常用写法
> ```js
> let n = 10;             // number（整数小数不分）
> let s = "hi";           // string
> let b = true;           // boolean
> let arr = [1, 2, 3];    // array（数组）
> let obj = { a: 1 };     // object（对象）
> let nothing = null;     // 空值
> let u;                  // undefined（未定义）
> typeof x;               // 查看类型
> ```

**用途**：JS 是动态类型，变量类型可随时变，`typeof` 查类型。

**易错点**：
- `null` 是"显式空"，`undefined` 是"未赋值"，两者语义不同。
- `typeof null` 返回 `"object"`（历史遗留 bug，别被误导）。

**版本/平台**：ES6+。

**来源**：MDN · Data types（https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Data_structures ），2026-10-25 访问。

## 运算符与比较

> [!example]+ 最常用写法
> ```js
> 1 == "1"      // true，宽松相等（会类型转换）
> 1 === "1"     // false，严格相等（推荐用 ===）
> 1 != "1"      // false
> 1 !== "1"     // true
> ```

**用途**：比较时**优先用 `===` 和 `!==`**（严格相等，不类型转换）。

**易错点**：
- `==` 会做隐式类型转换，结果出人意料（如 `0 == ""` 为 true），是 bug 来源。
- 养成习惯：判断相等一律 `===`。

**版本/平台**：ES6+。

**来源**：MDN · Equality（https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Equality_comparisons_and_sameness ），2026-10-25 访问。

## 控制流

> [!example]+ 最常用写法
> ```js
> if (x > 0) { } else { }
> for (let i = 0; i < 10; i++) { }
> for (const item of arr) { }      // 遍历数组
> while (cond) { }
> ```

**用途**：分支和循环，语法类似 C/Java。

**易错点**：`for...of` 遍历数组值，`for...in` 遍历对象键（别混用）。

**版本/平台**：ES6+。

**来源**：MDN · Control flow（https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Control_flow_and_error_handling ），2026-10-25 访问。

## 模板字符串

> [!example]+ 最常用写法
> ```js
> let name = "Alice";
> let msg = `Hello ${name}`;   // 用反引号 + ${} 插值
> let multi = `多行
> 字符串`;
> ```

**用途**：反引号 `` ` `` 包裹，`${}` 插入变量，支持多行。

**易错点**：是反引号（键盘 1 左边的 `），不是单引号。

**版本/平台**：ES6+。

**来源**：MDN · Template literals（https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Template_literals ），2026-10-25 访问。

## 相关链接

- [[JavaScript-函数与作用域]]
- [[JavaScript-对象与数组]]
- [[JavaScript-DOM]]
