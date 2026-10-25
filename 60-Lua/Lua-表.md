---
title: Lua-表
type: cheatsheet
tags:
  - 速查
  - 语言/Lua
---

# Lua-表

> [!note] 版本说明
> 基于 Lua 5.4。table 是 Lua 唯一的复合数据结构，同时承担数组、字典、对象、模块的角色，是最重要的概念。

## 表是什么

### 逻辑

table 就是"一堆键值对的集合"，键可以是数字也可以是字符串。

- 键是连续数字 → 表现得像**数组**
- 键是字符串 → 表现得像**字典/对象**
- 同一个 table 可以同时有数字键和字符串键

一句话：**"Lua 的一切复杂数据都是 table"**。

## 数组用法

> [!example]+ 最常用写法
> ```lua
> local arr = {10, 20, 30}
> arr[1]          -- 10，注意下标从 1 开始！
> arr[3]          -- 30
> #arr            -- 3，长度
> arr[#arr + 1] = 40   -- 末尾追加
> table.insert(arr, 50)  -- 插入
> table.remove(arr, 1)   -- 删除下标 1
> ```

**用途**：table 当数组用。

**易错点**：
- **下标从 1 开始**（不是 0！），这是 Lua 和几乎所有语言最大的区别，坑过无数人。
- `#arr` 取长度，但表里有"空洞"（nil 值）时 `#` 结果不保证。

**版本/平台**：Lua 5.4。

**来源**：Lua 官方手册 · Table constructors（https://www.lua.org/manual/5.4/manual.html#3.4.9 ），2026-10-25 访问。

## 字典用法

> [!example]+ 最常用写法
> ```lua
> local t = {
>     name = "Alice",
>     age = 20,
> }
> t.name          -- "Alice"，点访问
> t["name"]       -- 等价，方括号访问
> t.city = "BJ"   -- 新增键
> t.age = nil     -- 删除键（赋 nil 即删除）
> t.name          -- 访问不存在的键返回 nil（不报错）
> ```

**用途**：table 当字典/对象用，键值对存取。

**易错点**：
- 访问不存在的键返回 `nil`，**不会报错**（这是很多隐蔽 bug 的来源）。
- 删除键就是把它赋值为 `nil`。
- 判断键是否存在要用 `t.name ~= nil`（因为值可能就是 nil）。

**版本/平台**：Lua 5.4。

**来源**：Lua 官方手册 · Tables（https://www.lua.org/manual/5.4/manual.html#3.4.9 ），2026-10-25 访问。

## 遍历表

> [!example]+ 最常用写法
> ```lua
> -- 遍历数组（数字键，用 ipairs）
> for i, v in ipairs(arr) do
>     print(i, v)
> end
>
> -- 遍历字典（所有键值对，用 pairs）
> for k, v in pairs(t) do
>     print(k, v)
> end
> ```

**用途**：`ipairs` 遍历数组（连续数字键），`pairs` 遍历所有键值对。

**易错点**：
- `ipairs` 只能遍历**连续的数字键**（从 1 开始，遇到 nil 停止）。
- 遍历字典/混合键用 `pairs`（顺序不保证）。

**版本/平台**：Lua 5.4。

**来源**：Lua 官方手册 · ipairs / pairs（https://www.lua.org/manual/5.4/manual.html#pdf-ipairs ），2026-10-25 访问。

## 表作为对象

> [!example]+ 最常用写法
> ```lua
> local player = {
>     hp = 100,
>     name = "hero",
> }
>
> function player.attack()      -- 冒号定义方法，可访问 self
>     print(self.name .. " attacks")
> end
>
> player.attack()               -- 调用
> ```

**用途**：Lua 没有专门的 class，用 table + 函数模拟面向对象。

**易错点**：定义方法用**冒号 `:`**（自动传 `self`），调用也用 `:`；用点 `.` 则要手动传 self。

**版本/平台**：Lua 5.4。

**来源**：Lua 官方手册 · Function definitions（https://www.lua.org/manual/5.4/manual.html#3.4.11 ），2026-10-25 访问。

## 相关链接

- [[Lua-基础语法]]
- [[Lua-函数与模块]]
- [[Lua-游戏插件实践]]
