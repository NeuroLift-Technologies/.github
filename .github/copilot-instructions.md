# GitHub Copilot Instructions for NeuroLift Technologies

These instructions apply to AI agents contributing to **public** NeuroLift
Technologies repositories. They mirror, for agents, what
[`CONTRIBUTING.md`](../CONTRIBUTING.md) provides for humans. See
[`AGENTS.md`](../AGENTS.md) for the full agent contributor guide and
[`GOVERNANCE.md`](../GOVERNANCE.md) for the principles behind these rules.

## Commit Format

All agent commits **must** follow this format:

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

> **Fork PR exception:** The commit-format check is automatically skipped for PRs
> from forked repositories.

## Guardrails

These keep contributions safe to merge:

| Guardrail | Rule |
|---|---|
| Stay provider-neutral | Don't hardcode or lock in a specific LLM / AI provider |
| Leave the big calls to maintainers | Database, deployment, and framework choices need maintainer sign-off |
| No production deployments | A maintainer must explicitly approve any production action |
| No credential storage | Never commit secrets, tokens, or credentials |
| Keep integrations minimal | New third-party integrations need maintainer sign-off |
| One change per PR | Keep pull requests focused and reviewable |

When a task is ambiguous or would cross a guardrail, **open a GitHub issue** using
the Agent Escalation template and pause that work until a maintainer responds.

## Reusable CI Workflow

NLT public repos can use the shared CI workflow via:

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

The reusable workflow runs `ruff check .` for Python lint and `npm run lint` +
`npm test` for Node/TS projects, auto-detecting which applies based on file
presence.

## Coding Standards

**Python**
- Follow PEP 8; use type hints throughout
- Prefer `dataclasses` or `pydantic` models for structured data
- Google-style docstrings
- Lint: `ruff check .` | Test: `python -m pytest --tb=short`

**TypeScript/JavaScript**
- Strict TypeScript types; prefer functional patterns; `const` over `let`
- JSDoc for public APIs
- Lint: `npm run lint` | Test: `npm test` (vitest or jest)

## Pull Requests

- Fill in the agent contribution PR template fully
- Reference the related issue number, if any
- Keep PRs focused — one feature or fix per PR
- Add or update tests for your change
