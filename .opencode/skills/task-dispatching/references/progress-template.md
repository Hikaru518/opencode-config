# progress.md 模板

MonkeyKing 在 Step 3 创建 progress.md 时，遵循以下格式：

---

```markdown
---
plan: "<topic>"
started: "YYYY-MM-DD HH:MM"
status: "in_progress | completed | blocked"
source:
  implementation_plan: "<topic>-implementation-plan.md 的路径"
  tasks_json: "<topic>-tasks.json 的路径"
---

# Progress: <topic>

## 任务状态

| # | Task ID | 标题 | 状态 | 尝试次数 |
|---|---------|------|------|---------|
| 1 | TASK-001 | ... | pending | 0 |
| 2 | TASK-002 | ... | pending | 0 |

状态值：`pending` | `in_progress` | `completed` | `failed`

## 执行日志

<!-- 每个任务完成（或失败）后，在此追加一条记录 -->

### TASK-001: <标题>
- 状态: completed
- 开始时间: YYYY-MM-DD HH:MM
- 完成时间: YYYY-MM-DD HH:MM
- 尝试次数: 1
- Monkey summary: （粘贴 Monkey 返回的 summary）

### TASK-002: <标题>
- 状态: failed
- 开始时间: YYYY-MM-DD HH:MM
- 尝试次数: 3
- 尝试记录:
  - 尝试 1: 方法 → 结果
  - 尝试 2: 方法 → 结果
  - 尝试 3: 方法 → 结果
- 失败原因: ...
```
