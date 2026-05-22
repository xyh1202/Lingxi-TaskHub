# CODEX_TASKS.md — 灵犀任务中台 Codex 开发任务单

> 目标：让 Codex 按阶段开发，不要一次性乱写。每个阶段完成后运行测试或构建。

---

## 总要求

请实现一个名为 **灵犀任务中台 Lingxi TaskHub** 的项目管理平台 MVP。

技术栈：

- 前端：React + TypeScript + Vite + TailwindCSS
- 后端：Express + TypeScript + Prisma + SQLite
- 鉴权：JWT + bcrypt
- 参数校验：Zod

目录结构：

```text
projects/lingxi-taskhub/
  frontend/
  backend/
  PROJECT_PLAN.md
  CODEX_TASKS.md
  API_SPEC.md
```

开发原则：

- 先跑通 MVP，不做复杂动画和过度抽象。
- 每个模块单独拆文件。
- 前后端类型清晰。
- 所有接口返回统一 JSON。
- 所有登录后接口都要校验 JWT。
- 用户只能访问自己的数据。

---

## 阶段 1：项目初始化

### 1.1 初始化前端

在 `frontend/` 中创建 Vite React TypeScript 项目。

安装依赖：

```bash
npm install react react-dom react-router-dom zustand @tanstack/react-query lucide-react
npm install -D typescript vite @vitejs/plugin-react tailwindcss postcss autoprefixer @types/react @types/react-dom
```

配置：

- TailwindCSS
- React Router
- TanStack Query Provider
- 基础全局样式

### 1.2 初始化后端

在 `backend/` 中创建 Node TypeScript 项目。

安装依赖：

```bash
npm install express cors dotenv jsonwebtoken bcryptjs zod @prisma/client
npm install -D typescript tsx prisma @types/node @types/express @types/cors @types/jsonwebtoken @types/bcryptjs
```

配置：

- `tsconfig.json`
- `src/server.ts`
- `src/app.ts`
- `.env.example`
- Prisma SQLite

### 1.3 验收

运行：

```bash
cd frontend && npm run build
cd backend && npm run dev
```

要求：

- 前端可构建。
- 后端 `/api/health` 返回 `{ "ok": true }`。

---

## 阶段 2：数据库和后端基础

### 2.1 Prisma Schema

实现以下模型：

- User
- Project
- Task
- WorkflowLog
- Material

实现以下枚举：

- ProjectStatus
- TaskStatus
- Priority
- WorkflowType
- MaterialType

执行：

```bash
npx prisma migrate dev --name init
npx prisma generate
```

### 2.2 基础插件/工具

实现：

- Prisma client 单例
- env 配置读取
- JWT 工具
- 密码 hash/compare 工具
- errorHandler
- requireAuth middleware

### 2.3 验收

- 数据库文件生成成功。
- Prisma Client 可正常调用。
- TypeScript 无类型错误。

---

## 阶段 3：鉴权模块

### 3.1 后端接口

实现：

- `POST /api/auth/register`
- `POST /api/auth/login`
- `GET /api/auth/me`

要求：

- 注册时 username/email 唯一。
- 密码使用 bcryptjs 加密。
- 登录成功返回 token 和 user。
- `/me` 根据 token 返回当前用户。

### 3.2 前端页面

实现：

- `/login`
- `/register`

功能：

- 表单输入。
- 调用后端接口。
- 保存 token。
- 登录成功跳转 `/dashboard`。

### 3.3 验收

- 可以注册。
- 可以登录。
- 刷新页面仍保持登录态。
- 未登录访问业务页面跳转登录。

---

## 阶段 4：前端布局和仪表盘

### 4.1 AppLayout

实现：

- Sidebar
- Topbar
- 主内容区域
- 退出登录按钮

导航：

- 仪表盘
- 项目
- 工作流日志
- 项目资料
- 设置

### 4.2 DashboardPage

展示统计卡片：

- 项目总数
- 进行中项目
- 已完成任务
- 工作流日志数

展示最近项目和最近活动。

### 4.3 后端统计接口

可放在：

- `GET /api/dashboard/summary`

如果不想新增模块，也可以前端从项目/任务/日志接口组合统计。

### 4.4 验收

- 登录后看到完整布局。
- 侧边栏可切换页面。
- 仪表盘无报错。

---

## 阶段 5：项目管理模块

### 5.1 后端接口

实现：

- `GET /api/projects`
- `POST /api/projects`
- `GET /api/projects/:id`
- `PATCH /api/projects/:id`
- `DELETE /api/projects/:id`

要求：

