---
title: JavaScript-对象与数组
type: cheatsheet
tags:
  - 速查
  - 语言/JavaScript
---

# JavaScript-对象与数组

> [!note] 版本说明
> 基于 ES6+。对象和数组是 JS 最常用的两种复合类型，是操作数据的基础。

## 对象

> [!example]+ 最常用写法
> ```js
> const person = {
>     name: "Alice",
>     age: 20,
>     sayHi() { return "hi"; }   // 方法简写
> };
>
> person.name;          // "Alice"，点访问
> person["age"];        // 20，方括号访问（键可动态）
> person.name = "Bob";  // 修改
> person.city = "BJ";   // 新增属性
> delete person.age;    // 删除属性
> ```

**用途**：键值对集合，JS 里几乎一切（除了基本类型）都是对象。

**易错点**：
- 点 `.` 访问要求键是合法标识符；动态键或含特殊字符用 `[]`。
- 访问不存在的属性返回 `undefined`（不报错）。

**版本/平台**：ES6+。

**来源**：MDN · Object（https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object ），2026-10-25 访问。

## 解构赋值

> [!example]+ 最常用写法
> ```js
> const { name, age } = person;        // 对象解构
> const [a, b] = [1, 2];               // 数组解构
> const { name: n } = person;          // 重命名
> ```

**用途**：一次性取出对象的多个属性或数组元素，代码简洁。

**易错点**：对象解构用 `{}`，数组解构用 `[]`，别混。

**版本/平台**：ES6+。

**来源**：MDN · Destructuring（https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment ），2026-10-25 访问。

## 数组常用方法

> [!example]+ 最常用写法
> ```js
> const arr = [1, 2, 3];
> arr.push(4);         // 末尾加，返回新长度
> arr.pop();           // 删末尾，返回被删元素
> arr.shift();         // 删开头
> arr.unshift(0);      // 开头加
> arr.includes(2);     // 是否包含
> arr.indexOf(2);      // 找下标，找不到 -1
> arr.slice(0, 2);     // 切片，不改原数组
> arr.splice(1, 1);    // 从下标1删1个（改原数组）
> arr.join("-");       // "1-2-3"，拼成字符串
> ```

**用途**：数组增删查。配合 `map/filter/reduce`（见 [[JavaScript-函数与作用域]]）覆盖绝大多数场景。

**易错点**：
- `slice` 不改原数组（返回新数组），`splice` 改原数组。
- `includes` 比 `indexOf !== -1` 更直观，判断"是否包含"优先用它。

**版本/平台**：ES6+。

**来源**：MDN · Array（https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array ），2026-10-25 访问。

## 展开运算符 ...

> [!example]+ 最常用写法
> ```js
> const a = [1, 2];
> const b = [...a, 3, 4];     // [1,2,3,4]，展开数组
> const c = { ...person, age: 30 };  // 浅拷贝并覆盖 age
> ```

**用途**：展开数组/对象，常用于合并、浅拷贝、传参。

**易错点**：`...` 展开对象是**浅拷贝**，嵌套对象仍共享引用。

**版本/平台**：ES6+。

**来源**：MDN · Spread syntax（https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Spread_syntax ），2026-10-25 访问。

## 相关链接

- [[JavaScript-基础语法]]
- [[JavaScript-函数与作用域]]
- [[JavaScript-DOM]]
