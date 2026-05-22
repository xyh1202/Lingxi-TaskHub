# 灵犀任务中台 Lingxi TaskHub — 项目策划与开发说明

> 面向个人开发者、小团队和内容创作者的智能项目管理平台。核心能力：项目管理、任务看板、资料归档、AI 工作流记录、项目摘要生成、进度统计。

---

## 1. 项目定位

### 1.1 项目名称

**灵犀任务中台 / Lingxi TaskHub**

### 1.2 一句话介绍

灵犀任务中台是一个面向个人开发者、小团队和内容创作者的智能项目管理平台，用于管理项目、任务、资料、AI Agent 工作流和项目成果证明。

### 1.3 产品目标

- 解决多项目并行时任务分散、资料混乱、进度不清晰的问题。
- 帮助用户沉淀 AI Agent 参与项目的过程记录和成果材料。
- 提供轻量、清晰、可扩展的项目执行工作台。
- 后续支持 AI 摘要、周报、复盘、项目证明材料自动生成。

### 1.4 合规边界

本项目是正向效率工具，不涉及：

- 刷量
- 刷单
- 套利
- 违规引流
- 虚假交易
- 账号买卖
- 批量注册
- 非法采集
- 绕过平台规则
- 侵犯用户隐私

所有功能围绕真实项目管理、任务协作、文档整理和 AI 辅助办公展开。

---

## 2. 用户画像

### 2.1 个人开发者

需求：

- 管理多个 side project。
- 记录开发计划、代码提交、终端日志、部署记录。
- 用 AI 生成项目策划、README、技术方案、接口文档。

### 2.2 小型团队

需求：

- 管理项目进度。
- 看板协作。
- 成员任务分配。
- 项目资料统一存放。

### 2.3 内容创作者 / 运营人员

需求：

- 管理选题、脚本、素材、发布计划。
- 记录 AI 生成过程。
- 自动生成阶段总结和成果展示。

---

## 3. 核心功能

### 3.1 用户系统

- 注册
- 登录
- 退出登录
- 当前用户信息
- JWT 鉴权
- 基础用户设置

MVP 阶段只做邮箱/用户名 + 密码登录即可。

### 3.2 项目管理

用户可以创建多个项目，每个项目包含：

- 项目名称
- 项目简介
- 项目状态
- 项目优先级
- 项目标签
- 开始时间
- 截止时间
- 项目负责人
- 项目封面色

项目状态：

- planning：规划中
- active：进行中
- paused：暂停
- completed：已完成
- archived：已归档

### 3.3 任务看板

每个项目下有任务列表。

任务字段：

- 标题
- 描述
- 状态
- 优先级
- 截止时间
- 负责人
- 标签
- 排序值

任务状态：

- todo：待开始
- doing：进行中
- review：待确认
- done：已完成
- archived：已归档

### 3.4 项目资料归档

资料类型：

- 文档
- 图片
- 截图
- 终端日志
- Git 提交记录
- 演示链接
- 外部链接
- API 文档
- 复盘报告

MVP 阶段先支持：

- 文本资料
- 链接资料
- 截图/文件上传可以后置

### 3.5 AI 工作流日志

这是项目特色功能。

用于记录 AI Agent 在项目里的参与过程，例如：

- 生成项目策划
- 拆分开发任务
- 生成代码
- 修复 bug
- 生成终端截图
- 输出 README
- 生成复盘文档

日志字段：

- 所属项目
- 标题
- Agent 名称
- 操作类型
- 输入摘要
- 输出摘要
- 关联文件
- 关联 commit
- 创建时间

操作类型：

- planning：策划
- coding：代码生成
- debugging：调试
- document：文档生成
- review：代码审查
- deploy：部署
- proof：证明材料

### 3.6 AI 摘要与复盘

MVP 先做“占位接口 + Mock 返回”。

后续接入 LLM 后支持：

- 项目摘要
- 周报
- 复盘报告
- 项目证明材料
- 下一步建议
- 风险提醒

### 3.7 数据统计

仪表盘展示：

- 项目总数
- 进行中项目数
- 已完成任务数
- 逾期任务数
- AI 工作流日志数
- 最近活动

---

## 4. MVP 范围

第一版不要做太大，先做闭环。

### 4.1 必须做

