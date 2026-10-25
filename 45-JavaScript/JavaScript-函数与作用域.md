---
title: JavaScript-函数与作用域
type: cheatsheet
tags:
  - 速查
  - 语言/JavaScript
---

# JavaScript-函数与作用域

> [!note] 版本说明
> 基于 ES6+。函数是 JS 一等公民，箭头函数是现代主流写法。

## 函数定义

> [!example]+ 最常用写法
> ```js
> function add(a, b) {          // 函数声明
>     return a + b;
> }
>
> const add2 = function(a, b) { // 函数表达式
>     return a + b;
> };
>
> const add3 = (a, b) => a + b; // 箭头函数（最简洁）
> ```

**用途**：三种写法，箭头函数是现代最常用的简洁写法。

**易错点**：
- 箭头函数单行可省略 `return` 和大括号（`(a,b) => a+b`）。
- 箭头函数的 `this` 继承外层（和普通函数不同，见 [[JavaScript-异步]]）。

**版本/平台**：ES6+。

**来源**：MDN · Functions（https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Functions ），2026-10-25 访问。

## 默认参数与剩余参数

> [!example]+ 最常用写法
> ```js
> function greet(name = "world") {   // 默认参数
>     return `hello ${name}`;
> }
>
> function sum(...nums) {            // 剩余参数，收集成数组
>     return nums.reduce((a, b) => a + b, 0);
> }
> sum(1, 2, 3);   // 6
> ```

**用途**：参数给默认值，`...` 收集多余参数成数组。

**易错点**：剩余参数 `...nums` 必须是**最后一个**参数，且是真正的数组（不像老 `arguments` 是类数组）。

**版本/平台**：ES6+。

**来源**：MDN · Rest parameters（https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/rest_parameters ），2026-10-25 访问。

## 作用域

> [!example]+ 最常用写法
> ```js
> let global = 1;            // 全局作用域
>
> function f() {
>     let local = 2;         // 函数作用域
>     if (true) {
>         let block = 3;     // 块级作用域（let/const 才有）
>     }
>     // block 这里访问不到
> }
> ```

**用途**：`let`/`const` 是块级作用域，`var` 是函数作用域（这是它被淘汰的原因之一）。

**易错点**：
- `let`/`const` 在 `{}` 块内声明，块外访问不到。
- `var` 会提升且无视块，容易出 bug，别用。

**版本/平台**：ES6+。

**来源**：MDN · Scope（https://developer.mozilla.org/zh-CN/docs/Glossary/Scope ），2026-10-25 访问。

## 高阶函数（map/filter/reduce）

> [!example]+ 最常用写法
> ```js
> const nums = [1, 2, 3, 4];
> nums.map(x => x * 2);            // [2,4,6,8]，映射
> nums.filter(x => x > 2);         // [3,4]，过滤
> nums.reduce((sum, x) => sum + x, 0);  // 10，累加
> ```

**用途**：数组最常用的三个方法，替代 for 循环，代码更清晰。

**易错点**：
- `map` 返回新数组（不改原数组），`filter` 也返回新数组。
- `reduce` 第二个参数是初始值，别漏。

**版本/平台**：ES6+。

**来源**：MDN · Array.prototype.map（https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map ），2026-10-25 访问。

## 相关链接

- [[JavaScript-基础语法]]
- [[JavaScript-对象与数组]]
- [[JavaScript-异步]]
