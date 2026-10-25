---
title: Cpp-STL常用容器
type: cheatsheet
tags:
  - 速查
  - 语言/Cpp
---

# Cpp-STL常用容器

> [!note] 版本说明
> 基于 C++17。STL（标准模板库）容器是 C++ 最常用的工具，掌握 vector/string/map/set 即可覆盖大部分场景。

## vector 动态数组

> [!example]+ 最常用写法
> ```cpp
> #include <vector>
> using namespace std;
> vector<int> v = {1, 2, 3};
> v.push_back(4);        // 末尾添加
> v[0] = 10;             // 下标访问（不检查越界）
> v.size();              // 元素个数
> v.pop_back();          // 删除末尾
> v.empty();             // 是否为空
> for (int x : v) { }    // 遍历
> ```

**用途**：可动态增长的数组，最常用容器。

**易错点**：
- `v[i]` 不检查越界，越界是**未定义行为**；要安全用 `v.at(i)`（越界抛异常）。
- 遍历优先用范围 for，简单安全。

**版本/平台**：C++11+（C++17 通用）。

**来源**：cppreference · std::vector（https://en.cppreference.com/w/cpp/container/vector ），2026-10-25 访问。

## string 字符串

> [!example]+ 最常用写法
> ```cpp
> #include <string>
> string s = "hello";
> s.length();            // 或 s.size()，长度
> s + " world"           // 拼接
> s.substr(0, 2);        // "he"，从 0 起取 2 个
> s.find("ell");         // 查找，返回下标，找不到返回 string::npos
> s[0];                  // 下标访问字符
> s == "hello"           // 比较
> ```

**用途**：比 C 风格 `char[]` 好用得多的字符串类型。

**易错点**：
- `find` 找不到返回 `string::npos`（一个很大的值），不是 -1。
- `substr(pos, len)` 的第二个参数是**长度**，不是结束下标。
- 字符串比较用 `==` 直接比内容。

**版本/平台**：C++11+。

**来源**：cppreference · std::string（https://en.cppreference.com/w/cpp/string/basic_string ），2026-10-25 访问。

## map 键值对

> [!example]+ 最常用写法
> ```cpp
> #include <map>
> map<string, int> m;
> m["apple"] = 5;        // 插入或修改
> m["apple"];            // 访问；键不存在会自动插入默认值 0
> m.count("apple");      // 是否存在（0 或 1）
> m.erase("apple");      // 删除
> for (auto& [k, v] : m) { }   // 遍历键值对（C++17 结构化绑定）
> ```

**用途**：按键存取值，内部自动按 key 排序，基于红黑树。

**易错点**：
- `m[key]` 键不存在时会**自动插入一个默认值**，别误用于只读查询；只查用 `m.find(key)` 或 `m.count(key)`。
- 需要不排序、更快用 `unordered_map`（哈希表）。

**版本/平台**：C++11+（结构化绑定需 C++17）。

**来源**：cppreference · std::map（https://en.cppreference.com/w/cpp/container/map ），2026-10-25 访问。

## set 集合

> [!example]+ 最常用写法
> ```cpp
> #include <set>
> set<int> s;
> s.insert(3);           // 插入，自动去重并排序
> s.count(3);            // 是否存在
> s.erase(3);            // 删除
> s.size();              // 大小
> ```

**用途**：自动去重 + 排序的集合。

**易错点**：`set` 元素唯一且有序；要允许重复用 `multiset`，要更快且无序用 `unordered_set`。

**版本/平台**：C++11+。

**来源**：cppreference · std::set（https://en.cppreference.com/w/cpp/container/set ），2026-10-25 访问。

## 迭代器基础

> [!example]+ 最常用写法
> ```cpp
> vector<int> v = {1, 2, 3};
> for (auto it = v.begin(); it != v.end(); ++it) {
>     cout << *it;      // *it 取元素值
> }
> ```

**用途**：通用遍历方式，`begin()` 指向首元素、`end()` 指向末尾之后。

**易错点**：遍历条件用 `!= end()` 而不是 `<`；`*it` 解引用取值。

**版本/平台**：C++11+。

**来源**：cppreference · Iterator（https://en.cppreference.com/w/cpp/iterator ），2026-10-25 访问。

## 相关链接

- [[Cpp-基础语法]]
- [[Cpp-类与对象]]
- [[Cpp-编译]]
- [[数据结构-数组与动态数组]]
- [[Python-列表与元组]]
- [[数据结构-散列表]]
- [[数据结构-红黑树]]
