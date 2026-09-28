# AI 助教答疑平台

> 智能答疑 · 随时提问

一个基于 **HTML5 + CSS** 的 AI 助教答疑平台前端原型，包含**个性化注册页面**与**登录页面**。纯原生实现，不依赖 JavaScript 与任何外部库。

---

## 一、项目简介

本平台面向高校师生，提供 AI 智能答疑服务。本阶段完成用户体系的入口页面：

| 页面 | 文件 | 说明 |
|------|------|------|
| 主页 | `index.html` | 答疑对话界面：提问输入框 + 「模拟回复」气泡 |
| 登录页 | `login.html` | 账号/邮箱 + 密码登录，支持「记住我」 |
| 注册页 | `register.html` | 用户名、邮箱、手机号、密码、确认密码、身份选择 |
| 截图目录 | `screenshots/` | 存放多轮对话过程截图 |

两页面通过底部 `<a>` 链接互相跳转，形成完整闭环。

---

## 二、开发环境与方式

- **操作系统**：Windows 11 Home China
- **编辑器**：VS Code
- **开发方式**：VS Code 内 AI 编程助手（Codex / Claude Code）**多轮对话**驱动开发
- **技术栈**：纯 HTML5 + CSS（无 JS、无外部框架/图标库）
- **版本管理**：Git + Gitee

---

## 三、多轮对话开发过程

> ⚠️ 提交学习通前，请按下方「截图操作指引」把每轮对话截图放入 `screenshots/` 目录，替换表格中的占位图。

| 轮次 | 我的提问 / 需求（摘要） | AI 助手的实现 | 截图 |
|------|------------------------|--------------|------|
| 第 1 轮 | 完成登录页 `login.html` 与注册页 `register.html`，纯 HTML5+CSS，尽量使用表单增强特性 | 生成两个完整页面，含 required / pattern / type="email" / type="tel" / select 等全部增强特性 | ![第1轮](screenshots/第1轮.png) |
| 第 2 轮 | 「看看效果」 | 在默认浏览器打开两个页面预览，并逐项说明可测试的原生校验项 | ![第2轮](screenshots/第2轮.png) |
| 第 3 轮 | 补充完整作业要求：设计平台 + 多轮对话 + 整理文档 + 推送代码仓库 | 规范化项目目录、生成开发文档、初始化 Git 仓库 | ![第3轮](screenshots/第3轮.png) |
| 第 4 轮 | 描述平台主页（答疑对话界面）效果图 | 新建 `index.html`，实现大标题、提问输入框与「模拟回复」气泡 | ![第4轮](screenshots/第4轮.png) |
| 第 5 轮 | 「同步到 GitHub」 | 配置远程仓库、提交代码，通过本地代理成功推送到 GitHub | ![第5轮](screenshots/第5轮.png) |

> 多轮对话的核心价值在于「需求逐步细化 → 代码迭代 → 文档沉淀 → 版本管理」的完整闭环，每一轮截图都是过程性证据。

### 截图操作指引（Windows）

1. 按下 `Win + Shift + S`，鼠标框选需要截图的对话区域（或 `Win + PrtScn` 截全屏）。
2. 将截图按轮次保存到 `screenshots/` 目录，**文件名必须**为：`第1轮.png`、`第2轮.png`、`第3轮.png`、`第4轮.png`、`第5轮.png`。
3. 保存后刷新预览，图片即自动嵌入上方表格与打印文档。

---

## 四、HTML5 表单增强特性详解

两个页面**尽可能使用原生表单校验能力**，将数据校验交给浏览器，无需编写一行 JS。逐项说明如下：

### 4.1 `required` —— 必填校验
所有关键字段均为必填，未填写时浏览器阻止提交并给出提示。

```html
<input type="email" name="email" placeholder="请输入邮箱地址" required>
```

**应用位置**：登录页的账号、密码；注册页的全部字段。

### 4.2 `placeholder` —— 占位提示
每个输入框都有灰色占位文字，引导用户正确填写，聚焦后自动消失。

```html
<input type="password" name="password" placeholder="请输入密码" required>
```

### 4.3 `autofocus` —— 自动聚焦
页面加载后自动聚焦首个输入框，减少一次点击。

```html
<!-- login.html -->
<input type="text" id="account" name="account" required autofocus autocomplete="username">

<!-- register.html -->
<input type="text" id="username" name="username" required autofocus autocomplete="username">
```

### 4.4 `autocomplete` —— 自动填充
提示浏览器按语义自动填充，提升体验：

