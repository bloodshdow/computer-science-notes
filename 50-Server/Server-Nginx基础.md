---
title: Server-Nginx基础
type: cheatsheet
tags:
  - 速查
  - 主题/服务器
  - 服务器
---

# Server-Nginx基础

> [!note] 平台说明
> 基于 Ubuntu 26.04 + Nginx。Nginx 是高性能 Web 服务器和反向代理，部署静态网站最常用。

## 安装与启动

> [!example]+ 最常用写法
> ```bash
> sudo apt update
> sudo apt install nginx
> sudo systemctl start nginx
> sudo systemctl enable nginx
> dpkg -l | grep nginx      # 验证是否已装
> ```

**用途**：安装并启动 Nginx 服务。

**易错点**：装完浏览器访问服务器 IP，看到 Nginx 欢迎页即成功；打不开先检查 `systemctl status nginx` 和防火墙。

**版本/平台**：Ubuntu 26.04 / Nginx。

**来源**：Nginx 官方文档（https://nginx.org/en/docs/ ），2026-10-25 访问。

## 关键目录与文件

> [!example]+ 最常用写法
> ```bash
> /etc/nginx/nginx.conf          # 主配置
> /etc/nginx/sites-available/    # 可用站点配置
> /etc/nginx/sites-enabled/      # 已启用的站点（软链接）
> /var/www/html/                 # 默认网站根目录
> ```

**用途**：了解 Nginx 配置和文件放哪。

**易错点**：站点配置放 `sites-available`，用软链接到 `sites-enabled` 才生效；改完配置要 `sudo nginx -t` 检查、再 `reload`。

**版本/平台**：Ubuntu 26.04 / Nginx。

**来源**：Nginx 官方文档（同上），2026-10-25 访问。

## 配置静态站点

> [!example]+ 最常用写法
> ```nginx
> server {
>     listen 80;
>     server_name example.com;
>     root /var/www/example;        # 网站文件目录
>     index index.html;
> }
> ```

**用途**：让 Nginx 托管一个静态网站（HTML/CSS/JS）。

**易错点**：
- `root` 指向网站文件所在目录。
- 改完执行 `sudo nginx -t` 验证语法，再 `sudo systemctl reload nginx` 生效。

**版本/平台**：Nginx。

**来源**：Nginx 官方文档 · Server blocks（https://nginx.org/en/docs/http/server_names.html ），2026-10-25 访问。

## 反向代理

> [!example]+ 最常用写法
> ```nginx
> server {
>     listen 80;
>     server_name example.com;
>     location / {
>         proxy_pass http://127.0.0.1:8000;   # 转发到本地后端
>         proxy_set_header Host $host;
>     }
> }
> ```

**用途**：把请求转发给后端应用（如 Python 跑在 8000 端口），实现前后端部署。

**易错点**：`proxy_pass` 指向后端监听地址；后端端口（如 8000）不要直接暴露公网，走 Nginx 转发更安全。

**版本/平台**：Nginx。

**来源**：Nginx 官方文档 · Reverse proxy（https://nginx.org/en/docs/http/ngx_http_proxy_module.html ），2026-10-25 访问。

## 常用管理命令

> [!example]+ 最常用写法
> ```bash
> sudo nginx -t                # 检查配置语法
> sudo systemctl reload nginx  # 重载配置（不中断服务）
> sudo systemctl restart nginx # 重启
> sudo tail -f /var/log/nginx/error.log   # 看错误日志
> ```

**用途**：配置检查、重载、查日志。

**易错点**：改配置后先 `nginx -t` 通过再 `reload`，避免配错导致服务挂掉。

**版本/平台**：Nginx。

**来源**：Nginx 官方文档（同上），2026-10-25 访问。

## 相关链接

- [[Server-SSH远程]]
- [[Server-Linux服务与systemd]]
- [[Server-域名与HTTPS]]
