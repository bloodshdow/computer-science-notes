---
title: CSharp-编译运行
type: cheatsheet
tags:
  - 速查
  - 语言/CSharp
---

# CSharp-编译运行

> [!note] 版本说明
> 基于 .NET 8（.NET 10 最新 LTS）。.NET 跨平台，Windows/Linux/macOS 都能跑 C#。

## 创建与运行项目

> [!example]+ 最常用写法
> ```bash
> dotnet new console -o MyApp   # 新建控制台项目
> cd MyApp
> dotnet run                    # 编译并运行
> dotnet build                  # 只编译
> ```

**用途**：`.NET SDK` 的 `dotnet` 命令管理项目生命周期。

**易错点**：
- `dotnet run` 会先编译再运行，一步到位。
- 项目文件是 `.csproj`，程序入口在 `Program.cs`。

**版本/平台**：.NET 8 / dotnet CLI。

**来源**：Microsoft Learn · dotnet CLI（https://learn.microsoft.com/zh-cn/dotnet/core/tools/ ），2026-10-25 访问。

## 装 .NET SDK

> [!example]+ 步骤
> ```bash
> # Linux（Ubuntu 26.04）
> sudo apt install dotnet-sdk-8.0
> dotnet --version    # 验证
> ```
> ```text
> # Windows：到 dotnet.microsoft.com 下载 .NET SDK 安装包
> ```

**用途**：装 .NET SDK（含编译器和运行时）。

**易错点**：写代码要装 **SDK**（含编译），只装 Runtime（运行环境）不能编译。

**版本/平台**：.NET 8 SDK。

**来源**：Microsoft Learn · 安装 .NET（https://learn.microsoft.com/zh-cn/dotnet/core/install/ ），2026-10-25 访问。

## 常见错误

> [!example]+ 最常用写法
> ```text
> error CS1002: ; expected
>     → 少分号
> error CS0103: The name 'xxx' does not exist
>     → 变量/方法名拼错或没 using
> error CS0246: The type or namespace 'xxx' could not be found
>     → 缺 using 或引用
> ```

**用途**：C# 错误码是 `CSxxxx`，搜索这个码能快速找到解决方案。

**易错点**：忘记 `using` 引入命名空间（如 `using System;`）是最常见错误。

**版本/平台**：dotnet。

**来源**：Microsoft Learn（https://learn.microsoft.com/zh-cn/dotnet/csharp/language-reference/compiler-messages/ ），2026-10-25 访问。

## 相关链接

- [[CSharp-基础语法]]
- [[环境配置-Git]]
- [[Linux-包管理]]
