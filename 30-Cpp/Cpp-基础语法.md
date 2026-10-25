---
title: Cpp-基础语法
type: cheatsheet
tags:
  - 速查
  - 语言/Cpp
---

# Cpp-基础语法

> [!note] 版本说明
> 本篇基于 C++17（主流稳定版本，教学常用）。编译运行见 [[Cpp-编译]]。

## 第一个程序与输入输出

> [!example]+ 最常用写法
> ```cpp
> #include <iostream>
> using namespace std;
> int main() {
>     int x;
>     cin >> x;                      // 输入
>     cout << "x = " << x << endl;   // 输出，endl 换行
>     return 0;
> }
> ```

**用途**：C++ 用 `cin`/`cout` 做输入输出，需要 `#include <iostream>`。

**易错点**：
- `<<` 是输出、`>>` 是输入，方向别搞反。
- `endl` 换行且刷新缓冲；想更省用 `"\n"`。
- `using namespace std;` 教学常用，但大型项目建议 `std::cout` 显式写。

**版本/平台**：C++17。

**来源**：cppreference · Basic Input/Output（https://en.cppreference.com/w/cpp/io ），2026-10-25 访问。

## 变量与基本类型

> [!example]+ 最常用写法
> ```cpp
> int a = 10;         // 整数
> double b = 3.14;    // 浮点
> char c = 'A';       // 字符，单引号
> bool flag = true;   // 布尔
> string s = "hi";    // 字符串，需 #include <string>
> ```

**用途**：声明变量。C++ 是**静态类型**，变量类型声明后固定。

**易错点**：
- 字符用单引号 `'A'`，字符串用双引号 `"A"`，两者不同。
- `string` 需要 `#include <string>`。
- 声明变量时要给初始值，未初始化的内置类型是垃圾值。

**版本/平台**：C++17。

**来源**：cppreference · Fundamental types（https://en.cppreference.com/w/cpp/language/types ），2026-10-25 访问。

## 运算符

> [!example]+ 最常用写法
> ```cpp
> int a = 7, b = 2;
> a / b        // 3，整数除法舍去小数
> a % b        // 1，取余
> a += 1       // 自增赋值，等价 a = a + 1
> a++          // 自增
> ```

**用途**：算术与自增自减运算。

**易错点**：
- 两个整数相除结果是整数（舍去小数），要小数得先转 `double`。
- `a++`（先用后加）和 `++a`（先加后用）有区别，别在复杂表达式里混用。

**版本/平台**：C++17。

**来源**：cppreference · Operators（https://en.cppreference.com/w/cpp/language/operator_arithmetic ），2026-10-25 访问。

## 控制流

> [!example]+ 最常用写法
> ```cpp
> if (x > 0) { } else if (x == 0) { } else { }
> for (int i = 0; i < 10; i++) { }      // 经典 for
> while (cond) { }
> ```

**用途**：分支与循环，用大括号 `{}` 表示代码块。

**易错点**：
- 条件必须用小括号 `()`，代码块用大括号 `{}`（和 Python 的缩进不同）。
- 判断相等用 `==`，单个 `=` 是赋值，是经典 bug 来源。

**版本/平台**：C++17。

**来源**：cppreference · Statements（https://en.cppreference.com/w/cpp/language/statements ），2026-10-25 访问。

## 范围 for（Range-based for）

> [!example]+ 最常用写法
> ```cpp
> #include <vector>
> vector<int> v = {1, 2, 3};
> for (int x : v) {          // 复制遍历
>     cout << x;
> }
> for (int& x : v) {         // 引用遍历，可修改元素
>     x *= 2;
> }
> ```

**用途**：C++11 起的简洁遍历写法，遍历容器最常用。

**易错点**：
- 默认是**按值**复制，改不了原元素；想修改要用引用 `int&`。
- 不想拷贝大对象时用 `const auto&`。

**版本/平台**：C++11+（C++17 通用）。

**来源**：cppreference · Range-based for loop（https://en.cppreference.com/w/cpp/language/range-for ），2026-10-25 访问。

## 引用（&）

> [!example]+ 最常用写法
> ```cpp
> int x = 5;
> int& r = x;      // r 是 x 的别名
> r = 10;          // 改 r 就是改 x
> void swap(int& a, int& b) { int t = a; a = b; b = t; }  // 用引用交换
> ```

**用途**：引用是变量的别名，用于函数传参避免拷贝、实现"改原值"。

**易错点**：
- 引用定义时必须初始化，且不能重新绑定到别的变量。
- 引用不是指针，没有 `null`，更安全；传参不想被改加 `const`。

**版本/平台**：C++11+。

**来源**：cppreference · Reference declaration（https://en.cppreference.com/w/cpp/language/reference ），2026-10-25 访问。

## auto 类型推导

> [!example]+ 最常用写法
> ```cpp
> auto x = 10;              // int
> auto s = string("hi");    // string
> vector<int> v = {1, 2, 3};
> for (auto it = v.begin(); it != v.end(); ++it) { }  // 省写长类型
> ```

**用途**：让编译器自动推断类型，省写冗长类型名。

**易错点**：`auto` 会丢掉引用和 const，需要时显式写 `auto&` 或 `const auto&`。

**版本/平台**：C++11+。

**来源**：cppreference · auto（https://en.cppreference.com/w/cpp/language/auto ），2026-10-25 访问。

## 相关链接

- [[Cpp-STL常用容器]]
- [[Cpp-类与对象]]
- [[Cpp-编译]]
