# CHANGELOG.md 模板

在首次创建目标项目的 `CHANGELOG.md` 时使用此模板。后续更新时在现有内容基础上追加新条目。

格式遵循 [Keep a Changelog](https://keepachangelog.com) 规范。

---

以下是模板内容：

```markdown
# Changelog

本文件记录项目的所有重要变更。

格式基于 [Keep a Changelog](https://keepachangelog.com)。

## [功能名称] - YYYY-MM-DD

### Added
- TASK-001: <标题> — <一句话描述做了什么>
- TASK-002: <标题> — <一句话描述做了什么>

### Changed
- （如果修改了已有代码/功能）

### Fixed
- （如果修复了 bug）
```

## 格式规则

- 每个 implementation plan 完成后追加一个版本块
- 版本块标题使用功能名称（来自 implementation plan 的 topic）+ 日期
- 新条目追加在文件顶部（`# Changelog` 标题之后、已有版本块之前）
- 每个 task 一行，格式：`TASK-ID: 标题 — 简要描述`
- 分类使用 Added / Changed / Fixed，空分类可省略
- 信息来源：progress.md 中的 task 完成记录 + Monkey 的 summaries