- 只能操作自己的项目。
- 支持按状态筛选。
- 删除项目时级联删除任务、日志、资料。

### 5.2 前端页面

实现：

- `ProjectsPage`
- `ProjectDetailPage`
- `ProjectCard`
- `ProjectForm`

功能：

- 项目列表。
- 创建项目。
- 编辑项目。
- 删除项目。
- 进入项目详情。

### 5.3 验收

- 可以创建项目。
- 项目列表能展示。
- 可以进入详情页。
- 可以修改和删除项目。

---

## 阶段 6：任务看板模块

### 6.1 后端接口

实现：

- `GET /api/projects/:projectId/tasks`
- `POST /api/projects/:projectId/tasks`
- `PATCH /api/tasks/:id`
- `DELETE /api/tasks/:id`
- `PATCH /api/tasks/:id/status`

要求：

- 只能访问自己项目下的任务。
- 支持状态切换。

### 6.2 前端组件

实现：

- `TaskBoard`
- `TaskColumn`
- `TaskCard`
- `TaskForm`

MVP 不需要拖拽，使用按钮切换状态：

- 移到待开始
- 移到进行中
- 移到待确认
- 标记完成

### 6.3 验收

- 项目详情页能看到任务看板。
- 可以新增任务。
- 可以切换任务状态。
- 可以删除任务。

---

## 阶段 7：AI 工作流日志模块

### 7.1 后端接口

实现：

- `GET /api/workflow-logs`
- `POST /api/workflow-logs`
- `GET /api/workflow-logs/:id`
- `PATCH /api/workflow-logs/:id`
- `DELETE /api/workflow-logs/:id`

支持 query：

- `projectId`
- `actionType`

### 7.2 前端页面/组件

实现：

- `WorkflowLogsPage`
- `WorkflowLogCard`
- `WorkflowLogForm`

字段：

- 标题
- 项目
- Agent 名称
- 操作类型
- 输入摘要
- 输出摘要
- 关联文件
- 关联 commit

### 7.3 验收

- 可以新增工作流日志。
- 可以按项目筛选。
- 项目详情页展示该项目日志。

---

## 阶段 8：项目资料模块

### 8.1 后端接口

实现：

- `GET /api/materials`
- `POST /api/materials`
- `GET /api/materials/:id`
- `PATCH /api/materials/:id`
- `DELETE /api/materials/:id`

支持 query：

- `projectId`
- `type`

### 8.2 前端页面/组件

实现：

- `MaterialsPage`
- `MaterialCard`
- `MaterialForm`

MVP 支持两类：

- text
- link

### 8.3 验收

- 可以新增资料。
- 可以按项目筛选资料。
- 项目详情页展示资料。

---

## 阶段 9：Mock AI 摘要模块

### 9.1 后端接口

实现：

- `POST /api/ai/project-summary`
- `POST /api/ai/workflow-proof`

`project-summary` 输入：

```json
{
  "projectId": "xxx"
}
```

返回：

```json
{
  "summary": "...",
  "progress": "...",
  "nextSteps": ["..."],
  "risks": ["..."]
}
```

`workflow-proof` 输入：

```json
{
  "projectId": "xxx"
}
```

返回：

```json
{
  "proofText": "..."
}
```

### 9.2 前端功能

在项目详情页加按钮：

- 生成项目摘要
- 生成项目证明文案

弹窗展示结果。

### 9.3 验收

- 点击按钮能拿到 mock 文案。
- 文案包含项目名称、任务数、日志数、资料数。

---

## 阶段 10：打磨和构建

### 10.1 前端打磨

- 空状态。
- Loading 状态。
- 错误提示。
- 表单校验。
- 移动端基础适配。

### 10.2 后端打磨

- 统一错误格式。
- 404 处理。
- CORS 配置。
- `.env.example`。
- seed 数据。

### 10.3 文档

更新 README：

- 项目介绍。
- 技术栈。
- 本地启动。
- 环境变量。
- API 简介。
- MVP 功能列表。

### 10.4 最终验收命令

```bash
cd backend
npm install
npx prisma migrate dev
npm run dev

cd ../frontend
npm install
npm run build
npm run dev
```

---

## Codex 注意事项

1. 不要把所有代码写进一个文件。
2. 不要跳过鉴权。
3. 不要让用户访问别人的数据。
4. 不要接真实 AI API，MVP 先 mock。
5. 不要做复杂拖拽，先按钮切换状态。
6. 保持 UI 干净，使用 TailwindCSS。
7. 每个阶段完成后先构建或运行类型检查。
