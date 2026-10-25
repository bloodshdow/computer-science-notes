---
title: Server-SSH远程
type: cheatsheet
tags:
  - 速查
  - 主题/服务器
  - 服务器
---

# Server-SSH远程

> [!note] 平台说明
> 基于 Ubuntu 26.04 + OpenSSH。SSH 是远程管理服务器的基础，搭站前必须先会。

## 连接远程服务器

> [!example]+ 最常用写法
> ```bash
> ssh 用户名@服务器IP        # 默认端口 22
> ssh -p 2222 用户@IP       # 指定端口
> ssh -i 密钥.pem 用户@IP   # 用密钥文件连接
> ```

**用途**：从本地登录远程 Linux 服务器。

**易错点**：
- 首次连接会提示确认指纹，输入 `yes`。
- 云服务器常用密钥登录，密钥文件权限要正确（`chmod 600 密钥.pem`）。

**版本/平台**：OpenSSH（Ubuntu 26.04）。

**来源**：OpenSSH 手册（https://man.openbsd.org/ssh ），2026-10-25 访问。

## 上传下载文件 scp / rsync

> [!example]+ 最常用写法
> ```bash
> scp 本地文件 用户@IP:/远程路径     # 上传
> scp 用户@IP:/远程文件 本地路径     # 下载
> scp -r 本地目录 用户@IP:/远程路径  # 上传整个目录
> rsync -avz 本地目录/ 用户@IP:/远程目录/  # 增量同步，更快
> ```

**用途**：本地和服务器之间传文件。

**易错点**：
- `scp -r` 才能传目录。
- 大量/频繁同步用 `rsync`，只传差异部分，效率高。

**版本/平台**：OpenSSH / rsync。

**来源**：scp / rsync 手册（`man scp`、`man rsync`），2026-10-25 访问。

## 密钥登录（免密）

> [!example]+ 最常用写法
> ```bash
> ssh-keygen -t ed25519          # 本地生成密钥对
> ssh-copy-id 用户@IP            # 把公钥复制到服务器（免密登录）
> # 之后直接 ssh 用户@IP 无需密码
> ```

**用途**：配置密钥登录，比密码更安全、更方便。

**易错点**：
- 生成密钥时直接回车用默认路径，可设空密码。
- 私钥（`id_ed25519`）留在本地别泄露；公钥（`.pub`）放到服务器。

**版本/平台**：OpenSSH。

**来源**：OpenSSH 手册（https://man.openbsd.org/ssh-keygen ），2026-10-25 访问。

## SSH 配置简化

> [!example]+ 最常用写法
> ```bash
> # 编辑 ~/.ssh/config
> Host myserver
>     HostName 1.2.3.4
>     User ubuntu
>     Port 22
> # 之后直接： ssh myserver
> ```

**用途**：给服务器起别名，省去每次敲 IP 和用户名。

**易错点**：配置文件 `~/.ssh/config` 权限应为 `600`，否则 SSH 可能拒绝使用。

**版本/平台**：OpenSSH。

**来源**：OpenSSH 手册 · ssh_config（https://man.openbsd.org/ssh_config ），2026-10-25 访问。

## 相关链接

- [[Server-Linux服务与systemd]]
- [[Server-Nginx基础]]
- [[Linux-文件与权限]]
