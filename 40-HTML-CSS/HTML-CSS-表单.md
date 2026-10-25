---
title: HTML-CSS-表单
type: cheatsheet
tags:
  - 速查
  - 语言/HTML-CSS
  - HTML
---

# HTML-CSS-表单

## 表单基本结构

> [!example]+ 最常用写法
> ```html
> <form action="/submit" method="post">
>     <label for="name">姓名：</label>
>     <input type="text" id="name" name="name">
>     <button type="submit">提交</button>
> </form>
> ```

**用途**：收集用户输入并提交。`action` 是提交地址，`method` 是请求方式（`get`/`post`）。

**易错点**：
- `<label for="id">` 的 `for` 要对应 `<input>` 的 `id`，点击标签能聚焦输入框。
- 提交按钮用 `<button type="submit">`；`<button>` 默认 type 就是 submit，但显式写更清晰。

**版本/平台**：HTML5。

**来源**：MDN · form（https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/form ），2026-10-25 访问。

## 常用 input 类型

> [!example]+ 最常用写法
> ```html
> <input type="text" placeholder="提示文字">        <!-- 文本 -->
> <input type="password">                          <!-- 密码 -->
> <input type="email">                             <!-- 邮箱 -->
> <input type="number" min="0" max="100">          <!-- 数字 -->
> <input type="checkbox"> 复选                        <!-- 复选框 -->
> <input type="radio" name="g"> 单选                <!-- 单选，同名成组 -->
> <input type="date">                              <!-- 日期 -->
> <input type="file">                              <!-- 文件上传 -->
> ```

**用途**：不同类型提供不同的输入控件和内置校验。

**易错点**：
- 单选 `radio` 要靠**相同的 `name`** 才能互斥成组。
- `email`/`number` 等类型浏览器会自动做格式校验。
- `checkbox` 勾选的值要配合 `value` 提交。

**版本/平台**：HTML5。

**来源**：MDN · input types（https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input ），2026-10-25 访问。

## 下拉与多行文本

> [!example]+ 最常用写法
> ```html
> <select name="city">
>     <option value="bj">北京</option>
>     <option value="sh" selected>上海</option>
> </select>
>
> <textarea name="desc" rows="5" cols="30"></textarea>
> ```

**用途**：`<select>` 下拉选择，`<textarea>` 多行文本输入。

**易错点**：`selected` 标记默认选中项；`textarea` 是成对标签，不要自闭合。

**版本/平台**：HTML5。

**来源**：MDN · select / textarea（https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/select ），2026-10-25 访问。

## 必填与校验

> [!example]+ 最常用写法
> ```html
> <input type="text" required>          <!-- 必填 -->
> <input type="text" pattern="[0-9]{4}"> <!-- 正则约束 -->
> <input type="text" maxlength="10">    <!-- 最大长度 -->
> ```

**用途**：前端基本校验，减少无效提交。

**易错点**：前端校验只是体验优化，**不能替代后端校验**（可被绕过）。

**版本/平台**：HTML5。

**来源**：MDN · form validation（https://developer.mozilla.org/zh-CN/docs/Learn/Forms/Form_validation ），2026-10-25 访问。

## 相关链接

- [[HTML-CSS-常用标签]]
- [[HTML-CSS-盒模型与选择器]]
