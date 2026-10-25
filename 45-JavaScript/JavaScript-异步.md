---
title: JavaScript-异步
type: cheatsheet
tags:
  - 速查
  - 语言/JavaScript
---

# JavaScript-异步

> [!note] 版本说明
> 基于 ES6+。异步是 JS 的核心特性（网络请求、定时器、读文件都靠它）。现代写法用 async/await。

## 为什么需要异步

### 逻辑

JS 是**单线程**的。如果网络请求要等 1 秒才返回，同步写法会卡住整个页面 1 秒。

异步就是：**发起请求后不干等，先去做别的，结果回来了再回头处理**。

## Promise

> [!example]+ 最常用写法
> ```js
> fetch("https://api.example.com/data")   // 发起请求，返回 Promise
>     .then(res => res.json())            // 结果回来了处理
>     .then(data => console.log(data))
>     .catch(err => console.error(err));  // 出错处理
> ```

**用途**：Promise 表示"未来会完成的结果"，`then` 处理成功、`catch` 处理失败。

**易错点**：`.catch` 要记得写，否则出错时静默失败，很难排查。

**版本/平台**：ES6+。

**来源**：MDN · Promise（https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise ），2026-10-25 访问。

## async / await（现代主流写法）

> [!example]+ 最常用写法
> ```js
> async function getData() {
>     try {
>         const res = await fetch("https://api.example.com/data");
>         const data = await res.json();
>         console.log(data);
>     } catch (err) {
>         console.error(err);
>     }
> }
> ```

**用途**：`async/await` 让异步代码看起来像同步，可读性最好，是现在推荐写法。

**易错点**：
- `await` 只能在 `async` 函数里用。
- `await` 的报错用 `try/catch` 捕获（等价于 Promise 的 `.catch`）。
- 忘记 `await` 会拿到 Promise 对象而不是结果。

**版本/平台**：ES2017+。

**来源**：MDN · async function（https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/async_function ），2026-10-25 访问。

## 常见异步场景

> [!example]+ 最常用写法
> ```js
> setTimeout(() => { }, 1000);   // 1 秒后执行（定时器）
> setInterval(() => { }, 1000);  // 每 1 秒执行一次
>
> // fetch 发请求
> const res = await fetch(url);
> const data = await res.json();  // 解析 JSON
> ```

**用途**：定时器 `setTimeout`/`setInterval`，网络请求 `fetch`。

**易错点**：
- `fetch` 返回的 `res.json()` 也是异步，要 `await`。
- 检查 `res.ok` 判断请求是否成功（404 也会正常返回，不算抛错）。

**版本/平台**：ES6+ / 浏览器 & Node.js。

**来源**：MDN · fetch（https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API ），2026-10-25 访问。

## 相关链接

- [[JavaScript-函数与作用域]]
- [[JavaScript-DOM]]
