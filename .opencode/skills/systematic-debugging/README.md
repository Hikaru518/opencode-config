> This skill is modified from https://github.com/obra/superpowers/tree/main/skills/systematic-debugging, MIT License

superpower 对于 TDD 的应用和技能描述让我非常印象深刻。这个 systematic-debugging 技能，我基本上是基于 superpower 项目的内容修改的。

我在保留了整体的测试思想的情况下我大概的修改内容如下

**本地项目化改造**
- 翻译和校对工作。这个项目中的大部分内容都是中文。
- 移除了 superpower 强相关的内容。
- 我将文件结构和翻译时的语言习惯改为了本项目中的结构和语言描述。同时还有一些章节顺序调整。

**内容更改**
- 更多的语言适用。原技能有非常强烈的 ts 语言绑定的倾向，一些内容是用 ts 代码解释的。我把大部分的代码都改成了伪代码。其中改动最大的应当是 `references/root-cause-tracing.md`。
- 加入内容总结。我在特定章节加入了总结。例如我认为当读者初次阅读 `references/defense-in-depth` 时会对四层模型毫无概念，因此先加入了四层模型的总结。比起 LLM，这实际上更多的是给人类读者准备的。
- 删除了一部分我认为不必要的 prompt 引导。原作者 Jesse 会在心理学上对 llm 进行引导，我事实上非常认同这个观点而且很受启发。但是我认为过多这方面的内容会对 llm 造成 context 空间的浪费和污染。
    - 这里贴一个原作者 Jesse 的博客链接，他是如何将转化为 https://blog.fsck.com/2026/01/30/Latent-Space-Engineering/
