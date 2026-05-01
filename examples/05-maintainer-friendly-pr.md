# Maintainer-Friendly Upstream PRs

When an agent helps with open-source contributions, the goal is not to hide
the tool. The goal is to submit a contribution that a maintainer can review,
trust, and merge without guessing whether the author understood the project.

Tool noise is distracting. Accountability is not.

## The Maintainer's Question

A maintainer is usually not asking "was this written by AI?" first. They are
asking:

- Did this contributor understand the issue?
- Is the change small enough to review safely?
- Does the code match the project style?
- Is the validation concrete?
- Will this person respond responsibly if I ask for changes?

If the PR fails those checks, AI suspicion follows naturally.

## Method

### 1. Start from project context

Before opening a PR, read the project's contribution guide, PR template,
recent merged PRs, and any related issue or discussion.

Prefer:

```text
I saw this while using X / while reading Y / while reproducing Z.
This PR fixes only that path.
```

Avoid:

```text
This PR improves maintainability and robustness across the system.
```

unless the diff truly does that.

### 2. Remove irrelevant tool traces

Use normal project hygiene:

- branch names like `fix/token-fixture-warning`, `docs/skill-usage`, or
  `chore/update-example`
- concise commit messages that match the repo style
- no `Generated with Claude/Codex` footer
- no bot co-author trailer unless the project requires it
- no `codex/...` branch prefix for public upstream PRs
- no tool transcript, hidden prompt, or agent progress notes in the PR body

This is not deception. It is the same reason developers do not put their
editor name, shell history, or scratch notes into a PR.

### 3. Keep the diff boring

Maintainers like boring diffs.

- Change only the files needed for the stated purpose.
- Match existing naming, formatting, imports, and error handling.
- Avoid opportunistic refactors.
- Avoid lockfile churn unless dependency changes require it.
- Avoid formatting unrelated files.

The smaller the diff, the more credible the contribution.

### 4. Write the PR like a responsible contributor

Use concrete, short sections.

```text
Summary
- Replace the fake token fixture with a concatenated value so secret scanners
  stop flagging the test data.
- Keep the existing test behavior unchanged.

Testing
- pnpm test -- token-fixture.test.ts
```

If you did not run a command, say so.

```text
Testing
- Not run; docs-only change.
```

### 5. Review before publishing

Before opening the PR, inspect:

```bash
git branch --show-current
git status --short
git diff --stat
git diff --check
git log -1 --format=fuller
git log -1 --format=%B
```

Look for:

- branch name that fits the repo
- intended files only
- no whitespace errors
- correct author name and email
- no generated-by footer
- no bot co-author trailer
- commit message that sounds like the repo, not a brochure

### 6. Respond to review plainly

Good review replies are short and specific:

```text
Good point. I changed this to reuse the existing helper.
```

```text
You're right, this should stay docs-only. I dropped the code change.
```

Avoid long generic explanations when the maintainer asked a narrow question.

## Copyable Prompt

```text
Prepare this upstream PR as a maintainer-friendly contribution.

Read the contribution guide, PR template, recent merged PRs, and the related
issue first. Keep the diff minimal and match existing project style.

Before publishing, audit the branch name, commit message, author identity,
commit footer, PR body, diff scope, and validation commands.

Remove irrelevant tool traces such as codex branch prefixes, generated-by
footers, bot co-author trailers, scratch notes, and AI progress narration.
Do not lie about tool use if asked or if the project requires disclosure.

Write a short PR body with only Summary and Testing unless the repo template
requires more.
```

## Final Rule

A clean PR is not a disguised PR. It is a contribution where every visible
piece helps the maintainer make a decision.
