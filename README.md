# AI Axure Faster Skill (axure_faster_skill)

> 这是一个专门提供给 AI 智能体（如 Claude Code、Gemini、Antigravity CLI）安装和使用的 **Skill（技能包）**。

通过安装此 Skill，你的 AI 助手将学会如何利用底层自带的 HTML/CSS/HTMX 极简脚手架，以**零构建、无刷新、自带领航线便签系统**的方式，为你快速生成类似 Axure 体验的高保真交互原型。

![UI Preview](./template/assets/preview.jpg)

## 📦 这个 Skill 里包含什么？

- `SKILL.md`: 核心！这是写给 AI 智能体看的“系统指令”。里面严格定义了 AI 在生成组件时如何使用 HTMX 进行无刷新路由、如何挂载 `data-task-id` 并在底部编写自动化说明便签。
- `template/`: 脚手架模板文件夹。当 AI 被要求初始化项目时，它会将这里的 `index.html` 外壳框架、内置好的 Vanilla CSS、路由逻辑以及相关的演示页面一并复制到你的工作区。

## 🚀 如何安装和使用

如果你使用的是支持自定义技能集的 Agent 系统（如 Antigravity）：
1. 将此仓库克隆到你工作区的对应技能池中：
   ```bash
   git clone https://github.com/wangchangwei/axure_faster_skill.git .agents/skills/axure_faster_skill
   ```
2. 启动你的 Agent，它将自动识别并加载 `SKILL.md` 的能力。
3. 对你的 Agent 说：
   > “请使用 `axure_faster_skill` 帮我初始化一个原型脚手架，并新建一个商品列表页面，列出商品图片、标题和加入购物车按钮。”
4. Agent 会自动拷贝模板、注册导航、编写带有 `data-task-id` 的组件并连好说明便签！

## ✨ 核心特性体验（模板效果）

如果成功生成了页面，你可以通过内置的 npm 命令快速启动预览：
```bash
npm start
# 默认服务将在 http://localhost:7788 启动
```
- **一对一便签**：所有的页面说明便签都会自动分布在屏幕左右侧，并有完美的折线与组件相连。
- **任务编号提示**：将鼠标悬浮在组件上即可弹出分配的业务 ID，且便签上会自动生成精美的 ID Badge。
- **动态无刷新**：页面的流转体验非常顺滑。
