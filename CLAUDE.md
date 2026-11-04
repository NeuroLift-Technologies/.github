# CLAUDE.md — NeuroLift-Technologies/.github

This is the **public organization configuration hub** for NeuroLift
Technologies. GitHub treats this repository specially: the files here serve as
org-wide defaults for any public repository that does not define its own.

## What lives here

- Community health files — `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`,
  `GOVERNANCE.md`, `SECURITY.md`, `SUPPORT.md`, `LICENSE`
- Machine-readable and human-readable governance contracts:
  - `governance.yaml` — machine-readable contract (`ORG-DEV-OTOI-1.0.4`)
  - `governance.json` — human-readable JSON version
- Default issue and pull request templates (`ISSUE_TEMPLATE/`,
  `PULL_REQUEST_TEMPLATE/`)
- Public contributor guides for both humans and AI agents
- The org profile (`profile/README.md`) and a reusable CI workflow
  (`.github/workflows/reusable-ci.yml`)

This repository contains **no application code** — it is configuration and
documentation only.

## If you're an AI agent

Read [`AGENTS.md`](AGENTS.md) — it's the agent-facing contributor guide and the
companion to [`CONTRIBUTING.md`](CONTRIBUTING.md). It covers the commit format,
the public guardrails, and how to escalate by opening an issue. The principles
behind them are in [`GOVERNANCE.md`](GOVERNANCE.md).

**Read first:**
1. Governance contract (machine-readable, ORG-DEV-OTOI-1.0.4): `governance.yaml`
2. Agent guide: `AGENTS.md`
3. Review format: `REVIEW.md`
4. Project context: `README.md`
5. Active threads: `docs/active-threads.md` (if present)

## If you're a human contributor

Start with [`CONTRIBUTING.md`](CONTRIBUTING.md).

When in doubt on either path: keep changes focused, don't commit secrets, and
open an issue rather than guessing.