- 用户登录/注册
- 仪表盘
- 项目列表
- 创建项目
- 项目详情
- 任务看板
- 创建/编辑任务
- AI 工作流日志列表
- 新增 AI 工作流日志
- 项目资料列表
- 新增链接/文本资料
- Mock AI 摘要按钮

### 4.2 暂时不做

- 多人团队
- 复杂权限
- 文件上传
- 在线编辑器
- 真实 AI 接口
- 支付
- 模板市场
- 移动端 App

---

## 5. 技术架构

### 5.1 推荐技术栈

前端：

- React
- TypeScript
- Vite
- TailwindCSS
- React Router
- Zustand
- TanStack Query
- Lucide React 图标库

后端：

- Node.js
- Fastify 或 Express
- TypeScript
- Prisma ORM
- SQLite（MVP）
- PostgreSQL（后续生产）
- JWT 鉴权
- Zod 参数校验

### 5.2 MVP 推荐选择

为了让 Codex 快速写出来：

- 前端：React + TypeScript + Vite + TailwindCSS
- 后端：Express + TypeScript + Prisma + SQLite
- Monorepo：frontend / backend 两个目录

---

## 6. 推荐目录结构

```text
lingxi-taskhub/
  README.md
  PROJECT_PLAN.md
  CODEX_TASKS.md
  API_SPEC.md
  .gitignore
  docker-compose.yml

  frontend/
    package.json
    index.html
    vite.config.ts
    tsconfig.json
    tailwind.config.js
    postcss.config.js
    src/
      main.tsx
      App.tsx
      index.css
      routes/
        AppRouter.tsx
      pages/
        LoginPage.tsx
        RegisterPage.tsx
        DashboardPage.tsx
        ProjectsPage.tsx
        ProjectDetailPage.tsx
        WorkflowLogsPage.tsx
        MaterialsPage.tsx
        SettingsPage.tsx
      components/
        layout/
          AppLayout.tsx
          Sidebar.tsx
          Topbar.tsx
        common/
          Button.tsx
          Card.tsx
          Input.tsx
          Modal.tsx
          Badge.tsx
          EmptyState.tsx
        projects/
          ProjectCard.tsx
          ProjectForm.tsx
          ProjectStats.tsx
        tasks/
          TaskBoard.tsx
          TaskColumn.tsx
          TaskCard.tsx
          TaskForm.tsx
        workflow/
          WorkflowLogCard.tsx
          WorkflowLogForm.tsx
        materials/
          MaterialCard.tsx
          MaterialForm.tsx
      hooks/
        useAuth.ts
        useProjects.ts
        useTasks.ts
        useWorkflowLogs.ts
      services/
        apiClient.ts
        authApi.ts
        projectApi.ts
        taskApi.ts
        workflowApi.ts
        materialApi.ts
      store/
        authStore.ts
      types/
        auth.ts
        project.ts
        task.ts
        workflow.ts
        material.ts
      utils/
        formatDate.ts
        constants.ts

  backend/
    package.json
    tsconfig.json
    prisma/
      schema.prisma
      seed.ts
    src/
      server.ts
      app.ts
      config/
        env.ts
      plugins/
        prisma.ts
        auth.ts
      middleware/
        errorHandler.ts
        requireAuth.ts
      routes/
        auth.routes.ts
        project.routes.ts
        task.routes.ts
        workflow.routes.ts
        material.routes.ts
        ai.routes.ts
      controllers/
        auth.controller.ts
        project.controller.ts
        task.controller.ts
        workflow.controller.ts
        material.controller.ts
        ai.controller.ts
      services/
        auth.service.ts
        project.service.ts
        task.service.ts
        workflow.service.ts
        material.service.ts
        ai.service.ts
      schemas/
        auth.schema.ts
        project.schema.ts
        task.schema.ts
        workflow.schema.ts
        material.schema.ts
      utils/
        password.ts
        jwt.ts
        logger.ts
```

---

## 7. 前端页面设计

### 7.1 登录页

路径：`/login`

功能：

- 用户名/邮箱输入
- 密码输入
- 登录按钮
- 跳转注册
- 错误提示

### 7.2 注册页

路径：`/register`

功能：

- 用户名
- 邮箱
- 密码
- 确认密码
- 注册按钮

### 7.3 仪表盘

路径：`/dashboard`

展示：

