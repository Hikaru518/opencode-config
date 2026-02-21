# Research Template

这个模板用于 brainstorm workflow 的 Step 3（research 阶段），指导 doc-writer subagent 整合项目内探索和互联网研究的发现，产出 `docs/plans/YYYY-MM-DD-HH-MM/research.md`。

## 使用说明

- **目标**：为 design 阶段提供决策支持，而非全面研究
- **原则**：聚焦决策、可溯源、突出冲突、轻量级（500–1500 字）
- **输入**：explore subagent（项目内）+ websearch subagent（互联网）的研究结果
- **输出**：结构化的研究报告，作为 Step 4（用户访谈）的输入

## 模板结构

```markdown
---
topic: <topic>
date: <YYYY-MM-DD>
research_scope:
  codebase: true/false  # 是否进行了项目内探索
  internet: true/false  # 是否进行了互联网研究
source:
  initial: docs/plans/<YYYY-MM-DD-HH-MM>/initial.md
  research_topics: docs/plans/<YYYY-MM-DD-HH-MM>/research-topics.md
---

## 1. Research Summary（研究摘要）
<!-- 1-3 段总结：为什么做这次研究？发现了什么关键信息？对 design 有什么影响？ -->

## 2. Project Findings（项目内发现，如果没有进行项目内探索则跳过）
### 2.1 Existing Patterns（现有模式）
<!-- 项目中已有的类似实现、约定、模式。每条附文件路径作为证据。 -->
- **Pattern 1**：<描述>（证据：`path/to/file.ext`）
- **Pattern 2**：

### 2.2 Domain Knowledge（领域知识）
<!-- 项目特有的业务逻辑、术语、约束。来源：文档、注释、架构决策。 -->
- **Knowledge 1**：<描述>（来源：`path/to/doc.md`）
- **Knowledge 2**：

### 2.3 Recent Changes（最近变更）
<!-- 近期相关提交、PR、讨论。说明趋势或正在进行的工作。 -->
- **Change 1**：<描述>（commit hash / PR #）
- **Change 2**：

### 2.4 Technical Constraints（技术约束）
<!-- 技术栈、依赖、性能/安全要求等硬约束。 -->
- **Constraint 1**：<描述>
- **Constraint 2**：

## 3. Best Practice Findings（最佳实践发现，如果没有进行互联网研究则跳过）
### 3.1 Common Approaches（常见做法）
<!-- 业界如何解决类似问题？列出 2-4 种主流方案。每条附参考链接。 -->
- **Approach A**：<描述>（参考：<URL>）
- **Approach B**：<描述>（参考：<URL>）

### 3.2 Official Recommendations（官方建议）
<!-- 来自官方文档/RFC/标准的推荐做法。优先级最高。 -->
- **Recommendation 1**：<描述>（来源：<官方文档 URL>）
- **Recommendation 2**：

### 3.3 Known Pitfalls（已知陷阱）
<!-- 别人踩过的坑、反模式、需要避免的做法。 -->
- **Pitfall 1**：<描述>（参考：<URL>）
- **Pitfall 2**：

### 3.4 SOTA / Emerging Practices（前沿实践，可选）
<!-- 最新的方案、工具、模式（如果相关且成熟度足够）。 -->
- **Practice 1**：<描述>（参考：<URL>）

## 4. Trade-offs Analysis（权衡分析）
<!-- 综合项目约束和最佳实践，列出 2-3 个关键的取舍点。格式：
- **Trade-off 1**：选项 A vs 选项 B
  - **A 的优势**：
  - **B 的优势**：
  - **建议**：在什么条件下选哪个？
-->

### Trade-off 1：<选项 A> vs <选项 B>
- **A 的优势**：
- **B 的优势**：
- **建议**：<在什么条件下选哪个？>

### Trade-off 2：<选项 C> vs <选项 D>
- **C 的优势**：
- **D 的优势**：
- **建议**：<在什么条件下选哪个？>

## 5. Key References（关键参考）
### 5.1 Project Files（项目文件）
<!-- 被引用的本地文件路径，bullet list。 -->
- `path/to/file1.ext` - <简短说明>
- `path/to/file2.ext` - <简短说明>

### 5.2 External Links（外部链接）
<!-- 被引用的在线资源，bullet list，附简短说明。 -->
- <URL> - <简短说明>
- <URL> - <简短说明>

## 6. Open Questions for Design（留给 design 的问题）
<!-- 研究后仍未解决的问题，需要在 interview/design 阶段与用户澄清。 -->
- **Q1**：<问题描述>
- **Q2**：<问题描述>

---

**Research Completed:** <YYYY-MM-DD HH:MM>  
**Next Step:** 进入 Step 4（用户访谈），使用本 research 作为输入。
```
