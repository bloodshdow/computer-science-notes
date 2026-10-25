---
title: Lua-基础语法
type: cheatsheet
tags:
  - 速查
  - 语言/Lua
---

# Lua-基础语法

> [!note] 版本说明
> 基于 Lua 5.4（主流稳定版）。Lua 是轻量脚本语言，大量用于游戏引擎（Roblox、Love2D、魔兽世界插件等）和配置/扩展。语法极简。

## 第一个程序与注释

> [!example]+ 最常用写法
> ```lua
> print("Hello, Lua")
>
> -- 这是单行注释
> --[[
> 这是多行注释
> ]]
> ```

**用途**：`print` 输出，`--` 注释。

**易错点**：Lua 注释用 `--`，不是 `//` 或 `#`。多行注释是 `--[[ ... ]]`。

**版本/平台**：Lua 5.4。

**来源**：Lua 官方手册（https://www.lua.org/manual/5.4/ ），2026-10-25 访问。

## 变量

> [!example]+ 最常用写法
> ```lua
> local x = 10          -- 局部变量（推荐，加 local）
> x = 20                -- 不加 local 是全局变量
> local s = "hi"        -- 字符串
> local b = true        -- 布尔
> local n = nil         -- nil 表示空/不存在
> ```

**用途**：Lua 是动态类型，变量用 `local` 声明为局部变量。

**易错点**：
- **务必加 `local`**，否则变量变成全局的，容易互相污染（Lua 最著名的坑）。
- `nil` 是唯一的"空"值，未赋值的变量默认是 `nil`。

**版本/平台**：Lua 5.4。

**来源**：Lua 官方手册 · Variables（https://www.lua.org/manual/5.4/manual.html#3.3.7 ），2026-10-25 访问。

## 数据类型

> [!example]+ 最常用写法
> ```lua
> 1, 2.5           -- number（整数小数统一）
> "hi"             -- string
> true, false      -- boolean
> nil              -- nil（空）
> {1, 2, 3}        -- table（唯一的复合类型，见 [[Lua-表]]）
> type(x)          -- 查看类型
> ```

**用途**：Lua 只有 8 种类型，最特殊的是 **table** 承担了数组、字典、对象、模块等一切角色。

**易错点**：
- 数字只有 `number` 一种（不区分 int/float）。
- `0` 和空字符串 `""` 在 Lua 里都是**真值**，只有 `nil` 和 `false` 是假（和 C 不同！）。

**版本/平台**：Lua 5.4。

**来源**：Lua 官方手册 · Types（https://www.lua.org/manual/5.4/manual.html#2.1 ），2026-10-25 访问。

## 运算符

> [!example]+ 最常用写法
> ```lua
> 7 / 2       -- 3.5，除法
> 7 // 2      -- 3，整除（5.3+）
> 7 % 2       -- 1，取余
> 2 ^ 3       -- 8，幂运算（注意是 ^ 不是 **）
> "a" .. "b"  -- "ab"，字符串拼接用 ..
> #"hello"    -- 5，长度
> 1 == 1      -- true
> 1 ~= 2      -- true，不等于是 ~=
> ```

**用途**：Lua 有和别的语言不同的运算符，要记牢。

**易错点**：
- **字符串拼接用 `..`**（不是 `+`），这是 Lua 特有。
- **不等于用 `~=`**（不是 `!=`）。
- **幂用 `^`**（不是 `**`）。

**版本/平台**：Lua 5.4。

**来源**：Lua 官方手册 · Expressions（https://www.lua.org/manual/5.4/manual.html#3.4 ），2026-10-25 访问。

## 控制流

> [!example]+ 最常用写法
> ```lua
> if x > 0 then
>     print("正")
> elseif x == 0 then      -- 注意是 elseif（连写）
>     print("零")
> else
>     print("负")
> end
>
> for i = 1, 10 do        -- 1 到 10（含 10）
>     print(i)
> end
>
> while cond do
> end
> ```

**用途**：Lua 用 `then/end` 表示代码块（不是大括号）。

**易错点**：
- 分支是 `elseif`（**连写**，不是 else if）。
- 每个块以 `end` 结尾，`if` 要配 `then`。
- `for i = 1, 10` 是**闭区间**，包含 10。

**版本/平台**：Lua 5.4。

**来源**：Lua 官方手册 · Control structures（https://www.lua.org/manual/5.4/manual.html#3.3.4 ），2026-10-25 访问。

## 相关链接

- [[Lua-表]]
- [[Lua-函数与模块]]
- [[Lua-游戏插件实践]]