- 项目总数
- 进行中项目
- 已完成任务
- AI 工作流日志数
- 最近项目
- 最近活动

### 7.4 项目列表页

路径：`/projects`

功能：

- 项目卡片列表
- 创建项目按钮
- 状态筛选
- 标签筛选
- 搜索项目

### 7.5 项目详情页

路径：`/projects/:projectId`

模块：

- 项目基本信息
- 项目统计
- 任务看板
- AI 工作流日志
- 项目资料
- AI 摘要按钮

### 7.6 任务看板

看板列：

- 待开始
- 进行中
- 待确认
- 已完成

MVP 可以先不用拖拽，用按钮切换状态。

### 7.7 AI 工作流日志页

路径：`/workflow-logs`

功能：

- 日志列表
- 按项目筛选
- 按操作类型筛选
- 新增日志
- 查看日志详情

### 7.8 项目资料页

路径：`/materials`

功能：

- 资料列表
- 按项目筛选
- 新增文本资料
- 新增链接资料

---

## 8. 后端模块设计

### 8.1 Auth 模块

接口：

- `POST /api/auth/register`
- `POST /api/auth/login`
- `GET /api/auth/me`

职责：

- 密码加密
- JWT 签发
- 用户鉴权

### 8.2 Project 模块

接口：

- `GET /api/projects`
- `POST /api/projects`
- `GET /api/projects/:id`
- `PATCH /api/projects/:id`
- `DELETE /api/projects/:id`
- `GET /api/projects/:id/summary`

职责：

- 项目 CRUD
- 项目统计
- 项目摘要

### 8.3 Task 模块

接口：

- `GET /api/projects/:projectId/tasks`
- `POST /api/projects/:projectId/tasks`
- `PATCH /api/tasks/:id`
- `DELETE /api/tasks/:id`
- `PATCH /api/tasks/:id/status`

职责：

- 任务 CRUD
- 任务状态流转
- 看板数据

### 8.4 Workflow 模块

接口：

- `GET /api/workflow-logs`
- `POST /api/workflow-logs`
- `GET /api/workflow-logs/:id`
- `PATCH /api/workflow-logs/:id`
- `DELETE /api/workflow-logs/:id`

职责：

- AI 工作流日志记录
- 按项目筛选
- 按类型筛选

### 8.5 Material 模块

接口：

- `GET /api/materials`
- `POST /api/materials`
- `GET /api/materials/:id`
- `PATCH /api/materials/:id`
- `DELETE /api/materials/:id`

职责：

- 项目资料归档
- 文本/链接资料管理

### 8.6 AI 模块

MVP 用 Mock。

接口：

- `POST /api/ai/project-summary`
- `POST /api/ai/workflow-proof`

返回内容：

- 项目摘要
- 当前进度
- 已完成事项
- 下一步建议
- 可对外展示的证明文案

---

## 9. 数据模型

### 9.1 User

```prisma
model User {
  id           String   @id @default(cuid())
  username     String   @unique
  email        String   @unique
  passwordHash String
  createdAt    DateTime @default(now())
  updatedAt    DateTime @updatedAt

  projects     Project[]
  tasks        Task[]
  workflowLogs WorkflowLog[]
  materials    Material[]
}
```

### 9.2 Project

```prisma
model Project {
  id          String        @id @default(cuid())
  ownerId     String
  name        String
  description String
  status      ProjectStatus @default(planning)
  priority    Priority      @default(medium)
  tags        String        @default("[]")
  coverColor  String        @default("#6366f1")
  startDate   DateTime?
  dueDate     DateTime?
  createdAt   DateTime      @default(now())
  updatedAt   DateTime      @updatedAt

  owner        User          @relation(fields: [ownerId], references: [id])
  tasks        Task[]
  workflowLogs WorkflowLog[]
  materials    Material[]
}
```

### 9.3 Task

```prisma
model Task {
  id          String     @id @default(cuid())
  projectId   String
  assigneeId  String?
  title       String
  description String?
  status      TaskStatus @default(todo)
  priority    Priority   @default(medium)
  tags        String     @default("[]")
  sortOrder   Int        @default(0)
  dueDate     DateTime?
  createdAt   DateTime   @default(now())
  updatedAt   DateTime   @updatedAt

  project  Project @relation(fields: [projectId], references: [id], onDelete: Cascade)
  assignee User?   @relation(fields: [assigneeId], references: [id])
}
```

