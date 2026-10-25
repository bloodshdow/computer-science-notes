---
title: 环境配置-Git
type: cheatsheet
tags:
  - 速查
  - 主题/环境配置
  - 工具/Git
---

# 环境配置-Git

> [!note] 定位
> Git 是版本控制工具，Windows 和 Linux 都要装。这里讲安装 + 首次配置（SSH 密钥 + 用户信息）。日常命令见下方。

## 安装 Git

> [!example]+ 步骤
> ```bash
> # Linux（Ubuntu 26.04）
> sudo apt install git
> git --version          # 验证
> ```
> ```text
> # Windows：git-scm.com 下载安装包，一路默认即可
> ```

**用途**：装 Git 本体。

**易错点**：Windows 装完会自带 "Git Bash" 终端，是 Linux 风格的命令行，很好用。

**版本/平台**：Git（Windows/Linux）。

**来源**：Git 官方文档（https://git-scm.com/book/ ），2026-10-25 访问。

## 首次配置：用户信息

> [!example]+ 最常用写法
> ```bash
> git config --global user.name "你的名字"
> git config --global user.email "你的邮箱"
> git config --global --list      # 查看配置
> ```

**用途**：让提交记录里带上你的身份，只在第一次装好时配一次。

**易错点**：`--global` 是全局生效；邮箱建议用 GitHub 注册邮箱，否则提交不关联账号。

**版本/平台**：Git。

**来源**：Git 官方文档（https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E9%A6%96%E6%AC%A1%E8%BF%90%E8%A1%8C-Git-%E5%89%8D%E7%9A%84%E9%85%8D%E7%BD%AE ），2026-10-25 访问。

## 配置 SSH 密钥（连 GitHub/Gitee 用）

> [!example]+ 最常用写法
> ```bash
> # 1. 生成密钥（一路回车即可）
> ssh-keygen -t ed25519 -C "你的邮箱"
>
> # 2. 查看公钥，复制输出
> cat ~/.ssh/id_ed25519.pub
>
> # 3. 到 GitHub → Settings → SSH keys → New SSH key，粘贴保存
>
> # 4. 测试连接
> ssh -T git@github.com
> ```

**用途**：配好后用 SSH 方式 clone/push，不用每次输密码。

**易错点**：
- 公钥是 `.pub` 结尾的那个（可以公开），私钥 `id_ed25519` 千万别泄露。
- 测试成功会提示 "Hi 用户名! You've successfully authenticated"。

**版本/平台**：Git + SSH。

**来源**：GitHub 官方文档（https://docs.github.com/zh/authentication/connecting-to-github-with-ssh ），2026-10-25 访问。

## 日常最常用命令

> [!example]+ 最常用写法
> ```bash
> git clone 仓库地址          # 克隆远程仓库到本地
> git status                  # 看当前改动状态
> git add 文件名              # 暂存改动（或 git add . 全部暂存）
> git commit -m "提交说明"    # 提交
> git push                    # 推送到远程
> git pull                    # 拉取远程更新
> ```

**用途**：日常开发的基本流程：改 → add → commit → push。

**易错点**：
- `add` 和 `commit` 是两步，忘 `add` 会提示"没有暂存的改动"。
- 改完先 `git status` 看清楚改了什么再提交，是好习惯。

**版本/平台**：Git。

**来源**：Git 官方文档（https://git-scm.com/book/ ），2026-10-25 访问。

## 把 Obsidian 库同步到 GitHub

> [!example]+ 完整步骤
> ```bash
> # 1. 进入 vault 目录，初始化（首次）
> cd 编程速查
> git init
> git branch -m main
>
> # 2. 配置身份（只需一次）
> git config --global user.name "你的名字"
> git config --global user.email "你的邮箱"
>
> # 3. 首次提交
> git add .
> git commit -m "初始导入"
>
> # 4. 关联远程仓库（先在 GitHub 网页上新建空仓库）
> git remote add origin git@github.com:你的用户名/仓库名.git
> git push -u origin main
>
> # 5. 以后每次改动后
> git add . && git commit -m "更新说明" && git push
> ```

**用途**：把 Obsidian 库放进 GitHub，获得版本控制 + 云备份 + 跨设备同步。

**易错点**：
- 先配好 SSH 密钥（见上节）才能用 `git@github.com` 免密 push。
- `.gitignore` 里建议忽略 `.obsidian/workspace.json`（工作区状态，每人不同）。
- 推荐装 **Obsidian Git 插件**，设置自动定时提交+推送，就不用每次手动敲命令了。

**版本/平台**：Git + GitHub。

**来源**：GitHub 官方文档（https://docs.github.com/zh/repositories/creating-and-managing-repositories/quickstart-for-repositories ），2026-10-25 访问。

## 相关链接

- [[环境配置-VSCode]]
- [[环境配置-WSL]]
- [[Linux-常用命令]]
- [[Server-SSH远程]]
- [[00-总目录]]
