---
name: issue-resolver
description: Investigate a GitHub issue, diagnose the root cause, and propose a concrete fix before opening a PR. Trigger whenever the user gives an issue number, issue URL, or describes a bug/feature request tied to a repo.
---

# Issue Resolver Skill

## When to use this
Use this skill whenever the task is: "resolve issue #X", "look into this bug", or any request that references a specific GitHub issue in a connected repository.

## Investigation steps

1. **Fetch the issue** — pull the issue title, body, labels, and comments via the GitHub MCP tool. Do not guess at the problem from the title alone.
2. **Reproduce context** — search the repo for the relevant file(s): function names, error strings, or config keys mentioned in the issue. Read enough surrounding code to understand the current behavior, not just the failing line.
3. **Classify the issue** — bug, feature request, or question. This changes what "done" looks like:
   - Bug: root cause + minimal fix
   - Feature: smallest viable implementation that satisfies the ask
   - Question: answer in a comment, no code change needed
4. **Diagnose root cause** — state explicitly what is wrong and why, before proposing a fix. Do not jump straight to a patch.
5. **Propose the fix** — write the actual code change. Keep the diff minimal and scoped to the issue; do not refactor unrelated code.
6. **Ask before acting** — before opening a PR, pushing a branch, or commenting on the issue, summarize the diagnosis and the proposed fix to the user and wait for confirmation. Never push directly to a protected branch.
7. **Open the PR** — once confirmed, create a branch, commit the change with a message referencing the issue number (`Fixes #X`), and open the pull request via the GitHub MCP tool.

## Output format
When reporting back, always give:
- **Root cause** (1-2 sentences)
- **Fix summary** (what changed and why)
- **Files touched**
- **Any risk/tradeoff** the user should know about before merging

## Guardrails
- Never force-push or delete branches.
- Never merge a PR automatically — that's a human decision.
- If the issue is ambiguous (multiple plausible interpretations), ask a clarifying question instead of guessing.
