---
name: axure_faster_skill
description: 编写和扩展类似 Axure 原型页面的开发规范，包括导航菜单注册、无刷新页面切换以及使用一对一便签组件说明系统（禁止使用 Emoji）。
---

# 原型框架开发规范 (Axure-like Workflow)

在处理原型开发任务时，必须严格遵守以下规范：

## 0. 脚手架初始化
- 如果用户要求“初始化脚手架”或当前工作区没有 `index.html` 框架，请将本 Skill 目录下 `template/` 文件夹中的所有文件和文件夹复制到用户工作区的根目录，作为开发基础。

## 1. 页面创建与无刷新切换
- **框架结构**：`index.html` 作为类似 Axure 的外层主框架工作区，其中 `<div id="main-frame">` 用于动态承载所有子页面的内容。
- **独立文件**：每个新原型页面应作为独立的 HTML 文件编写（如 `login.html`）。
- **导航栏注册**：新增页面后，**必须**在 `index.html` 的顶部导航菜单（`<div class="nav-links" id="nav-pages">`）中添加对应的入口。必须使用 HTMX 属性实现加载：
  ```html
  <a href="#" class="nav-link" hx-get="新页面.html" hx-target="#main-frame" hx-swap="innerHTML" onclick="document.querySelectorAll('.nav-link').forEach(l=>l.classList.remove('active')); this.classList.add('active');">页面名称</a>
  ```

## 2. 组件说明便签系统 (Sticky Notes)
为了方便阐述页面原型中各组件的交互和逻辑，本脚手架提供了一套自动化的便签连线系统：
- **精准绑定（一对一对应）**：每一个需要说明的组件必须拥有一个独立且唯一的 `id` 属性（例如 `id="btn-submit"`）。同时，**必须**添加 `data-task-id` 属性来记录任务定义的专属编码（例如 `data-task-id="A1"`）。
- **便签编写**：在对应的子页面 HTML 文件最底部，使用带有 `data-target` 属性的 `.sticky-note` 容器来编写说明，指向组件的 HTML `id`：
  ```html
  <!-- 组件本体 -->
  <button id="btn-submit" data-task-id="A1">提交</button>

  <!-- 便签本体 -->
  <div class="sticky-note fade-in" data-target="btn-submit">
      <h4>提交按钮</h4>
      <p>点击之后提交用户信息到服务端进行校验。</p>
  </div>
  ```
- **自动显示任务 ID**：底层系统会自动读取目标组件上的 `data-task-id`，并将其作为一个醒目的徽标（Badge）自动注入并显示在便签的标题旁边！同时，鼠标悬浮在组件上时，悬浮提示框也会优先显示这个任务编码（例如 `#A1`）。
- **自动机制说明**：无需手动处理样式排版、连线和生命周期清理。底层 JS 会自动收集当前页面的便签，根据组件的屏幕位置智能停靠在左侧或右侧的固定栏中，并使用灰色的折线虚线将便签和真实组件精准相连；在 HTMX 页面切换前，系统会自动清空旧便签，确保便签绝对不会在页面间跨域累积。鼠标悬浮在任意组件上可快速查看组件 ID，方便快速提取目标 ID。

## 3. 视觉规范：禁止使用 Emoji
- 无论是页面的标题、按钮文本，还是便签内部的说明文字，**全局严格禁止使用任何 Emoji 表情符号**（例如绝对不可出现 🚀、📝 等符号）。界面需始终保持纯正、严肃的设计风格。
