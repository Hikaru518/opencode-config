# opencode-config

我的个人 [OpenCode](https://opencode.ai/) 配置仓库。

这是一个多 Agent 协作的 AI 辅助开发工作流，涵盖从需求头脑风暴到代码实施的完整开发流程。

## 快速开始

在开始之前，确保你已经设置过以下的环境变量。

这是为了 enable opencode 中的 WebSearch 和 LSP 功能。

```bash
export OPENCODE_ENABLE_EXA=1
export OPENCODE_EXPERIMENTAL=true
```

然后按照下面的步骤使用本项目中的配置

1. 将 .opencode 目录拷贝到你的 working repo 目录下
2. 在你的 repo 下打开 opencode
3. 切换到 Brainstorm 模式
4. 描述你的想法。如 “我想要搭建一个个人博客。”

或者，在打开 opencode 之后，在 Plan 模式下

```markdown
使用 dev-workflow-wiki 技能介绍编程流程。
```
并在后续针对性的提问。

## 工作流概览

Step 1. **头脑风暴**
- 讨论想法，通过逐步访谈的形式将想法转化为设计文档 `design.md`。

Step 2. **技术设计**
- Fox agent 根据 `design.md`，通过访谈重要的技术决策，将设计文档转化为技术设计 `implementation-plan.md`。
- 任务会被拆解为粒度尽可能小的、可验证的 task，并输出一份任务列表 `tasks.json`。

Step 3. **代码编写**
- 一个调度者 agent 会按照任务的依赖顺序调度子 agent，完成代码 task，同时更新任务完成进度。
- 输入是技术设计 `implementation-plan.md` 和任务列表 `tasks.json`。
- 最终会询问是否要生成 pr。并输出一份报告，说明每个 task 的完成情况。
- 这一步中会安静地工作，尽可能不会打扰用户。

Step 4. **Review 并更新项目级别上下文** 
- 代码评审。
- 当评审结束之后，确认没有需要改动的内容之后。更新项目级别的上下文。


## Agents

不同的 agent 负责不同的角色。目前主要有下面的 agent

1. **Brainstorm**。通过研究和用户访谈，将模糊的想法转化为结构化的设计文档。
2. **Fox**。技术负责人，将设计文档转化为统一的技术方案和有序的任务列表。
3. **MonkeyKing**。任务调度者，按任务列表顺序串行派发任务给 Monkey，验证完成状态并维护进度。
   - **Monkey**。短生命周期的执行者 subagent，使用 TDD 实现单个编码任务。
4. **WatchDog**。审核者。负责审查 PR 代码变更，并更新长期的项目上下文信息。

Agent 的流程和规范是由他们拥有的 skills 决定的。每个 agent 会有 1-2 个关键 skills 来决定流程。

## 参考

在搭建这个项目的框架时，我主要研究和参考了以下的项目已研究规范的软件开发流程。

**自动化流程，Coding Agent 编排框架**
- [obra/superpowers](https://github.com/obra/superpowers) 
- [snarktank/ralph](https://github.com/snarktank/ralph)
- [bmad-code-org](https://github.com/bmad-code-org/BMAD-METHOD)
- [softaworks/gepetto](https://github.com/softaworks/gepetto)
- [Fission-AI/OpenSpec](https://github.com/Fission-AI/OpenSpec)

其中 `gepetto` 是一个专注于头脑风暴的 repo。其它都是完整的编程自动化流程。

**Skill 库**
- [Jeffallan/claude-skills](https://github.com/Jeffallan/claude-skills)
- [softaworks/agent-toolkit](https://github.com/softaworks/agent-toolkit)

这些参考项目都非常有启发，也推荐给感兴趣的读者。

我使用和改动了其中的一些 skills，详细的来源和改动我已经在引用的 skill 中的 README.md 中标注。
