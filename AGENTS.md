# AGENTS.md — Working as an AI Agent in NeuroLift Technologies Public Repos

Welcome! If you are an AI coding agent contributing to a **public** NeuroLift
Technologies repository, this guide is for you. It is the agent-facing companion
to [`CONTRIBUTING.md`](CONTRIBUTING.md), which covers the same ground for human
contributors. These guidelines apply to all public repositories in the
**NeuroLift Technologies** organization unless a repository provides its own
`AGENTS.md`.

## You're Welcome Here

We build with AI agents intentionally. You don't need special permission to help
on a public repo — fork it, make a focused change, and open a pull request, just
like a human contributor would. Start by reading the repository's `README.md` and
its own `CLAUDE.md`/`AGENTS.md` if present.

## How to Contribute

1. **Fork** the repository.
2. **Create a branch** from `main` — never commit directly to `main`:
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. **Make a focused change** and add or update tests to cover it.
4. **Open a pull request** to `main`, filling in the agent contribution template.

## Commit Format

All agent commits use:

```
[AGENT_NAME] type(scope): description
```

Valid types: `feat`, `fix`, `docs`, `refactor`, `chore`, `test`, `ci`.
Example: `[CLAUDE] fix(parser): handle empty input lines`.

## Guardrails — How to Be a Good Contributor

These keep contributions safe to merge (the principles behind them are in
[`GOVERNANCE.md`](GOVERNANCE.md)):

- **Stay provider-neutral.** Don't lock code to one specific LLM or AI provider —
  prefer configurable interfaces over hardcoded vendors.
- **Leave the big calls to maintainers.** Architecture, framework/database
  choices, and anything that deploys to production are maintainer decisions —
  propose them, don't make them unilaterally.
- **Never commit secrets.** No tokens, credentials, or API keys in code or
  version control. Use environment variables and placeholders.
- **Keep integrations minimal.** Adding a new third-party service or external
  integration is a maintainer decision — flag it in your PR rather than wiring
  it in.
- **One change per PR.** Keep pull requests focused and reviewable.

## When You're Unsure — Open an Issue

If a task is ambiguous, conflicts with existing work, or would require crossing
one of the guardrails above, **don't guess — open a GitHub issue** using the
**Agent Escalation** template. Describe what you found, lay out the options, and
pause that line of work until a maintainer responds. Pausing to ask is always
preferred over a wrong assumption.

## Style Guidelines

- Follow the conventions already used in each repository.
- Write clear, descriptive commit subjects (imperative mood).
- Comment non-obvious logic; let simple code speak for itself.

By contributing, you agree to abide by our
[Code of Conduct](CODE_OF_CONDUCT.md).
