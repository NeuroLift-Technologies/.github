# GitHub Copilot Instructions for NeuroLift Technologies

These instructions apply to all repositories in the NeuroLift Technologies organization.

## Governance Framework (OTOI)

All NLT repositories operate under **ORG-DEV-OTOI-1.0.0** — the organization-wide coding agent contract.

**Session start protocol (mandatory for significant work):**
1. Read `NLT-DEV-OTOI.md` (canonical contract, lives in `.github-private`)
2. Read the repo-level `CLAUDE.md` (project context)
3. Read `docs/active-threads.md` (current work state, if present)

**Final authority:** Joshua W. Dorsey, Sr. Escalate rather than guess on any architectural, deployment, UX, or strategic decision. Use `templates/escalation.md`.

**Escalate immediately when:**
- Task scope is unclear or conflicts with existing work
- An architectural or deployment decision is required (database, framework, infra)
- A blocker cannot be resolved by the agent
- An ethical concern arises
- LLM provider or external service selection is needed

## Commit Format

All agent commits **must** follow this format — enforced by CI:

```
[AGENT_NAME] type(scope): description
```

Valid types: `feat`, `fix`, `docs`, `refactor`, `chore`, `test`, `ci`

Examples:
```
[COPILOT] feat(auth): add OAuth2 callback handler
[COPILOT] fix(api): handle null response from upstream service
[COPILOT] docs(readme): clarify deployment prerequisites
```

> **Fork PR exception:** The commit format check is automatically skipped for PRs from forked repositories.

## Non-Negotiable Guardrails

| Guardrail | Rule |
|---|---|
| No LLM provider lock-in | Never hardcode or commit to a specific LLM provider without Joshua's approval |
| No architecture decisions | Database, deployment, and framework choices require human sign-off |
| No production deployments | Human must explicitly approve all production actions |
| No credential storage | Never store secrets, tokens, or credentials in code or VCS |
| No external integrations | Third-party service connections require Joshua's approval |
| No OTOI self-amendment | Governance docs (`NLT-DEV-OTOI.md`, `AGENTS.md`, SOPs) cannot be changed by agents |

## Repository Architecture

NLT uses a **two-repo governance model**:

- **`NeuroLift-Technologies/.github`** (public) — org profile, community health files, default issue/PR templates, Copilot instructions, reusable CI workflows
- **`NeuroLift-Technologies/.github-private`** (private) — canonical OTOI contract, agent templates, SOPs, escalation formats, internal procedures

Files synced from `.github-private` are marked with:
```
<!-- SYNCED FROM .github-private — do not edit directly -->
```
Edit synced files in `.github-private` only; changes propagate via `sync-governance-public.yml`.

Each individual NLT repo contains a thin `CLAUDE.md` stub that points agents to both governance repos.

### Key Directories in This Repo

| Path | Contents |
|---|---|
| `agents/` | GitHub Copilot custom agent profiles (`.md` with required NLT frontmatter) |
| `templates/` | Governance artifact templates (registration, handoff, escalation, intent log) |
| `SOPs/` | Standard operating procedures (onboarding, repo setup, incident response) |
| `docs/active-threads.md` | Live work-state baton board — read before starting any task |
| `docs/agent-log/` | Agent registration and handoff records |
| `.nltotoi/` | Governance validation namespace (validation script, file registry) |

## Governance Validation

Run the governance validation script locally to check that a repo has all required OTOI-compliant files:

```bash
bash .nltotoi/scripts/validate-governance.sh
```

Options:
- `--strict` — treat warnings as errors (exits 1 on any warning)
- `--repo-root PATH` — validate a different directory than the current git root

This script is also run in CI via `validate-governance.yml` on every push and pull request.

## Reusable CI Workflow

NLT repos use the shared CI workflow via:

```yaml
# .github/workflows/ci.yml in any NLT repo
name: CI
on: [push, pull_request]
jobs:
  ci:
    uses: NeuroLift-Technologies/.github/.github/workflows/reusable-ci.yml@main
    with:
      node-version: '20'
      python-version: '3.12'
```

The reusable workflow runs `ruff check .` for Python lint and `npm run lint` + `npm test` for Node/TS projects, auto-detecting which applies based on file presence.

## Coding Standards

**Python**
- Follow PEP 8; use type hints throughout
- Prefer `dataclasses` or `pydantic` models for structured data
- Google-style docstrings
- Lint: `ruff check .` | Test: `python -m pytest --tb=short`
- Run a single test: `python -m pytest path/to/test_file.py::test_function_name`

**TypeScript/JavaScript**
- Strict TypeScript types; prefer functional patterns; `const` over `let`
- JSDoc for public APIs
- Lint: `npm run lint` | Test: `npm test` (vitest or jest)
- Run a single test: `npx vitest run path/to/test.spec.ts` or `npx jest path/to/test.spec.ts`

## Agent Records & File Naming

When writing governance artifacts to a repo:

- Agent registrations: `docs/agent-log/registrations/{YYYY-MM-DD}-{agent-name}-{session-id}.json`
- Handoff records: `docs/agent-log/handoffs/{YYYY-MM-DD}-{session-id}.json`
- Escalation records: `docs/escalations/`
- Active thread tracking: `docs/active-threads.md`

Use the templates in `templates/` (from `.github-private`) for these records.

## Agent Profiles (`agents/`)

Agent profile files in `agents/*.md` **must** include the following frontmatter fields exactly:

```yaml
---
name: [agent name]
description: [one-line purpose]
version: [semver, e.g. 1.0.0]
nlt-otoi-version: ORG-DEV-OTOI-1.0.0
nlt-solidarity-framework: true
nlt-haief: true
nlt-authority: Joshua W. Dorsey, Sr.
---
```

The system prompt must reference `ORG-DEV-OTOI-1.0.0`, include escalation guidance, and align with Solidarity Framework principles. It must never suggest unilateral architectural decisions or credential storage.

## MCP Server Configuration

`mcp-config.yaml` (repo root) defines org-wide MCP server endpoints for AI tools. It includes GitHub MCP and Cloudflare MCP servers (docs, bindings, observability, radar, etc.). Credentials are loaded from environment variables — never commit `.env` files. Clients without native HTTP transport support can use `mcp-remote` as a bridge (see the fallback section at the bottom of that file).

## Pull Requests

- Fill in the PR template fully, including the agent contribution checklist
- Reference the related issue number
- Keep PRs focused — one feature or fix per PR
- Ensure `docs/active-threads.md` is updated and a handoff record is written before the session ends
