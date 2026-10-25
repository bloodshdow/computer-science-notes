---
title: Lua-游戏插件实践
type: cheatsheet
tags:
  - 速查
  - 语言/Lua
---

# Lua-游戏插件实践

> [!note] 版本说明
> 基于 Lua 5.4。Lua 广泛用于游戏脚本和插件（Roblox、Love2D、魔兽世界/ElvUI 插件、Neovim 配置等）。这里讲游戏脚本常见套路。

## 游戏循环（Love2D 风格）

> [!example]+ 最常用写法
> ```lua
> function love.load()        -- 初始化（加载资源）
>     player = { x = 100, y = 100 }
> end
>
> function love.update(dt)    -- 每帧更新，dt 是帧间隔（秒）
>     player.x = player.x + 100 * dt   -- 按时间移动，帧率无关
> end
>
> function love.draw()        -- 每帧绘制
>     love.graphics.rectangle("fill", player.x, player.y, 32, 32)
> end
> ```

**用途**：游戏引擎用回调函数组织代码：load 初始化、update 更新逻辑、draw 绘制画面。

**易错点**：
- 移动要乘 `dt`（帧间隔），否则不同帧率下速度不一样。
- `dt` 单位是秒，`100 * dt` 表示每秒移动 100 像素。

**版本/平台**：LÖVE（Love2D）/ Lua。

**来源**：LÖVE 官方 wiki（https://love2d.org/wiki/Main_Page ），2026-10-25 访问。

## 事件回调（插件常见）

> [!example]+ 最常用写法
> ```lua
> -- 注册事件处理器（魔兽世界插件/ElvUI 风格）
> local frame = CreateFrame("Frame")
> frame:RegisterEvent("PLAYER_LOGIN")
> frame:SetScript("OnEvent", function(self, event, ...)
>     if event == "PLAYER_LOGIN" then
>         print("玩家登录了")
>     end
> end)
> ```

**用途**：游戏/插件靠"注册事件 → 回调函数"响应游戏内事件。

**易错点**：
- 回调里用 `self` 访问触发对象（冒号定义）。
- 事件名是字符串，拼错不会报错、只是不触发（难排查）。

**版本/平台**：魔兽世界 WoW API / Lua。

**来源**：Wowpedia 插件 API（https://warcraft.wiki.gg/wiki/World_of_Warcraft_API ），2026-10-25 访问。

## 常用工具函数

> [!example]+ 最常用写法
> ```lua
> math.random(1, 10)          -- 1~10 随机整数
> math.max(a, b)              -- 取大
> math.floor(3.7)             -- 3，向下取整
> string.format("%.2f", 3.14159)   -- 格式化
> string.sub("hello", 1, 3)   -- "hel"，截取
> tonumber("42")              -- 字符串转数字
> tostring(42)                -- 数字转字符串
> ```

**用途**：游戏脚本常用的数学和字符串函数。

**易错点**：
- `math.random` 要先用 `math.randomseed(os.time())` 设种子，否则每次结果相同。
- `string.sub` 的下标从 1 开始（和表一致）。

**版本/平台**：Lua 5.4 标准库。

**来源**：Lua 官方手册 · math / string（https://www.lua.org/manual/5.4/manual.html#6.7 ），2026-10-25 访问。

## 相关链接

- [[Lua-表]]
- [[Lua-函数与模块]]
- [[Lua-基础语法]]
