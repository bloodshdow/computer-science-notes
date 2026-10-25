---
title: Cpp-类与对象
type: cheatsheet
tags:
  - 速查
  - 语言/Cpp
---

# Cpp-类与对象

> [!note] 版本说明
> 基于 C++17。类（class）是 C++ 面向对象的核心。

## 定义类与构造/析构

> [!example]+ 最常用写法
> ```cpp
> #include <iostream>
> using namespace std;
>
> class Person {
> public:
>     string name;
>     int age;
>     Person(string n, int a) : name(n), age(a) {}   // 构造函数
>     ~Person() { cout << "析构\n"; }                 // 析构函数
>     void sayHi() { cout << "Hi " << name; }
> };
>
> int main() {
>     Person p("Alice", 20);   // 调用构造函数
>     p.sayHi();               // 调用成员函数
> }
> ```

**用途**：封装数据（成员变量）和行为（成员函数）。

**易错点**：
- 构造函数名和类同名、无返回值；析构函数名前加 `~`。
- `public:` 后的成员外部可访问，`private:` 后的只能类内部访问（默认是 `private`）。
- 成员初始化用初始化列表 `: name(n), age(a)`，比在函数体里赋值高效。

**版本/平台**：C++17。

**来源**：cppreference · Classes（https://en.cppreference.com/w/cpp/language/classes ），2026-10-25 访问。

## 访问控制

> [!example]+ 最常用写法
> ```cpp
> class A {
> private:    // 只有类内部能访问
>     int secret;
> public:     // 外部能访问
>     int getSecret() { return secret; }
> };
> ```

**用途**：`private` 隐藏内部细节，`public` 提供对外接口，即封装。

**易错点**：`class` 默认成员是 `private`；`struct` 默认是 `public`（这是两者唯一区别）。

**版本/平台**：C++17。

**来源**：cppreference · Access specifiers（https://en.cppreference.com/w/cpp/language/access ），2026-10-25 访问。

## 继承

> [!example]+ 最常用写法
> ```cpp
> class Animal {
> public:
>     void eat() { }
> };
> class Dog : public Animal {   // Dog 继承 Animal
> public:
>     void bark() { }
> };
> Dog d;
> d.eat();     // 继承来的方法
> d.bark();    // 自己的方法
> ```

**用途**：子类复用父类的成员，表达"是"的关系。

**易错点**：继承用 `public`（`class Dog : public Animal`），表示公开继承，是最常用方式。

**版本/平台**：C++17。

**来源**：cppreference · Inheritance（https://en.cppreference.com/w/cpp/language/derived_class ），2026-10-25 访问。

## 虚函数与多态

> [!example]+ 最常用写法
> ```cpp
> class Animal {
> public:
>     virtual void speak() { cout << "?\n"; }   // 虚函数
>     virtual ~Animal() {}                      // 虚析构，重要
> };
> class Dog : public Animal {
> public:
>     void speak() override { cout << "Woof\n"; }
> };
> Animal* p = new Dog();
> p->speak();      // "Woof"，调用的是 Dog 的实现（多态）
> delete p;        // 虚析构保证正确释放
> ```

**用途**：基类指针指向派生类对象时，调用派生类的重写实现，即多态。

**易错点**：
- 实现多态，基类方法要加 `virtual`，子类重写加 `override`。
- 基类**析构函数必须是虚函数**，否则 `delete` 基类指针不会调用派生类析构，会内存泄漏。
- `override` 关键字能让编译器检查是否真的重写（拼错会报错）。

**版本/平台**：C++11+（`override`），C++17 通用。

**来源**：cppreference · virtual function（https://en.cppreference.com/w/cpp/language/virtual ），2026-10-25 访问。

## 相关链接

- [[Cpp-基础语法]]
- [[Cpp-STL常用容器]]
- [[Cpp-编译]]
