# 面向维护者的上游 PR

当 agent 帮你给开源项目提 PR 时，目标不是隐藏工具。目标是提交一个维护者能审阅、能信任、能合并的贡献，而不是让维护者猜“这个人到底读没读项目”。

工具噪声会干扰判断。责任感不会。

## 维护者真正关心什么

维护者通常不是先问“这是不是 AI 写的”。他们更在意：

- 这个贡献者理解问题了吗？
- 改动足够小、足够容易 review 吗？
- 代码符合项目风格吗？
- 验证是否具体？
- 如果我要求修改，这个人会不会负责地回应？

如果 PR 过不了这些检查，AI 感才会自然冒出来。

## 方法

### 1. 从项目上下文开始

提 PR 前，先读项目的贡献指南、PR 模板、近期已合并 PR，以及相关 issue 或讨论。

推荐这种真实触发点：

```text
我在使用 X / 阅读 Y / 复现 Z 时看到这个问题。
这个 PR 只修这条路径。
```

避免这种空泛说法：

```text
This PR improves maintainability and robustness across the system.
```

除非 diff 真的做到了。

### 2. 去掉无关工具痕迹

使用正常的项目卫生习惯：

- 分支名用 `fix/token-fixture-warning`、`docs/skill-usage`、`chore/update-example`
- commit message 简短，并贴近项目风格
- 不带 `Generated with Claude/Codex` footer
- 不带 bot co-author trailer，除非项目明确要求
- 给公开上游 PR 时不用 `codex/...` 分支前缀
- PR body 里不放工具 transcript、隐藏 prompt 或 agent 进度记录

这不是欺骗。开发者本来也不会把编辑器名称、shell 历史或草稿笔记放进 PR。

### 3. 让 diff 无聊一点

维护者喜欢无聊的 diff。

- 只改为完成当前目的必须改的文件。
- 匹配已有命名、格式、import 和错误处理方式。
- 不顺手重构。
- 除非依赖确实变化，否则不制造 lockfile churn。
- 不格式化无关文件。

diff 越小，贡献越可信。

### 4. 像负责的贡献者一样写 PR

用具体、短小的结构。

```text
Summary
- Replace the fake token fixture with a concatenated value so secret scanners
  stop flagging the test data.
- Keep the existing test behavior unchanged.

Testing
- pnpm test -- token-fixture.test.ts
```

如果没跑命令，直接说明。

```text
Testing
- Not run; docs-only change.
```

### 5. 发布前自查

开 PR 前检查：

```bash
git branch --show-current
git status --short
git diff --stat
git diff --check
git log -1 --format=fuller
git log -1 --format=%B
```

重点看：

- 分支名是否贴近项目风格
- 是否只包含目标文件
- 是否没有 whitespace error
- author name 和 email 是否正确
- 是否没有 generated-by footer
- 是否没有 bot co-author trailer
- commit message 是否像这个项目，而不是宣传稿

### 6. 简洁回应 review

好的 review 回复很短、很具体：

```text
Good point. I changed this to reuse the existing helper.
```

```text
You're right, this should stay docs-only. I dropped the code change.
```

维护者问窄问题时，不要回一大段通用解释。

## 可复制 Prompt

```text
把这个上游 PR 准备成一个面向维护者的正常贡献。

先读 contribution guide、PR template、近期已合并 PR 和相关 issue。
保持 diff 最小，并匹配项目已有风格。

发布前审计分支名、commit message、author identity、commit footer、PR body、diff scope 和验证命令。

去掉无关工具痕迹，例如 codex 分支前缀、generated-by footer、bot co-author trailer、草稿笔记和 AI 进度叙述。
如果维护者询问，或项目要求披露，不要隐瞒工具使用。

除非项目模板要求更多内容，否则 PR body 只写短的 Summary 和 Testing。
```

## 最后一条原则

干净的 PR 不是伪装出来的 PR。它是让每个可见部分都帮助维护者做判断的 PR。
