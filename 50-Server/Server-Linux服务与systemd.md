---
title: Server-Linux服务与systemd
type: cheatsheet
tags:
  - 速查
  - 主题/服务器
  - 服务器
---

# Server-Linux服务与systemd

> [!note] 平台说明
> 基于 Ubuntu 26.04。systemd 是 Ubuntu 默认的初始化系统，负责管理后台服务（如 nginx、mysql）。

## 服务管理 systemctl

> [!example]+ 最常用写法
> ```bash
> sudo systemctl start nginx      # 启动
> sudo systemctl stop nginx       # 停止
> sudo systemctl restart nginx    # 重启
> sudo systemctl status nginx     # 查看状态（验证方式）
> sudo systemctl enable nginx     # 开机自启
> sudo systemctl disable nginx    # 取消自启
> ```

**用途**：启动、停止、重启、查看服务，设置开机自启。

**易错点**：
- `start` 只是这次启动，`enable` 才是开机自启，两者要分别设。
- 排查问题先 `status`，看 `Active:` 和报错日志。

**版本/平台**：Ubuntu 26.04 / systemd。

**来源**：systemctl 手册页（`man systemctl`），2026-10-25 访问。

## 查看日志 journalctl

> [!example]+ 最常用写法
> ```bash
> sudo journalctl -u nginx          # 看某服务的日志
> sudo journalctl -u nginx -f       # 实时跟踪日志
> sudo journalctl -xe               # 最近日志 + 错误解释
> ```

**用途**：查看服务日志，定位启动失败原因。

**易错点**：`-f` 持续跟踪，退出按 `Ctrl+C`；服务起不来先看 `journalctl -u 服务名`。

**版本/平台**：Ubuntu 26.04 / systemd。

**来源**：journalctl 手册页（`man journalctl`），2026-10-25 访问。

## 编写自定义服务单元

> [!example]+ 最常用写法
> ```bash
> # 新建 /etc/systemd/system/myapp.service
> [Unit]
> Description=My App
> After=network.target
>
> [Service]
> WorkingDirectory=/opt/myapp
> ExecStart=/usr/bin/python3 /opt/myapp/app.py
> Restart=always
> User=ubuntu
>
> [Install]
> WantedBy=multi-user.target
> ```

**用途**：把自己写的程序（如 Python 后端）注册成系统服务，开机自启、崩溃重启。

**易错点**：
- 写完服务文件后要 `sudo systemctl daemon-reload` 再 `start`。
- `ExecStart` 用绝对路径；`Restart=always` 让进程崩溃后自动拉起。
- 用非 root 的 `User` 运行更安全。

**版本/平台**：Ubuntu 26.04 / systemd。

**来源**：systemd.service 手册页（`man systemd.service`），2026-10-25 访问。

## 相关链接

- [[Server-SSH远程]]
- [[Server-Nginx基础]]
- [[Linux-进程管理]]
