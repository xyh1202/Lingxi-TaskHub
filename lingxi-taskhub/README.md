# 灵犀任务中台 Lingxi TaskHub

面向个人开发者、小团队和内容创作者的智能项目管理平台。

## 核心能力

- 项目管理
- 任务看板
- 项目资料归档
- AI 工作流日志
- Mock AI 摘要
- 项目证明文案生成

## 技术栈

### Frontend

- React
- TypeScript
- Vite
- TailwindCSS
- React Router
- Zustand
- TanStack Query

### Backend

- Node.js
- Express
- TypeScript
- Prisma
- SQLite
- JWT
- bcryptjs
- Zod

## 文档

- `PROJECT_PLAN.md`：完整项目策划与开发说明
- `CODEX_TASKS.md`：给 Codex 的分阶段开发任务单
- `API_SPEC.md`：后端 API 与数据结构说明

## 推荐开发方式

把 `CODEX_TASKS.md` 分阶段交给 Codex，不要一次性让它写完整项目。

建议顺序：

1. 项目初始化
2. 数据库和后端基础
3. 鉴权模块
4. 前端布局和仪表盘
5. 项目管理模块
6. 任务看板模块
7. AI 工作流日志模块
8. 项目资料模块
9. Mock AI 摘要模块
10. 打磨和构建

## MVP 验收标准

- 用户可以注册、登录。
- 登录后进入仪表盘。
- 用户可以创建项目。
- 用户可以进入项目详情页。
- 用户可以创建任务，并切换任务状态。
- 用户可以新增 AI 工作流日志。
- 用户可以新增项目资料。
- 项目详情页能展示任务、日志、资料。
- 点击 AI 摘要按钮，可以得到一段 mock 项目总结。
- 前后端本地启动无报错。