### 9.4 WorkflowLog

```prisma
model WorkflowLog {
  id             String          @id @default(cuid())
  projectId      String
  userId         String
  title          String
  agentName      String?
  actionType     WorkflowType
  inputSummary   String?
  outputSummary  String
  relatedFiles   String          @default("[]")
  relatedCommit  String?
  createdAt      DateTime        @default(now())
  updatedAt      DateTime        @updatedAt

  project Project @relation(fields: [projectId], references: [id], onDelete: Cascade)
  user    User    @relation(fields: [userId], references: [id])
}
```

### 9.5 Material

```prisma
model Material {
  id          String       @id @default(cuid())
  projectId   String
  userId      String
  title       String
  type        MaterialType
  content     String
  url         String?
  createdAt   DateTime     @default(now())
  updatedAt   DateTime     @updatedAt

  project Project @relation(fields: [projectId], references: [id], onDelete: Cascade)
  user    User    @relation(fields: [userId], references: [id])
}
```

### 9.6 Enums

```prisma
enum ProjectStatus {
  planning
  active
  paused
  completed
  archived
}

enum TaskStatus {
  todo
  doing
  review
  done
  archived
}

enum Priority {
  low
  medium
  high
  urgent
}

enum WorkflowType {
  planning
  coding
  debugging
  document
  review
  deploy
  proof
}

enum MaterialType {
  text
  link
  document
  image
  terminal_log
  git_commit
}
```

---

## 10. 前端开发原则

- 页面先跑通，不追求复杂动画。
- 组件小而清晰。
- API 请求集中放到 `services/`。
- 类型集中放到 `types/`。
- 登录态用 Zustand 管理。
- 服务端数据用 TanStack Query 管理。
- TailwindCSS 做干净现代的 SaaS 风格。
- 所有表单都要有基础校验和错误提示。

---

## 11. 后端开发原则

- 所有接口都必须鉴权，除了注册和登录。
- 所有参数用 Zod 校验。
- 不允许用户访问不属于自己的项目数据。
- 密码必须 bcrypt 加密。
- JWT Secret 从环境变量读取。
- 错误统一返回 JSON。
- Prisma schema 是数据源头。
- MVP 阶段 AI 接口先返回 mock 文案。

---

## 12. UI 风格

关键词：

- 干净
- 现代
- 类 Linear / Notion / Vercel
- 深浅色先做浅色
- 卡片式布局
- 侧边栏导航
- 紫蓝色作为主色

推荐主色：

- primary：`#6366f1`
- background：`#f8fafc`
- card：`#ffffff`
- text：`#0f172a`
- muted：`#64748b`

---

## 13. 第一版验收标准

当以下功能能跑通，就算 MVP 完成：

1. 用户可以注册、登录。
2. 登录后进入仪表盘。
3. 用户可以创建项目。
4. 用户可以进入项目详情页。
5. 用户可以创建任务，并切换任务状态。
6. 用户可以新增 AI 工作流日志。
7. 用户可以新增项目资料。
8. 项目详情页能展示任务、日志、资料。
9. 点击 AI 摘要按钮，可以得到一段 mock 项目总结。
10. 前后端本地启动无报错。

---

## 14. 后续迭代方向

### 14.1 AI 增强

- 接入真实 LLM。
- 根据项目数据生成周报。
- 根据工作流日志生成证明材料。
- 自动整理终端日志。

### 14.2 团队协作

- 团队空间。
- 邀请成员。
- 项目权限。
- 评论系统。

### 14.3 文件系统

- 文件上传。
- 图片预览。
- 附件分类。
- 对象存储。

### 14.4 商业化

- 免费版。
- Pro 版。
- 团队版。
- AI 额度包。
- 私有化部署。

---

## 15. 给 Codex 的总任务说明

请基于本文档实现一个完整 MVP：

- 使用 monorepo：`frontend` + `backend`。
- 前端使用 React + TypeScript + Vite + TailwindCSS。
- 后端使用 Express + TypeScript + Prisma + SQLite。
- 实现注册登录、项目管理、任务看板、工作流日志、项目资料、Mock AI 摘要。
- 保证代码结构清晰、类型完整、接口可用、本地可运行。
- 先完成最小可用版本，不做过度设计。
