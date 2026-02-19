# tasks.json Schema（结构化任务列表）

此文档定义 `<topic>-tasks.json` 的字段、约束与示例。

## 文件位置与命名

- **文件名**：`<topic>-tasks.json`
- **推荐位置**：与 `<topic>-implementation-plan.md` 同目录（通常是 `docs/discussions/<...>/`）

## 顶层结构

```json
{
  "topic": "<topic>",
  "created": "YYYY-MM-DD",
  "tasks": []
}
```

### 顶层字段

- **topic**: string，主题名（与 design doc / plan 保持一致）
- **created**: string，创建日期（推荐 `YYYY-MM-DD`）
- **tasks**: array，任务列表，**数组顺序即执行顺序**（第 0 项最先执行）

## Task 对象结构

```json
{
  "id": "TASK-001",
  "title": "项目初始化与开发环境搭建",
  "priority": "P0",
  "depends_on": [],
  "user_story": "US-001",
  "description": "一段清晰的任务描述，足够自包含。",
  "files": {
    "create": ["src/main.ts"],
    "modify": ["package.json"],
    "test": ["tests/main.test.ts"]
  },
  "acceptance_criteria": [
    "AC1: ...",
    "AC2: ..."
  ],
  "tech_notes": "参考 ADR-001；遵循编码约定。"
}
```

### 字段说明与约束

- **id**: string  
  - 必须匹配 `TASK-NNN`（三位数字），例如 `TASK-007`
- **title**: string  
  - 简短、可读、动作导向（例如"实现 X API""添加 Y 页面"）
- **priority**: string  
  - 枚举：`P0` | `P1` | `P2`
- **depends_on**: string[]（可选，默认 `[]`）
  - 本任务的前置依赖任务 id 列表（如 `["TASK-001", "TASK-002"]`）
  - 用于说明排序理由，但执行顺序以数组位置为准
  - 所有 `depends_on` 引用的任务必须在数组中排在本任务之前
- **user_story**: string | null  
  - 对应 design doc 的 User Story（如 `US-003`）；若是纯基础设施可为 null
- **description**: string  
  - 必须自包含，足以让后续开发实现时不依赖额外上下文即可开工
- **files**: object（必须包含 create/modify/test 三个 key，即使为空数组）
  - **create**: string[]：本任务会创建的新文件（相对路径）
  - **modify**: string[]：本任务会修改的既有文件（相对路径）
  - **test**: string[]：本任务新增/修改的测试文件（相对路径）
  - 建议：数组内路径去重、排序（非强制）
- **acceptance_criteria**: string[]
  - 每条 AC 必须可观察、可验证；避免实现细节
  - 建议至少包含 1 条错误/边界条件
- **tech_notes**: string（可为空字符串，但建议有内容）
  - 记录必须遵循的 ADR、约束、目录/接口契约、性能/安全注意事项

##（可选）JSON Schema（草案）

以下为可用于校验的 JSON Schema（Draft 2020-12，非强制）：

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object",
  "additionalProperties": false,
  "required": ["topic", "created", "tasks"],
  "properties": {
    "topic": { "type": "string", "minLength": 1 },
    "created": { "type": "string", "minLength": 8 },
    "tasks": {
      "type": "array",
      "items": {
        "type": "object",
        "additionalProperties": false,
        "required": [
          "id",
          "title",
          "priority",
          "user_story",
          "description",
          "files",
          "acceptance_criteria",
          "tech_notes"
        ],
        "properties": {
          "id": { "type": "string", "pattern": "^TASK-\\\\d{3}$" },
          "title": { "type": "string", "minLength": 1 },
          "priority": { "type": "string", "enum": ["P0", "P1", "P2"] },
          "depends_on": {
            "type": "array",
            "items": { "type": "string", "pattern": "^TASK-\\\\d{3}$" },
            "default": []
          },
          "user_story": { "type": ["string", "null"] },
          "description": { "type": "string", "minLength": 1 },
          "files": {
            "type": "object",
            "additionalProperties": false,
            "required": ["create", "modify", "test"],
            "properties": {
              "create": { "type": "array", "items": { "type": "string" } },
              "modify": { "type": "array", "items": { "type": "string" } },
              "test": { "type": "array", "items": { "type": "string" } }
            }
          },
          "acceptance_criteria": {
            "type": "array",
            "minItems": 1,
            "items": { "type": "string", "minLength": 1 }
          },
          "tech_notes": { "type": "string" }
        }
      }
    }
  }
}
```
