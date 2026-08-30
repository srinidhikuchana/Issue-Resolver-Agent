# Issue Resolver Agent

A developer operations agent built on **TrueForge**, that investigates a GitHub issue, diagnoses the root cause, proposes a fix, and asks for confirmation before opening a PR.

**Track:** Best Use of TrueForge

## The workflow it automates

Normally, resolving a GitHub issue means: reading the issue, digging through the codebase to find the relevant files, understanding the bug, writing a fix, and opening a PR — all manually, switching between GitHub and your editor.

This agent takes over that loop:
1. Pulls the issue via the **GitHub MCP connector**
2. Investigates the repo using its **issue-resolver skill** (`skills/issue-resolver/SKILL.md`)
3. Diagnoses the root cause and proposes a minimal fix
4. **Asks before taking any action** — no auto-push, no auto-merge
5. Opens the PR once confirmed

## Tech stack

| Piece | What we used |
|---|---|
| Agent runtime | [TrueForge](https://github.com/truefoundry/trueforge) (standalone/local mode) |
| Model | OpenAI / OpenRouter |
| Tooling | GitHub MCP server |
| Skill | Custom `issue-resolver` skill ([source](skills/issue-resolver/SKILL.md)) |
| Code review | Qodo (PR-level review, see evidence below) |

This builds on an earlier project, **[GitHub Issue Solver](#)** (Python/Streamlit/GitHub REST API), reworked here as a proper agent using MCP tools + a reusable skill instead of hardcoded API calls.

## Running it yourself

1. Open this repo in a GitHub Codespace (Code → Codespaces → Create codespace)
2. In the terminal: `npx @truefoundry/trueforge`
3. Forward port `8790` and open it in the browser
4. Settings → Models: add your API key
5. Settings → Connectors: add the GitHub MCP server, authorize this repo
6. Settings → Skills: import `skills/issue-resolver/SKILL.md` from this repo
7. In chat: enable the GitHub connector + issue-resolver skill, then run: *"Resolve issue #\<number\>"*

## What it does & how it uses TrueForge (write-up)

<!--
Short write-up, required by the hackathon rules:
- What problem does this agent solve, in plain terms?
- Which TrueForge pieces are load-bearing (MCP connector, skill, subagents, sandbox)? Be specific — judges need to see TrueForge doing real work, not a thin wrapper around a single model call.
- What decisions did you make and why?
-->

## Demo video (~3 min)

<!-- Link to your demo video here, showing the agent actually resolving an issue through the TrueForge UI -->

## Qodo Code Review Evidence

- Representative merged PR: <!-- link -->
- What Qodo found / what we changed or dismissed: <!-- 1-2 lines -->
- PR history: <!-- link showing the initial Qodo review, your fixes/dismissals, and a follow-up review against the final code -->

## AI assistant disclosure

<!-- Required by hackathon rules. Example:
Claude (Anthropic) was used to help scaffold this repo, draft the SKILL.md instructions, and troubleshoot the TrueForge/Codespaces setup. All code was reviewed, tested, and understood by the team before committing. -->

## Guardrails

The agent never force-pushes, deletes branches, or merges PRs automatically — every write action requires explicit user confirmation first.

## License

MIT — see [LICENSE](LICENSE).
