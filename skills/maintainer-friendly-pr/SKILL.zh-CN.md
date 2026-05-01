---
name: maintainer-friendly-pr
description: 当需要准备外部开源 PR、GitHub PR body、分支名、commit message、review 回复，或在保持真实负责的前提下清理上游贡献里的无关 AI/tool 痕迹时使用。
---

# Maintainer-Friendly PR

[English](SKILL.md) · [简体中文](SKILL.zh-CN.md)

给别人的仓库提 PR 时使用这个 skill。

目标不是伪装 AI 使用，而是提交一个可 review、真实、低摩擦的贡献，让每个可见 artifact 都帮助维护者做判断。

## 边界

清理无关工具痕迹。不要撒谎。

- 如果维护者问起，不要声称工作完全没有工具辅助。
- 不要冒充其他贡献者。
- 如果项目要求披露 AI/tool 使用，遵守项目规则。
- 当项目不要求时，删除 generated-by footer、bot co-author trailer、草稿笔记和工具进度叙述。

## 工作流

### 1. 先读维护者上下文

编辑或发布前，先看：

- `CONTRIBUTING.md`、`README.md`、`.github/PULL_REQUEST_TEMPLATE.md`
- 近期已合并的同类 PR
- 相关 issue 或 discussion
- 现有命名、格式、测试和错误处理模式

如果没有 issue，而且改动比较主观或影响用户体验，优先先开 issue。

### 2. 让改动保持小

规则：

- 只改为完成当前目的必须改的文件
- 不顺手重构
- 不格式化无关文件
- 除非依赖确实变化，否则不制造 lockfile churn
- 复用项目已有 helper 和风格
- 测试聚焦被修改的行为

### 3. 使用正常分支和提交卫生

推荐分支名：

```text
fix/token-fixture-warning
docs/skill-usage
chore/update-example
```

公开上游 PR 避免这种分支名：

```text
codex/...
claude/...
ai-generated/...
```

commit message 规则：

- 如果项目风格明显，就贴近项目风格
- subject 简短
- 避免 `comprehensive`、`seamless`、`robust` 这类宣传词，除非它们真的精确
- 删除 generated-by footer
- 删除 bot co-author trailer，除非项目要求保留

### 4. 开 PR 前审计

运行或检查：

```bash
git branch --show-current
git status --short
git diff --stat
git diff --check
git log -1 --format=fuller
git log -1 --format=%B
```

检查：

- 分支名是否符合项目风格
- 是否只包含目标文件
- 是否没有 whitespace error
- author name 和 email 是否正确
- commit message 是否没有 generated-by footer
- commit message 是否没有不需要的 bot co-author trailer
- PR body 是否没有草稿笔记或 agent 进度叙述
- 验证命令是否具体

如果最后一个 commit 有不需要的 metadata，发布前先 amend。

### 5. 写短 PR body

推荐：

```text
Summary
- Fix ...
- Keep ...

Testing
- `exact command`
```

文档改动：

```text
Testing
- Not run; docs-only change.
```

避免宏大宣称。说明具体触发点：

- "While using X, I noticed Y."
- "This avoids secret-scanner false positives in the test fixture."
- "This documents the existing behavior."

### 6. 像贡献者一样回复 review

回复要窄、具体。

好的回复：

```text
Good point. I changed this to reuse the existing helper.
```

```text
You're right. I dropped the unrelated formatting change.
```

维护者问具体问题时，不要回一大段通用解释。

## 发布前检查表

```text
[ ] 我读了 contribution guide，或确认项目没有。
[ ] 分支名是项目风格，不是工具风格。
[ ] diff 只包含目标文件。
[ ] commit author 正确。
[ ] commit message 没有 generated-by footer。
[ ] commit message 没有不需要的 bot co-author trailer。
[ ] PR body 简短具体。
[ ] Testing 是精确命令，或明确说明没有运行。
[ ] 如果维护者询问或项目要求披露，我不会隐瞒工具使用。
```

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
