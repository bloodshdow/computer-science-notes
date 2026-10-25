---
title: Lua-函数与模块
type: cheatsheet
tags:
  - 速查
  - 语言/Lua
---

# Lua-函数与模块

> [!note] 版本说明
> 基于 Lua 5.4。Lua 函数是一等公民，支持多返回值、可变参数；模块用 `require` 加载。

## 函数定义

> [!example]+ 最常用写法
> ```lua
> local function add(a, b)
>     return a + b
> end
>
> add(1, 2)    -- 3
> ```

**用途**：`function` 定义，`local` 声明为局部函数。

**易错点**：函数定义前也要 `local`（否则成全局）；`end` 结尾。

**版本/平台**：Lua 5.4。

**来源**：Lua 官方手册 · Functions（https://www.lua.org/manual/5.4/manual.html#3.4.11 ），2026-10-25 访问。

## 多返回值

> [!example]+ 最常用写法
> ```lua
> local function minmax(a, b)
>     if a < b then return a, b else return b, a end
> end
>
> local lo, hi = minmax(3, 7)   -- lo=3, hi=7
> ```

**用途**：Lua 函数可以返回**多个值**，这是它区别于 C/Java 的特色。

**易错点**：
- 接收多返回值要对应多个变量。
- 只想取第一个值，多余返回值会被丢弃。

**版本/平台**：Lua 5.4。

**来源**：Lua 官方手册 · return（https://www.lua.org/manual/5.4/manual.html#3.3.4 ），2026-10-25 访问。

## 可变参数 ...

> [!example]+ 最常用写法
> ```lua
> local function sum(...)
>     local args = {...}        -- 收集所有参数成表
>     local total = 0
>     for _, v in ipairs(args) do
>         total = total + v
>     end
>     return total
> end
>
> sum(1, 2, 3)    -- 6
> ```

**用途**：`...` 收集可变数量的参数。

**易错点**：`{...}` 把可变参数包成 table，配合 `ipairs` 遍历。

**版本/平台**：Lua 5.4。

**来源**：Lua 官方手册 · Vararg（https://www.lua.org/manual/5.4/manual.html#3.4.11 ），2026-10-25 访问。

## 模块与 require

> [!example]+ 最常用写法
> ```lua
> -- 文件 mymodule.lua
> local M = {}
> function M.sayHi()
>     print("hi")
> end
> return M
>
> -- 使用方
> local mod = require("mymodule")   -- 加载模块（不带 .lua）
> mod.sayHi()
> ```

**用途**：把一个文件封装成模块，别的文件 `require` 引入。

**易错点**：
- `require("模块名")` **不带** `.lua` 后缀。
- 模块文件最后要 `return` 导出的表，习惯用局部表 `M`。

**版本/平台**：Lua 5.4。

**来源**：Lua 官方手册 · require（https://www.lua.org/manual/5.4/manual.html#pdf-require ），2026-10-25 访问。

## 相关链接

- [[Lua-表]]
- [[Lua-基础语法]]
- [[Lua-游戏插件实践]]
