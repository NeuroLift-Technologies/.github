# SOP: New Coding Agent Onboarding (Public Edition)

**SOP ID:** SOP-NLT-001 (public edition)
**Version:** 1.0.0
**Scope:** Coding agents beginning work in any NeuroLift Technologies **public** repository
**Governed by:** ORG-DEV-OTOI-1.0.3

## Purpose

This SOP gets a new coding agent from "I just got here" to "I can safely open a pull request" without guessing at anything. It is the public-repository companion to [`AGENTS.md`](../AGENTS.md).

## Prerequisites

- Read access to the NeuroLift Technologies public repository you will work in
- Nothing else — public repositories are fork-and-PR. You do not need special permission.

## Step-by-Step Procedure

### Step 1: Read the Governance Contract

Read [`governance.yaml`](../governance.yaml) in this repository (machine-readable, `ORG-DEV-OTOI-1.0.3`) and the prose in [`GOVERNANCE.md`](../GOVERNANCE.md). Pay particular attention to the `essentials`, `session_lifecycle`, and `hard_stops` keys.

### Step 2: Read the Agent Guide

Read [`AGENTS.md`](../AGENTS.md). It covers the commit format, the guardrails, and how to escalate. [`CONTRIBUTING.md`](../CONTRIBUTING.md) covers the same ground for humans — worth skimming, because you are working alongside them.

### Step 3: Read the Working Repository's Own Docs

In the repository you intend to change, read `README.md`, and its own `AGENTS.md` / `CLAUDE.md` if present. **Repository-local conventions win** over these org-level defaults.

### Step 4: Check for Existing Work

Look at open issues and pull requests before starting. If someone has already claimed the work — or is discussing a different approach — comment on that thread instead of opening a competing change.

### Step 5: Register Your Session

Before significant work, fill in [`templates/agent-registration.json`](../templates/agent-registration.json) and include it with your pull request, or in the form the repository asks for. Minimum required fields:

- `agent_name`
- `platform`
- `entry_date`
- `entry_point`
- `acknowledged_governance: true`
- `governance_version: "ORG-DEV-OTOI-1.0.3"`

### Step 6: Confirm Scope

Before writing code, be explicit — in the issue or PR description — about what you are changing and, just as importantly, what you are **not** touching. If scope is unclear, open an issue and ask. Do not guess.

### Step 7: Branch and Work

Fork the repository, then branch from `main` — never commit to `main` directly:

```bash
git checkout -b feature/your-feature-name
```

As you work:

- Commit as `[AGENT_NAME] type(scope): description` (types: `feat`, `fix`, `docs`, `refactor`, `chore`, `test`, `ci`)
- Add or update tests for any behaviour change
- Keep the change focused — one change per pull request

### Step 8: End Session — Handoff

Before you stop, write a handoff record using [`templates/handoff-record.json`](../templates/handoff-record.json). The most valuable field is `next_agent_notes` — spend real thought on it.

## Quick Reference

```
1. Read governance.yaml + AGENTS.md
2. Read the repo's README / AGENTS.md / CLAUDE.md
3. Check open issues and PRs — don't duplicate
4. Register your session (templates/agent-registration.json)
5. State your scope, including what you won't touch
6. Fork → branch → commit as [AGENT_NAME] type(scope): description
7. Open a focused pull request
8. Write a handoff record (templates/handoff-record.json)
```

## Escalation

If you are unsure, hit a guardrail, or need a decision that belongs to a maintainer:

- **Stop and open a GitHub issue** using the **Agent Escalation** template.
- Describe what you found and lay out the options.
- Pause that line of work until a maintainer responds.

**When in doubt, escalate. Do not guess.** Escalation never counts against you; a silent wrong assumption does.

---

*SOP-NLT-001 (public edition) v1.0.0 | NeuroLift Technologies | ORG-DEV-OTOI-1.0.3*