---
title: Linux-KDE桌面
type: cheatsheet
tags:
  - 速查
  - 语言/Linux
---

# Linux-KDE桌面

> [!note] 平台说明
> 本篇针对 KDE Plasma 桌面（你的笔记本环境）。命令适用于 KDE 5/6，具体版本可用 `plasmashell --version` 查看。

## 常用快捷键

> [!example]+ 最常用写法
> ```text
> Alt + Space     打开 KRunner（搜索应用/文件/命令）
> Ctrl + Alt + T  打开终端（默认 Konsole）
> Super(徽标键)   打开应用菜单
> Super + W       窗口概览 / 平铺
> Ctrl + F10      切换所有窗口
> ```

**用途**：KDE 里最常用的快捷操作。

**易错点**：快捷键可在 系统设置 → 快捷键 里自定义；部分笔记本 `Super` 键被 BIOS 占用需另设。

**版本/平台**：KDE Plasma 5/6（Ubuntu KDE 分支如 Kubuntu）。

**来源**：KDE 官方文档（https://docs.kde.org/ ），2026-10-25 访问。

## KRunner 快速启动

> [!example]+ 最常用写法
> ```text
> Alt + Space 输入应用名 → 回车启动
> Alt + Space 输入命令 → 直接执行
> Alt + Space 输入算式 → 直接算（如 2+2）
> ```

**用途**：最快的应用启动和命令入口，类似 macOS 的 Spotlight。

**易错点**：KRunner 默认就是 Alt+Space，若被改可在系统设置里找回。

**版本/平台**：KDE Plasma 5/6。

**来源**：KDE 官方文档 · KRunner（https://docs.kde.org/ ），2026-10-25 访问。

## 终端 Konsole 与包管理

> [!example]+ 最常用写法
> ```bash
> sudo apt install konsole        # KDE 自带终端
> sudo apt install dolphin        # 文件管理器
> # 系统设置对应的配置模块叫 systemsettings
> ```

**用途**：KDE 核心组件。文件管理用 Dolphin，设置用 System Settings。

**易错点**：KDE 的包在 Ubuntu 上同样用 `apt` 管理，见 [[Linux-包管理]]。

**版本/平台**：KDE Plasma / Ubuntu。

**来源**：KDE 官方文档（https://docs.kde.org/ ），2026-10-25 访问。

## 常用命令交互

> [!example]+ 最常用写法
> ```bash
> plasmashell --version      # 查看 KDE 版本
> kwin_x11 --replace &       # 重启窗口管理器（界面卡住时）
> systemsettings             # 打开系统设置
> ```

**用途**：查看版本、重启图形组件、打开设置。

**易错点**：界面卡死时 `kwin_x11 --replace` 可重启窗口管理器；Wayland 会话下命令不同（`kwin_wayland`）。

**版本/平台**：KDE Plasma 5/6。

**来源**：KDE 官方文档（https://docs.kde.org/ ），2026-10-25 访问。

## 相关链接

- [[Linux-常用命令]]
- [[Linux-包管理]]
