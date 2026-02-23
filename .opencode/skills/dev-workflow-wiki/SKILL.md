---
name: dev-workflow-wiki
description: "当用户询问开发流水线、agent 职责、skill 用途、产物流转等问题时触发。混合策略：核心流程概览来自 reference，具体 agent/skill 细节动态读取最新文件。"
---

# dev-workflow-wiki

## 概述

此技能用于回答关于本项目开发流水线的一切问题。它采用**混合回答策略**：

1. 流水线全局架构、agent 职责、产物流转、执行策略、关键设计决策 → 来自本 skill 的 `references/development-workflow.md`（核心知识手册）
2. 某个具体 agent 或 skill 的详细行为 → 动态读取 `.opencode/agents/<Name>.md` 或 `.opencode/skills/<name>/SKILL.md`
3. 模板或 schema 的具体格式 → 动态读取对应 skill 的 `references/` 目录下的文件

## 何时触发

1. 用户在询问开发流水线的全局问题时。例如 "开发流程是怎么样的？"
2. 用户询问具体 Agent / Skill 的行为。例如 "Fox agent 的是做什么的？"
3. 用户询问流水线相关的模板 / Schema 格式。例如 "tasks.json 的格式是什么？"
4. 其它相关的开发流水线问题

## 回答策略

### 策略 1：流水线全局问题

**适用场景**：用户问的是全局性问题，例如：
- "一共有哪些 agent？各自负责什么？"
- "产物是怎么在 agent 之间流转的？"
- "执行策略是什么？"
- "哪些关键设计决策已经确定了？"

**动作**：直接引用 `references/development-workflow.md` 的对应章节回答。

### 策略 2：具体 Agent / Skill 的行为

**适用场景**：用户问的是某个 agent 或 skill 的具体行为、工作流程、权限、配置，例如：
- "Fox agent 的工作流是什么？"
- "brainstorm skill 的 Step 3 做了什么？"
- "WatchDog 的代码审查流程是什么？"

**动作**：
1. 先从 `references/development-workflow.md` 中给出该 agent/skill 的概述（层级、职责、输入/输出）
2. 然后读取对应的实际文件获取最新细节：
   - Agent 文件：`.opencode/agents/<Name>.md`（Brainstorm / Fox / MonkeyKing / Monkey / WatchDog）
   - Skill 文件：`.opencode/skills/<name>/SKILL.md`
3. 综合两者回答

### 策略 3：模板 / Schema 格式

**适用场景**：用户问的是某种文件格式、模板结构或 JSON schema，例如：
- "tasks.json 的格式是什么？"
- "技术设计模板包含哪些部分？"
- "project-context 模板包含哪些部分？"

**动作**：读取对应 skill 的 `references/` 目录下的文件。常见路径：

**brainstorm skill**：
- Design 文档模板：`.opencode/skills/brainstorm/references/design-template.md`
- Research 模板：`.opencode/skills/brainstorm/references/research-template.md`
- Interview 模板：`.opencode/skills/brainstorm/references/brainstorm-interview.md`

**implementation-planning skill**：
- 技术设计模板：`.opencode/skills/implementation-planning/references/technical-design-template.md`
- 任务模板：`.opencode/skills/implementation-planning/references/task-template.md`
- 实施计划模板：`.opencode/skills/implementation-planning/references/implementation-plan-template.md`
- Tasks JSON schema：`.opencode/skills/implementation-planning/references/tasks-json-schema.md`

**task-dispatching skill**：
- Monkey prompt 模板：`.opencode/skills/task-dispatching/references/monkey-prompt-template.md`
- Progress 模板：`.opencode/skills/task-dispatching/references/progress-template.md`

**project-summary skill**：
- Project context 模板：`.opencode/skills/project-summary/references/project-context-template.md`
- Changelog 模板：`.opencode/skills/project-summary/references/changelog-template.md`
- 压缩指南：`.opencode/skills/project-summary/references/compress-project-summary.md`

**systematic-debugging skill**：
- Root cause tracing：`.opencode/skills/systematic-debugging/references/root-cause-tracing.md`
- Defense in depth：`.opencode/skills/systematic-debugging/references/defense-in-depth.md`
- Condition-based waiting：`.opencode/skills/systematic-debugging/references/condition-based-waiting.md`

## 回答格式要求

- **必须附带参考链接**：每次引用 agent、skill、模板或 reference 文件时，必须用 Markdown 链接格式附上文件路径，例如 `[Fox.md](.opencode/agents/Fox.md)`、`[implementation-planning SKILL.md](.opencode/skills/implementation-planning/SKILL.md)`。读者通过链接应能直接定位到原始文件
- **简洁准确**：优先用结构化列表或表格，避免冗长段落
- **善用 mermaid**：解释架构或流程时，引用或绘制 mermaid 图
- **坦诚边界**：如果问题超出知识范围（如运行时配置、具体业务逻辑），明确说明并建议用户查阅相关代码或文档
