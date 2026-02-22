# Task Template（任务模板）

以下模板用于 implementation-planning workflow 的 Step 5（任务拆解）。目标是产出可被后续的 agent 解析、可被 LLM coding agent 落地实现的细粒度任务。

## 任务粒度标准（必须满足）

- **单会话可完成**：一个 LLM agent 在一个 session 内可完成（包含 TDD 循环 + 可能的 debug 时间）
- **独立可验证**：完成后可以通过自动化方式验证（测试通过 / lint 通过 / 可运行）
- **文件影响可控**：建议影响文件数 \(create + modify + test\) ≤ 5–8
- **边界清晰**：描述足够自包含；不要求后续开发代码时阅读完整的 design doc 才能开工
- **Plan 只写 AC，不写测试**：验收标准定义"什么算完成"；测试设计由开发时决定

## 文件清单规则

文件清单帮助后续开发 agent 明确每个任务的影响范围：

- **必须列出**此 task 会创建/修改/新增测试的文件路径
- **不得过宽**：避免 `src/**` 这种不可执行的清单
- **相对路径**：路径相对项目根目录
- **分三类**：`Create` / `Modify` / `Test`

## 验收标准（AC）写法要求

- **可观察、可验证**：读者能明确知道如何证明它成立
- **一条 AC 一件事**：避免一个 AC 里写多个行为（出现 "and/以及/同时" 就要考虑拆分）
- **覆盖错误路径**：至少包含 1 条失败/边界条件（如：非法输入、权限不足、网络失败等）
- **避免实现细节**：不要规定"用某某库/某某 hook"，而要规定"对用户可见的行为/输出"

推荐格式：
- 行为描述（简洁）或 Given-When-Then
- 使用 checkbox 便于追踪

---

## 任务模板（Markdown）

```markdown
### TASK-001: <任务标题>

**优先级**: P0 | P1 | P2
**依赖**: 无 | TASK-002, TASK-003
**对应 User Story**: US-001 | null

**描述**:
用 5–12 行写清楚要做什么、为什么要做（与 design doc 的目标/约束对齐）、完成后能带来什么能力。

**文件清单**:
- Create:
  - `path/to/new_file.ext` — 为什么需要它 / 放这里的理由
- Modify:
  - `path/to/existing_file.ext` — 改动点概述（别写实现细节）
- Test:
  - `tests/path/to/test_file.ext` — 覆盖哪些 AC（粗粒度描述即可）

**验收标准**:
- [ ] AC1: <可验证的行为/输出>
- [ ] AC2: <边界/错误路径>
- [ ] AC3: <非功能性要求（可选）>

**技术备注**:
- 需要遵循的 ADR：ADR-00X
- 需要复用的目录/模块：`src/...`
- 重要约束：性能/安全/兼容性/日志字段等
```

---

## 好任务 vs 坏任务（示例）

### 好任务（边界清晰、可验证）

```markdown
### TASK-007: 前端脚手架与路由搭建
**优先级**: P1
**依赖**: 无
**对应 User Story**: US-003（用户可以通过 URL 直接访问各功能页面）

**描述**:
搭建前端项目基础路由结构。使用 React Router v6 配置 `/dashboard`、`/settings`、`/login` 三条路由，并为每条路由创建占位页面组件。
完成后，团队可以在各路由下独立开发页面功能，不会互相阻塞。

**文件清单**:
- Create:
  - `src/router/index.tsx` — 集中定义路由表，便于后续扩展
  - `src/pages/Dashboard.tsx` — Dashboard 占位页面
  - `src/pages/Settings.tsx` — Settings 占位页面
  - `src/pages/Login.tsx` — Login 占位页面
- Modify:
  - `src/App.tsx` — 将 RouterProvider 挂载到应用根节点
- Test:
  - `src/router/__tests__/router.test.tsx` — 覆盖 AC1–AC3

**验收标准**:
- [ ] AC1: 访问 `/dashboard`、`/settings`、`/login` 分别渲染对应占位页面，页面标题包含路由名称
- [ ] AC2: 访问不存在的路径（如 `/xyz`）时显示 404 页面，不产生白屏
- [ ] AC3: `npm run build` 无报错，构建产物可正常加载

**技术备注**:
- 使用 createBrowserRouter（React Router v6 data API），为后续 loader/action 做准备
- 404 页面使用 `errorElement`，不单独建路由
```

好的地方：
- **文件清单**明确（创建路由文件、修改入口、补测试）
- **AC** 可自动验证（页面可访问、路由切换、构建通过）
- 不依赖后端实现细节，边界清晰

### 坏任务（不可执行、不可验证）

```markdown
### TASK-003: 实现后端 API

**优先级**: P0
**依赖**: TASK-001, TASK-002
**对应 User Story**: US-001, US-002, US-003

**描述**:
实现后端所有 API，包括用户注册/登录、文件上传、截图生成、权限管理等功能。

**文件清单**:
- Create:
  - `src/api/**` — 所有 API 路由
  - `src/models/**` — 数据模型
- Modify:
  - `src/app.ts` — 注册路由
- Test:
  - `tests/**` — API 测试

**验收标准**:
- [ ] AC1: 所有 API 可正常调用
- [ ] AC2: 鉴权逻辑正确
- [ ] AC3: 错误处理完善

**技术备注**:
- 使用 Express + Prisma
```

问题分析：
- **范围过大**：用户注册、文件上传、截图、权限——至少 4 个独立功能塞进一个 task
- **文件清单用了通配符**（`src/api/**`、`tests/**`），无法明确影响范围
- **AC 不可验证**："所有 API 可正常调用"——哪些 API？什么算"正常"？"错误处理完善"——完善到什么程度？
- **依赖和 User Story 堆叠**：一个 task 关联多个 US，说明它在做多件事

修复方式：按接口契约拆成独立 task。以"用户注册"为例：

```markdown
### TASK-003: 用户注册 API

**优先级**: P0
**依赖**: TASK-001（数据库 schema 初始化）
**对应 User Story**: US-001（新用户可以注册账号）

**描述**:
实现 `POST /api/auth/register` 接口。接收 email + password，校验格式，
hash 密码后写入 users 表，返回 201 + user 对象（不含密码）。
邮箱已存在时返回 409。

**文件清单**:
- Create:
  - `src/api/auth/register.ts` — 注册路由处理函数
  - `src/services/user.service.ts` — 用户创建逻辑，密码 hash
- Modify:
  - `src/api/auth/index.ts` — 挂载 register 路由
- Test:
  - `tests/api/auth/register.test.ts` — 覆盖 AC1–AC3

**验收标准**:
- [ ] AC1: POST /api/auth/register 传入合法 email + password（≥8 位），返回 201，body 包含 id 和 email，不含 password
- [ ] AC2: 传入已存在的 email，返回 409，body 包含错误码 EMAIL_EXISTS
- [ ] AC3: 传入空 email 或 password 长度 < 8，返回 400，body 包含具体的校验错误字段

**技术备注**:
- 密码使用 bcrypt hash，cost factor = 12
- email 存储前统一转小写、trim
```
