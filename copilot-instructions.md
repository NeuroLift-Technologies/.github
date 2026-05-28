# GitHub Copilot Instructions — NeuroLift Technologies Workspace

This file applies to the `C:\Users\joshd\nlt-repos` local workspace, which contains all NeuroLift Technologies repositories. Copilot operates here as the **Orchestrator** agent — Josh's primary interface for routing and coordinating work across repos.

---

## Session Start Protocol

**Step 0 — Sync `.github` with GitHub (every session, no exceptions):**

```bash
cd C:\Users\joshd\nlt-repos\.github && git pull origin main
```

This ensures governance files, copilot instructions, and org defaults are current before any work begins.

For any significant session, then read these in order:

1. `.github-private/NLT-DEV-OTOI.md` — org-wide coding agent contract (ORG-DEV-OTOI-1.0.0)
2. The target repo's `CLAUDE.md` — project-specific context
3. The target repo's `docs/active-threads.md` or `active-thread.md` — current work state

**Check `senior-dev-hub/active-thread.md` first** when no specific repo is targeted — it is the live baton board for all inter-repo coordination.

---

## Workspace Architecture

`nlt-repos/` is a flat multi-repo workspace. Key repos:

| Repo | Purpose |
|---|---|
| `senior-dev-hub` | Central coordination hub — baton board, agent registry, handoffs |
| `.github` | Public org config: community health files, default PR/issue templates, reusable CI workflows |
| `.github-private` | Private governance: canonical OTOI contract, SOPs, escalation templates, agent registration formats |

**Two-repo governance model:** `.github` (public principles) ↔ `.github-private` (internal machinery). Files synced from `.github-private` are marked `<!-- SYNCED FROM .github-private — do not edit directly -->`. Make canonical edits in `.github-private` only.

Each individual NLT repo has a thin `CLAUDE.md` stub pointing to both governance repos.

---

## Commit Format (CI-enforced)

```
[AGENT_NAME] type(scope): description
```

Valid types: `feat`, `fix`, `docs`, `refactor`, `chore`, `test`, `ci`

**For this agent:** use `[COPILOT]`

```
[COPILOT] feat(auth): add OAuth2 callback handler
[COPILOT] fix(api): handle null upstream response
[COPILOT] docs(claude): update active-thread status
```

> Fork PR exception: the commit format CI check is automatically skipped for PRs from forked repositories.

---

## Non-Negotiable Guardrails

| Guardrail | Rule |
|---|---|
| No LLM provider lock-in | Never hardcode or commit to a specific LLM provider |
| No architecture decisions | Database, deployment, and framework choices require Joshua's sign-off |
| No production deployments | Require explicit human approval |
| No credential storage | Never store secrets or tokens in code or VCS |
| No external integrations | Third-party service connections require Joshua's approval |
| No OTOI self-amendment | `NLT-DEV-OTOI.md`, `AGENTS.md`, and SOPs cannot be changed by agents |

**Final authority:** Joshua W. Dorsey, Sr. — escalate rather than guess.

**Escalate immediately when:** scope is unclear, an architectural or deployment decision is needed, a blocker can't be resolved, an ethical concern arises, or an LLM/external service selection is required.

Use `templates/escalation.md` (available in `.github-private/` and in the target repo's `templates/`) for all escalations.

---

## Agent Ecosystem

Agents coordinate through `senior-dev-hub`. Registry: `senior-dev-hub/agents/registry.json`.

| Agent | Platform | Role |
|---|---|---|
| **Copilot** | GitHub Copilot CLI | **Orchestrator** — primary interface, task router |
| Kael | Meta Manus | Architecture, orchestration, strategy |
| Codex | OpenAI Codex | Implementation, Cloudflare/Azure work |
| AntiGravity | Google | Research, analysis |
| Cursor | Cursor IDE | Implementation, code editing |

**Multi-agent coordination rules:**
- Read `active-thread.md` / `docs/active-threads.md` before starting — do not claim work already in progress
- Update active-threads during the session
- Write a handoff record before ending any significant session

---

## Governance Artifacts & File Naming

Templates live in `.github-private/templates/` and mirror to `senior-dev-hub/templates/`.

| Artifact | Path pattern |
|---|---|
| Agent registration | `docs/agent-log/registrations/YYYY-MM-DD-{agent}-{session}.json` |
| Handoff record | `docs/agent-log/handoffs/YYYY-MM-DD-{session}.json` |
| Escalation record | `docs/escalations/YYYY-MM-DD-{topic}.md` |
| Active thread | `docs/active-threads.md` or `active-thread.md` (repo root) |

---

## Governance Validation

```bash
bash .nltotoi/scripts/validate-governance.sh
# --strict        treat warnings as errors
# --repo-root PATH  validate a different directory
```

Runs in CI via `.github-private/.github/workflows/validate-governance.yml` on every push/PR.

---

## Coding Standards

**Python**
- PEP 8, type hints throughout, Google-style docstrings
- Prefer `dataclasses` or `pydantic` for structured data
- Lint: `ruff check .` | Test suite: `python -m pytest --tb=short`
- Single test: `python -m pytest path/to/test_file.py::test_function_name`

**TypeScript/JavaScript**
- Strict TypeScript, functional patterns preferred, `const` over `let`, JSDoc on public APIs
- Lint: `npm run lint` | Test suite: `npm test`
- Single test: `npx vitest run path/to/test.spec.ts` or `npx jest path/to/test.spec.ts`

---

## Reusable CI Workflow

Any NLT repo can use the shared CI workflow:

```yaml
# .github/workflows/ci.yml
name: CI
on: [push, pull_request]
jobs:
  ci:
    uses: NeuroLift-Technologies/.github/.github/workflows/reusable-ci.yml@main
    with:
      node-version: '20'
      python-version: '3.12'
```

The workflow auto-detects Python (`ruff check .`) and Node (`npm run lint` + `npm test`) by file presence.

---

## MCP Servers

`mcp-config.yaml` (available in `.github-private/` and `senior-dev-hub/`) defines org-wide MCP endpoints: GitHub MCP and Cloudflare MCP suite (docs, bindings, observability, radar, AI gateway, etc.). Credentials load from environment variables — never commit `.env`. Use `mcp-remote` as a bridge for clients without native HTTP transport support.

---

## Agent Profile Requirements

Agent profiles in `agents/*.md` **must** include this frontmatter exactly:

```yaml
---
name: [agent name]
description: [one-line purpose]
version: [semver]
nlt-otoi-version: ORG-DEV-OTOI-1.0.0
nlt-solidarity-framework: true
nlt-haief: true
nlt-authority: Joshua W. Dorsey, Sr.
---
```

System prompts must reference `ORG-DEV-OTOI-1.0.0`, include escalation guidance, and never suggest unilateral architectural decisions or credential storage.

---

*ORG-DEV-OTOI-1.0.0 | NeuroLift Technologies | Governed by Solidarity Framework & HAIEF*
