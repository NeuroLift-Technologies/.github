# Agent Pull Request Template

**Purpose:** Standard pull request template for AI agent contributions to NeuroLift Technologies public repositories.

**Governed by:** `governance.yaml` (ORG-DEV-OTOI-1.0.3)

> **Start here:** [`governance.yaml`](governance.yaml) is the authoritative machine-readable contract and [`AGENTS.md`](AGENTS.md) is the agent-facing guide. If anything in this template disagrees with `governance.yaml`, `governance.yaml` wins.

## PR Metadata

**Agent:** [Name / platform]
**Branch:** [feature/...]
**Working repo:** [Repository name]
**PR Type:** [feat | fix | docs | refactor | chore | test | ci]
**Governance Version:** ORG-DEV-OTOI-1.0.3

---

## Before Merging

- [ ] Change is focused — one feature or fix in this PR
- [ ] Tests added or updated for the change (or N/A, explained below)
- [ ] No secrets, credentials, or API keys committed
- [ ] No LLM / AI provider hardcoded without maintainer sign-off
- [ ] No architecture decision or external integration made unilaterally
      (propose it in the description instead)
- [ ] Anything ambiguous was raised via an Agent Escalation issue, linked below

---

## Scope Declaration

<!-- REQUIRED if this PR adds any new top-level directory or a large batch of files.
     Reviewers should not be surprised by new top-level directories. -->

- [ ] **No new top-level directories added** — OR each new directory is documented below
- [ ] **No large unexplained file batches** — OR the additions are explained below

**New top-level directories (if any):** None.

---

## Commit Format

All commits in this PR follow: `[AGENT_NAME] type(scope): description`

---

## Changes Summary

<!-- What this PR changes and why. Be specific enough that a reviewer can
     understand the full scope from this section alone. -->

---

## Tests

- [ ] Existing tests pass (or N/A — explain why)
- [ ] New tests added for new functionality (or N/A — explain why)

---

## Related Issues

<!-- Link any Agent Escalation issue or other related issues -->

None / #[issue]
