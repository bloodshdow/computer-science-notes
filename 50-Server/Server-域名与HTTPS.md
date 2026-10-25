---
title: Server-域名与HTTPS
type: cheatsheet
tags:
  - 速查
  - 主题/服务器
  - 服务器
---

# Server-域名与HTTPS

> [!note] 平台说明
> 基于 Ubuntu 26.04。域名解析、SSL 证书（HTTPS）是网站上线到可公开访问的最后一步。

## 域名解析 DNS

> [!example]+ 最常用写法
> ```text
> 在域名服务商后台添加 A 记录：
>     主机记录  @       记录值  服务器IP
>     主机记录  www     记录值  服务器IP
> ```

**用途**：把域名指向服务器 IP，让用户能通过域名访问。

**易错点**：
- `@` 代表裸域名（example.com），`www` 是常见子域名。
- DNS 生效有延迟（几分钟到几小时），改完 `ping 域名` 验证。

**版本/平台**：通用 DNS。

**来源**：通用 DNS 概念（未联网核验，建议对照你的域名服务商文档），2026-10-25 访问。

## 申请免费证书 Certbot

> [!example]+ 最常用写法
> ```bash
> sudo apt install certbot python3-certbot-nginx
> sudo certbot --nginx -d example.com -d www.example.com
> # 自动配置 HTTPS，证书自动续期
> ```

**用途**：用 Let's Encrypt 申请免费 SSL 证书，一键开启 HTTPS。

**易错点**：
- 申请前域名必须已解析到本服务器 IP。
- Certbot 会自动续期；可 `sudo certbot renew --dry-run` 测试续期。

**版本/平台**：Ubuntu 26.04 / Certbot。

**来源**：Certbot 官方文档（https://certbot.eff.org/ ），2026-10-25 访问。

## 手动配置 HTTPS

> [!example]+ 最常用写法
> ```nginx
> server {
>     listen 443 ssl;
>     server_name example.com;
>     ssl_certificate     /etc/letsencrypt/live/example.com/fullchain.pem;
>     ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;
>     root /var/www/example;
>     index index.html;
> }
> # 再配一个 80 端口跳转到 443
> server {
>     listen 80;
>     server_name example.com;
>     return 301 https://$host$request_uri;
> }
> ```

**用途**：了解 HTTPS 的 Nginx 配置结构（Certbot 会自动生成，但懂原理便于排查）。

**易错点**：`fullchain.pem` 是证书链，`privkey.pem` 是私钥；私钥别泄露。80 端口用 `301` 跳转到 https。

**版本/平台**：Nginx。

**来源**：Nginx 官方文档 · SSL（https://nginx.org/en/docs/http/configuring_https_servers.html ），2026-10-25 访问。

## 防火墙放行端口

> [!example]+ 最常用写法
> ```bash
> sudo ufw allow 22          # SSH
> sudo ufw allow 80          # HTTP
> sudo ufw allow 443         # HTTPS
> sudo ufw enable            # 开启防火墙
> sudo ufw status            # 查看规则
> ```

**用途**：只放行必要端口（22/80/443），其他关闭，提高安全。

**易错点**：开启防火墙前**务必先放行 22 端口**，否则可能把自己 SSH 关在门外。

**版本/平台**：Ubuntu 26.04 / UFW。

**来源**：Ubuntu 官方文档 · UFW（https://ubuntu.com/server/docs/security-firewall ），2026-10-25 访问。

## 相关链接

- [[Server-Nginx基础]]
- [[Server-SSH远程]]
- [[Linux-文件与权限]]
