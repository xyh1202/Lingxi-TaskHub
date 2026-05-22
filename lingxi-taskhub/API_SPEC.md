# API_SPEC.md — 灵犀任务中台 API 说明

Base URL: `/api`

统一返回格式建议：

成功：

```json
{
  "data": {}
}
```

失败：

```json
{
  "error": {
    "message": "错误说明",
    "code": "ERROR_CODE"
  }
}
```

鉴权：

```http
Authorization: Bearer <token>
```

---

## 1. Health

### GET /health

返回：

```json
{
  "data": {
    "ok": true
  }
}
```

---

## 2. Auth

### POST /auth/register

请求：

```json
{
  "username": "guihua",
  "email": "guihua@example.com",
  "password": "12345678"
}
```

返回：

```json
{
  "data": {
    "token": "jwt-token",
    "user": {
      "id": "user-id",
      "username": "guihua",
      "email": "guihua@example.com"
    }
  }
}
```

### POST /auth/login

请求：

```json
{
  "account": "guihua",
  "password": "12345678"
}
```

说明：`account` 可以是 username 或 email。

返回同注册。

### GET /auth/me

返回：

```json
{
  "data": {
    "id": "user-id",
    "username": "guihua",
    "email": "guihua@example.com"
  }
}
```

---

## 3. Dashboard

### GET /dashboard/summary

返回：

```json
{
  "data": {
    "projectCount": 3,
    "activeProjectCount": 2,
    "completedTaskCount": 12,
    "overdueTaskCount": 1,
    "workflowLogCount": 8,
    "materialCount": 5,
    "recentProjects": [],
    "recentWorkflowLogs": []
  }
}
```

---

## 4. Projects

### GET /projects

Query：

- `status` 可选
- `keyword` 可选

返回：

```json
{
  "data": [
    {
      "id": "project-id",
      "name": "AI Mimic Town",
      "description": "AI 社交推理游戏",
      "status": "active",
      "priority": "high",
      "tags": ["AI", "Game"],
      "coverColor": "#6366f1",
      "startDate": null,
      "dueDate": null,
      "createdAt": "2026-05-22T00:00:00.000Z",
      "updatedAt": "2026-05-22T00:00:00.000Z",
      "stats": {
        "taskCount": 10,
        "doneTaskCount": 4,
        "workflowLogCount": 2,
        "materialCount": 3
      }
    }
  ]
}
```

### POST /projects

请求：

```json
{
  "name": "AI Mimic Town",
  "description": "AI 社交推理游戏",
  "status": "planning",
  "priority": "medium",
  "tags": ["AI", "Game"],
  "coverColor": "#6366f1",
  "startDate": null,
  "dueDate": null
}
```

### GET /projects/:id

返回项目详情，包含统计。

### PATCH /projects/:id

请求字段同创建，全部可选。

### DELETE /projects/:id

返回：

```json
{
  "data": {
    "success": true
  }
}
```

### GET /projects/:id/summary

返回：

```json
{
  "data": {
    "projectId": "project-id",
    "taskCount": 10,
    "doneTaskCount": 4,
    "workflowLogCount": 2,
    "materialCount": 3
  }
}
```

---

## 5. Tasks

### GET /projects/:projectId/tasks

返回：

```json
{
  "data": [
    {
      "id": "task-id",
      "projectId": "project-id",
      "title": "完成项目初始化",
      "description": "创建前后端基础结构",
      "status": "todo",
      "priority": "medium",
      "tags": ["frontend"],
      "sortOrder": 0,
      "dueDate": null,
      "createdAt": "2026-05-22T00:00:00.000Z",
      "updatedAt": "2026-05-22T00:00:00.000Z"
    }
  ]
}
```

### POST /projects/:projectId/tasks

请求：

```json
{
  "title": "完成项目初始化",
  "description": "创建前后端基础结构",
  "status": "todo",
  "priority": "medium",
  "tags": ["frontend"],
  "dueDate": null
}
```

### PATCH /tasks/:id

请求字段同创建，全部可选。

### PATCH /tasks/:id/status

请求：

```json
{
  "status": "doing"
}
```

### DELETE /tasks/:id

返回：

```json
{
  "data": {
    "success": true
  }
}
```

---

## 6. Workflow Logs

### GET /workflow-logs

Query：

- `projectId` 可选
- `actionType` 可选

返回：

```json
{
  "data": [
    {
      "id": "log-id",
      "projectId": "project-id",
      "title": "AI 生成项目策划",
      "agentName": "OpenClaw",
      "actionType": "planning",
      "inputSummary": "用户要求生成项目策划",
      "outputSummary": "生成 PROJECT_PLAN.md",
      "relatedFiles": ["PROJECT_PLAN.md"],
      "relatedCommit": "abc1234",
      "createdAt": "2026-05-22T00:00:00.000Z",
      "updatedAt": "2026-05-22T00:00:00.000Z"
    }
  ]
}
```

### POST /workflow-logs

请求：

```json
{
  "projectId": "project-id",
  "title": "AI 生成项目策划",
  "agentName": "OpenClaw",
  "actionType": "planning",
  "inputSummary": "用户要求生成项目策划",
  "outputSummary": "生成 PROJECT_PLAN.md",
  "relatedFiles": ["PROJECT_PLAN.md"],
  "relatedCommit": "abc1234"
}
```

### GET /workflow-logs/:id

返回单条日志。

### PATCH /workflow-logs/:id

请求字段同创建，全部可选。

### DELETE /workflow-logs/:id

返回 success。

---

## 7. Materials

### GET /materials

Query：

- `projectId` 可选
- `type` 可选

返回：

```json
{
  "data": [
    {
      "id": "material-id",
      "projectId": "project-id",
      "title": "项目 GitHub 地址",
      "type": "link",
      "content": "GitHub 仓库",
      "url": "https://github.com/example/repo",
      "createdAt": "2026-05-22T00:00:00.000Z",
      "updatedAt": "2026-05-22T00:00:00.000Z"
    }
  ]
}
```

### POST /materials

请求：

```json
{
  "projectId": "project-id",
  "title": "项目 GitHub 地址",
  "type": "link",
  "content": "GitHub 仓库",
  "url": "https://github.com/example/repo"
}
```

### GET /materials/:id

返回单条资料。

### PATCH /materials/:id

请求字段同创建，全部可选。

### DELETE /materials/:id

返回 success。

---

## 8. Mock AI

### POST /ai/project-summary

请求：

```json
{
  "projectId": "project-id"
}
```

返回：

```json
{
  "data": {
    "summary": "当前项目正在推进中，已建立基础任务和工作流记录。",
    "progress": "已完成 40% 的任务。",
    "nextSteps": [
      "继续完成核心开发任务",
      "补充项目资料",
      "增加更多工作流日志"
    ],
    "risks": [
      "部分任务尚未设置截止时间",
      "项目资料仍需补充"
    ]
  }
}
```

### POST /ai/workflow-proof

请求：

```json
{
  "projectId": "project-id"
}
```

返回：

```json
{
  "data": {
    "proofText": "本项目已使用 AI Agent 辅助完成项目规划、任务拆解和资料整理，产生了多条工作流日志和项目材料，可作为真实项目执行证明。"
  }
}
```

---

## 9. 状态枚举

### ProjectStatus

- planning
- active
- paused
- completed
- archived

### TaskStatus

- todo
- doing
- review
- done
- archived

### Priority

- low
- medium
- high
- urgent

### WorkflowType

- planning
- coding
- debugging
- document
- review
- deploy
- proof

### MaterialType

- text
- link
- document
- image
- terminal_log
- git_commit