| 字段 | autocomplete 值 | 含义 |
|------|----------------|------|
| 用户名/账号 | `username` | 用户名自动填充 |
| 邮箱 | `email` | 邮箱自动填充 |
| 手机号 | `tel` | 电话自动填充 |
| 登录密码 | `current-password` | 当前密码 |
| 注册密码/确认密码 | `new-password` | 新密码（可触发浏览器「生成强密码」建议） |

### 4.5 `type="email"` —— 邮箱类型校验
使用邮箱专用输入类型，浏览器自动校验格式（如必须含 `@` 与域名）。

```html
<input type="email" id="email" name="email" placeholder="请输入邮箱地址" required autocomplete="email">
```

### 4.6 `type="tel"` + `pattern` —— 手机号正则校验
`type="tel"` 在移动端弹出数字键盘；`pattern` 用正则限制 11 位大陆手机号格式，`title` 提供自定义错误提示。

```html
<input type="tel" id="phone" name="phone"
       placeholder="请输入11位手机号"
       pattern="1[3-9][0-9]{9}"
       title="请输入以1开头的11位有效手机号"
       required autocomplete="tel">
```

- 正则 `1[3-9][0-9]{9}`：以 `1` 开头，第二位为 `3~9`，后接 9 位数字，共 11 位。

### 4.7 `pattern` —— 用户名格式校验
用户名限定为 4–20 位字母或数字。

```html
<input type="text" id="username" name="username"
       pattern="[A-Za-z0-9]{4,20}"
       title="用户名需为4-20位字母或数字" required>
```

### 4.8 `minlength` —— 密码最小长度
限制密码至少 6 位。

```html
<input type="password" name="password" minlength="6" required autocomplete="new-password">
```

### 4.9 `select` + 禁用占位选项 —— 身份下拉选择
使用原生下拉框选择「学生 / 教师」，并用 `disabled` + `selected` 的空选项强制用户主动选择。

```html
<select id="role" name="role" required>
  <option value="" disabled selected>请选择您的身份</option>
  <option value="student">学生</option>
  <option value="teacher">教师</option>
</select>
```

### 4.10 `checkbox` —— 「记住我」
登录页使用复选框实现「记住我」，默认勾选。

```html
<label class="remember">
  <input type="checkbox" name="remember" value="1" checked> 记住我
</label>
```

---

## 五、其他 HTML5 / CSS3 能力

除表单增强外，页面还应用了以下现代 Web 能力：

1. **HTML5 文档类型与语义化**：`<!DOCTYPE html>`、`<meta charset>`、`<label for>` 关联输入框、语义化 `<form>`。
2. **响应式 `viewport`**：`<meta name="viewport" content="width=device-width, initial-scale=1.0">`，卡片 `max-width: 94vw` 自适应移动端。
3. **CSS3 渐变背景**：`linear-gradient(135deg, #e0f2fe, #dbeafe, #eff6ff)` 浅蓝色氛围。
4. **圆角与阴影**：`border-radius: 16px`、`box-shadow` 营造卡片悬浮质感。
5. **过渡动画**：输入框 `transition` + `:focus` 蓝色边框与光晕高亮。
6. **`accent-color`**：原生复选框、下拉统一品牌蓝。
7. **`appearance: none` 自定义下拉箭头**：用内联 SVG data URI 替换默认箭头。
8. **`::placeholder` 伪元素**：统一占位文字颜色。
9. **无障碍**：每个输入框均有 `label` 关联，聚焦与鼠标均可用。

---

## 六、版本记录

| 版本 | 内容 | 说明 |
|------|------|------|
| v1.0 | 初版 | 完成 `login.html` 与 `register.html`，含全部表单增强特性 |
| v1.1 | 文档化 | 规范化项目结构，补充开发文档与截图目录 |

> 若后续迭代出多个过程性版本，请按 v1.0 → v1.1 → … 依次编号，并在 Gitee 用 tag / commit 区分后一并提交链接。

---

## 七、Gitee 仓库

- **仓库地址**：`https://gitee.com/<你的用户名>/<仓库名>`（待创建后填写）
- **目录结构**：

```
ai-tutor-platform/
├── index.html         # 主页（答疑对话界面）
├── login.html         # 登录页
├── register.html      # 注册页
├── README.md          # 本文档
└── screenshots/       # 多轮对话截图
```

---

*本原型仅演示前端页面与表单能力，后端接口、真实登录鉴权将在后续版本接入。*
