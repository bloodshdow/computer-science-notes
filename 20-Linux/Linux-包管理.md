---
title: Linux-包管理
type: cheatsheet
tags:
  - 速查
  - 语言/Linux
---

# Linux-包管理

> [!note] 平台说明
> 本篇针对 **Debian/Ubuntu 系**（你笔记本是 Ubuntu）。Fedora/Arch 用 `dnf`/`pacman`，命令不同。

## apt 安装与更新

> [!example]+ 最常用写法
> ```bash
> sudo apt update                # 刷新软件源索引（安装前先跑）
> sudo apt upgrade               # 升级所有已装包
> sudo apt install 包名          # 安装
> sudo apt install vim git curl  # 一次装多个
> sudo apt remove 包名           # 卸载（保留配置）
> sudo apt purge 包名            # 卸载并删除配置
> ```

**用途**：从软件仓库安装、升级、卸载软件。

**易错点**：
- 安装前先 `sudo apt update`，否则可能装到旧版本或找不到包。
- `remove` 保留配置文件，`purge` 连配置一起删。

**版本/平台**：Ubuntu 26.04 / apt。

**来源**：Ubuntu 官方文档 · Package management（https://ubuntu.com/server/docs/package-management ），2026-10-25 访问。

## 搜索与查看

> [!example]+ 最常用写法
> ```bash
> apt search 关键词              # 搜包
> apt show 包名                  # 看包详情
> apt list --installed           # 列出已装包
> dpkg -l | grep 包名            # 查某包是否已装（验证方式）
> ```

**用途**：查找软件包、确认安装状态。

**易错点**：`dpkg -l | grep 包名` 是确认"是否已装"的常用验证方式；`apt search` 在远程仓库里搜。

**版本/平台**：Ubuntu 26.04 / apt + dpkg。

**来源**：Ubuntu 官方文档 · Package management（同上），2026-10-25 访问。

## 安装本地 .deb 文件（最常用场景）

### 推荐方式：apt 直接装

> [!example]+ 最常用写法
> ```bash
> # 先进入下载目录，再装。注意 ./ 前缀表示"当前目录下的这个文件"
> cd ~/Downloads
> sudo apt install ./包名.deb
> ```

**用途**：安装从网上下载的 `.deb`（如 Chrome、VSCode、微信、QQ）。这是**首选方式**，因为 `apt` 会自动下载并补齐依赖。

**易错点**：
- 一定要加 `./` 前缀，否则 `apt` 会把它当成仓库里的包名而不是本地文件。
- 装完验证：`dpkg -l | grep 包名` 看有没有出现在列表里。

### 备选方式：dpkg

> [!example]+ 最常用写法
> ```bash
> sudo dpkg -i 包名.deb        # 直接装，但不自动处理依赖
> ```

**用途**：老办法。缺点是缺依赖会装失败。

**易错点**：`dpkg -i` 报"依赖不满足"时，跑一次 `sudo apt install -f`（`-f` = fix-broken）会自动补装缺失的依赖。

### 图形化方式（KDE 桌面）

> [!note]- KDE 下双击安装
> 在 Dolphin（文件管理器）里双击 `.deb` 文件，KDE 会弹出"发现/Discover"或软件安装器，点"安装"即可，等同于走 apt。这是最快的方式，适合不记得命令时用。

### 装完怎么卸载

> [!example]+ 最常用写法
> ```bash
> sudo apt remove 包名          # 卸载，保留配置
> sudo apt purge 包名           # 卸载并删配置（彻底）
> ```

**易错点**：卸载用**包名**（如 `google-chrome-stable`），不是文件名。不知道包名时先 `dpkg -l | grep 关键词` 查。

**版本/平台**：Ubuntu 26.04 / apt + dpkg。

**来源**：Ubuntu 官方文档 · Package management（https://ubuntu.com/server/docs/package-management ）；dpkg 手册页（`man dpkg`），2026-10-25 访问。

## 软件源 sources.list

> [!example]+ 最常用写法
> ```bash
> cat /etc/apt/sources.list            # 查看软件源
> sudo apt update                      # 改完源后要更新
> ```

**用途**：软件源决定 apt 从哪里下载包；国内网络可换清华/阿里镜像加速。

**易错点**：改 `sources.list` 前先备份；改完必须 `sudo apt update` 才生效。

**版本/平台**：Ubuntu 26.04。

**来源**：Ubuntu 官方文档 · SourcesList（https://help.ubuntu.com/community/SourcesList ），2026-10-25 访问。

## 相关链接

- [[Linux-常用命令]]
- [[Python-虚拟环境与pip]]
- [[Linux-文件与权限]]
