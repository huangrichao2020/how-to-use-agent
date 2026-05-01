---
name: maintainer-friendly-pr
description: Use when preparing external open-source pull requests, GitHub PR bodies, branch names, commit messages, review replies, or cleaning irrelevant AI/tool traces from an upstream contribution while keeping truthful accountability.
---

# Maintainer-Friendly PR

[English](SKILL.md) · [简体中文](SKILL.zh-CN.md)

Use this skill when preparing a pull request for someone else's repository.
The goal is not to disguise AI use. The goal is to submit a reviewable,
truthful, low-friction contribution where every visible artifact helps the
maintainer decide.

## Boundary

Clean up irrelevant tool traces. Do not lie.

- Do not claim the work was manual-only if asked.
- Do not impersonate another contributor.
- Follow disclosure rules if the project asks for AI/tool disclosure.
- Remove generated-by footers, bot co-author trailers, scratch notes, and
  tool progress narration when they are not required by the project.

## Workflow

### 1. Read the maintainer context

Before editing or publishing, inspect:

- `CONTRIBUTING.md`, `README.md`, `.github/PULL_REQUEST_TEMPLATE.md`
- recent merged PRs with similar scope
- related issues or discussions
- existing naming, formatting, tests, and error-handling patterns

If there is no issue and the change is subjective or user-facing, prefer
opening an issue first.

### 2. Keep the change small

Rules:

- change only files needed for the stated purpose
- avoid opportunistic refactors
- avoid unrelated formatting
- avoid lockfile churn unless dependency changes require it
- reuse local helpers and style
- keep tests focused on the changed behavior

### 3. Use normal branch and commit hygiene

Prefer branch names like:

```text
fix/token-fixture-warning
docs/skill-usage
chore/update-example
```

Avoid public upstream branch names like:

```text
codex/...
claude/...
ai-generated/...
```

Commit message rules:

- match the repo style when obvious
- keep the subject concise
- avoid brochure words like "comprehensive", "seamless", "robust" unless they
  are precise
- remove generated-by footers
- remove bot co-author trailers unless required

### 4. Audit before opening the PR

Run or inspect:

```bash
git branch --show-current
git status --short
git diff --stat
git diff --check
git log -1 --format=fuller
git log -1 --format=%B
```

Check:

- branch name fits the repo
- intended files only
- no whitespace errors
- author name and email are correct
- commit message has no generated-by footer
- commit message has no unwanted bot co-author trailer
- PR body contains no scratch notes or agent progress narration
- validation commands are exact

If the last commit has unwanted metadata, amend it before publishing.

### 5. Write a short PR body

Prefer:

```text
Summary
- Fix ...
- Keep ...

Testing
- `exact command`
```

For docs-only changes:

```text
Testing
- Not run; docs-only change.
```

Avoid grand claims. Explain the concrete trigger:

- "While using X, I noticed Y."
- "This avoids secret-scanner false positives in the test fixture."
- "This documents the existing behavior."

### 6. Respond to review like a contributor

Reply narrowly and concretely.

Good:

```text
Good point. I changed this to reuse the existing helper.
```

```text
You're right. I dropped the unrelated formatting change.
```

Avoid generic essays when the maintainer asked a specific question.

## Pre-Publish Checklist

```text
[ ] I read the contribution guide or confirmed there is none.
[ ] The branch name is project-style, not tool-style.
[ ] The diff only contains intended files.
[ ] The commit author is correct.
[ ] The commit message has no generated-by footer.
[ ] The commit message has no unwanted bot co-author trailer.
[ ] The PR body is short and concrete.
[ ] Testing is exact, or I clearly said it was not run.
[ ] I am not hiding tool use if asked or required to disclose it.
```

## Copyable Prompt

```text
Prepare this upstream PR as a maintainer-friendly contribution.

Read the contribution guide, PR template, recent merged PRs, and related issue
first. Keep the diff minimal and match existing project style.

Before publishing, audit the branch name, commit message, author identity,
commit footer, PR body, diff scope, and validation commands.

Remove irrelevant tool traces such as codex branch prefixes, generated-by
footers, bot co-author trailers, scratch notes, and AI progress narration.
Do not lie about tool use if asked or if the project requires disclosure.

Write a short PR body with Summary and Testing unless the repo template
requires more.
```
