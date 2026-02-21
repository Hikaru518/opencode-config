# Monkey Prompt 模板

MonkeyKing 在 Step 4.2 派发 Monkey subagent 时，按以下模板构建 prompt：

---

```markdown

请你根据完成下面的编写代码任务。

# 任务: <task-id> — <task-title>

## 公共上下文

<!-- 从 implementation-plan.md 的技术设计部分提取以下内容，直接粘贴到这里 -->

### 架构概览
<!-- 系统的整体结构、核心模块、模块间关系 -->
...

### 相关 ADR
<!-- 与当前任务相关的架构决策记录 -->
...

### 目录结构
<!-- 项目的文件组织和每个目录的职责 -->
...

### 编码约定
<!-- 命名规范、错误处理、测试组织等项目特有的约定 -->
...

### Reference
本次任务的完整技术文档在 `此处给出 <topic>-implementation-plan.md 的路径`.

## 任务描述

你的任务是完成 `此处给出 task.json 的路径` 的 <task-id> - <task-title>. 请记住，你
- **不要 commit**：代码提交由上层的执行者在验证质量检查通过后执行
- **不要超出 task 范围**：只做当前 task 要求的改动，不"顺便"改进其他代码
- **不要跳过 TDD**：每一行 production code 都必须有对应的失败测试先行

## 质量检查命令

完成实现后，使用以下命令验证：
- 类型检查: `<typecheck command>`
- Lint: `<lint command>`
- 测试: `<test command>`
- 构建: `<build command>`

## 之前的尝试（如有）

<!-- 仅在重试时包含此部分 -->
<!-- 粘贴之前 Monkey 的失败 summary，帮助新 Monkey 避免重复相同的错误 -->

### 尝试 1
...

### 尝试 2
...


```
