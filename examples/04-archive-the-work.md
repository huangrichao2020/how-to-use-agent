# Example 04: Archive the Work

[English](04-archive-the-work.md) · [简体中文](04-archive-the-work.zh-CN.md)

Use this after the agent lands phase one of a larger change.

## Original prompts

```text
开始第一步吧，举一反三，小心谨慎
```

```text
你上面的改动记录 记得写工作手册，跟大版本架构设计放进同一个目录
```

```text
已归档到 wiki：queries/daily-report-2026-04-30-agent-redesign-v2-phase1-2
跟大版本架构设计手册（architectural-redesign-v2-planned）同在 queries/ 目录下。
```

## Developer intent

The first prompt authorizes a small implementation step. The second prompt
prevents the work from becoming private chat context. The third confirms the
archive path.

## A reusable version

```text
Start phase one.

Be conservative:
- reuse existing logic where possible
- avoid broad refactors
- keep the change reversible
- test the narrow behavior

After landing the change, write a work manual next to the architecture design.
The manual should include:
- what changed
- why it changed
- how to verify it
- what remains paused
- what phase two should do next
- exact file paths for the next agent

End by reporting the archive path.
```

## Completion test

The task is not complete when the code changes.

It is complete when:

- the first step works
- verification evidence exists
- the manual is written
- the manual and architecture design are near each other
- the next agent can continue from the archive path
