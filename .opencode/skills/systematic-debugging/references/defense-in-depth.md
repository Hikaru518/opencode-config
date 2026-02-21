# Defense-in-Depth 验证

## 概述

当你修复了一个bug 时，看起来在一个地方添加验证似乎就够了。但是只在一个地方添加校验是不够的，这个 bug 可能
1. 可能被不同的代码路径绕过。因此重新触发这个 bug
2. 被重构打破。
3. 被 mock 跳过。

**核心原则**：在数据经过的每一层都添加验证。

## 为什么需要多层验证

单点验证："我们修复了 bug"
多层验证："我们让 bug 不可能发生"

不同层捕获不同的情况：
- 入口验证捕获大多数 bug
- 业务逻辑验证捕获边界情况
- 环境守卫防止上下文相关的危险
- 调试日志在其他层失败时提供帮助

## 四层模型

四层模型的概述

1. Layer 1: Entrypoint 验证。在函数/API 入口处验证。
2. Layer 2: 业务逻辑验证。在业务逻辑层面保证当前的操作是正确的。
3. Layer 3: 环境守卫。拦截在环境上下文中的危险操作。
4. Layer 4: 调试埋点。在关键操作前记录上下文信息（目录、工作路径、调用栈等）。它不阻止任何操作，但能帮你快速定位问题根因，是事后分析的最后保障。

简单来说，它的适用情况是这样的
```
Layer 1: 输入合法吗？      → 挡住大部分问题
Layer 2: 业务上合理吗？    → 挡住边界情况
Layer 3: 环境上安全吗？    → 挡住上下文相关的危险
Layer 4: 出了事能查到吗？  → 兜底，提供排查线索
```

### Layer 1：入口点验证
**目的**：在 API 边界拒绝明显无效的输入。下面是伪代码示例

```
function createProject(name, workingDirectory):
    if workingDirectory is empty:
        throw "workingDirectory cannot be empty"
    if workingDirectory does not exist:
        throw "workingDirectory does not exist"
    if workingDirectory is not a directory:
        throw "workingDirectory is not a directory"
    // ... proceed
```

### Layer 2：业务逻辑验证
**目的**：确保数据对当前操作有意义。下面是伪代码示例

```
function initializeWorkspace(projectDir, sessionId):
    if projectDir is empty:
        throw "projectDir required for workspace initialization"
    // ... proceed
```

### Layer 3：环境守卫
**目的**：在特定上下文中防止危险操作。下面是伪代码示例

```
function gitInit(directory):
    if environment is "test":
        normalizedDir = resolve(directory)
        tempDir = system temp directory

        if normalizedDir is not under tempDir:
            throw "Refusing git init outside temp dir during tests"
    // ... proceed
```

### Layer 4：调试埋点
**目的**：为事后分析捕获上下文。下面是伪代码示例

```
function gitInit(directory):
    stack = capture current call stack
    log.debug("About to git init", {
        directory: directory,
        cwd: current working directory,
        stack: stack,
    })
    // ... proceed
```

## 应用模式

当你找到一个 bug 时：

1. **追踪数据流** — 错误值从哪里来？在哪里被使用？
2. **列出所有检查点** — 列出数据经过的每一个点
3. **在每一层添加验证** — 入口、业务逻辑、环境、调试
4. **测试每一层** — 尝试绕过 Layer 1，验证 Layer 2 能捕获

## 关键原则

四层都是必要的。在测试过程中，每一层都捕获了其他层遗漏的 bug：
- 不同的代码路径绕过了入口验证
- Mock 绕过了业务逻辑检查
- 不同平台上的边界情况需要环境守卫
- 调试日志帮助识别了结构性的误用

**不要停留在一个验证点。** 在每一层都添加检查。
