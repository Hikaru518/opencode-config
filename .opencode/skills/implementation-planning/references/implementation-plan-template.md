# Implementation Plan Template（实施计划模板）

此模板用于 implementation-planning workflow 的 Step 5，生成 `<topic>-implementation-plan.md`（纯 Markdown，面向人类审阅/ LLM agent 参考的公共上下文）。

## 使用约束

- **纯 Markdown**：不要把结构化任务塞进正文；任务列表落到 `tasks.json`
- **自包含**：后续开发时，人类开发者/LLM agent 只读本计划也能开工（不要求再读完整 brainstorm 产物）
- **技术设计稳定**：技术设计部分是所有 tasks 的公共约束，必须清晰且一致

---

````markdown
---
topic: <topic>
date: <YYYY-MM-DD>
status: draft # draft|approved
source:
  design: docs/discussions/<YYYY-MM-DD-HH-MM-brainstorm>/<topic>-design.md
  research: docs/discussions/<YYYY-MM-DD-HH-MM-brainstorm>/research.md
  interview: docs/discussions/<YYYY-MM-DD-HH-MM-brainstorm>/<topic>-interview.md
tasks_file: <topic>-tasks.json
---

# <topic> Implementation Plan

## 1. 概述

用 1–3 段写清楚：
- 这个项目做什么（与 design doc 对齐）
- 技术方案的总体思路（一句话架构）
- 任务总数
- 关键风险（1–3 条）

### 1.1 任务文件

- `tasks_file`: `<topic>-tasks.json`

### 1.2 任务执行顺序

用有序列表列出任务的执行顺序（即 tasks.json 中的数组顺序）：

1. **TASK-001**: <标题> — <一句话说明>
2. **TASK-002**: <标题> — <一句话说明>（依赖: TASK-001）
3. **TASK-003**: <标题> — <一句话说明>（依赖: TASK-001）
4. **TASK-004**: <标题> — <一句话说明>（依赖: TASK-002, TASK-003）

## 2. 技术设计

> 说明：如果采用轻量模式，可跳过 2.3 与 2.4 两节（或仅保留最小约定）。

### 2.1 架构概览

### 2.2 技术决策记录（ADR）

### 2.3 数据模型（轻量模式可跳过）

### 2.4 API/接口设计（轻量模式可跳过）

### 2.5 目录结构

### 2.6 编码约定

## 3. 风险与缓解（技术层面）

至少列 3 条：

- **R1**：<风险>
  - **影响**：<会导致什么后果>
  - **缓解**：<如何降低风险/如何验证>
- **R2**：
  - **影响**：
  - **缓解**：
- **R3**：
  - **影响**：
  - **缓解**：

---

**Planning Completed:** <YYYY-MM-DD HH:MM>  
````
