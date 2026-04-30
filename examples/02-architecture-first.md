# Example 02: Architecture Before Code

[English](02-architecture-first.md) · [简体中文](02-architecture-first.zh-CN.md)

Use this when the agent realizes the change is bigger than a normal patch.

## Original prompt

```text
这简直是大版本改动了，一条一条来，你先存档为大版本架构设计手册，然后我们一条条讨论和修改
```

## Developer intent

The prompt slows the agent down and turns the idea into a durable architecture
artifact.

Without this step, the agent may start editing code while the design is still
moving.

## A reusable version

```text
This is a major architecture change.

Do not implement yet.

First write an architecture design manual and save it in the project docs/wiki.
The manual should include:
- current problem
- target architecture
- migration phases
- risks
- rollback strategy
- what must stay unchanged for now

After archiving it, summarize the sections and we will discuss them one by one.
```

## Acceptance check

Before implementation starts, verify:

- The design has a stable path.
- The migration is split into phases.
- The first phase is small enough to test.
- The rollback path is written down.
- Future agents can find the design without reading the chat transcript.
