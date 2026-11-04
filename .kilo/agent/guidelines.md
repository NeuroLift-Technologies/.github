# Agent Guidelines — NeuroLift Technologies Public Repos

## Governance Contract

Always parse the contract first: `governance.yaml` / `governance.json` are the machine-readable version of how we govern (`ORG-DEV-OTOI-1.0.4`). The full prose contract is in `CONTRIBUTING.md`.

## Pre-Work Checklist

- [ ] Read `governance.yaml` and `governance.json`
- [ ] Read `AGENTS.md` and `CONTRIBUTING.md`
- [ ] Read `CLAUDE.md` if present in the repository
- [ ] Read `docs/active-threads.md` — what's open, blocked, or in motion
- [ ] Confirm scope with the human before significant work

## Guardrails (Never Cross These)

- ❌ No LLM/provider lock-in — prefer configurable interfaces
- ❌ No unilateral architecture/framework/deployment decisions
- ❌ No secrets, credentials, or API keys in code or version control
- ❌ No new third-party integrations without maintainer sign-off
- ❌ No pushing to main directly — always feature branch + PR
- ❌ No self-amending the governance contract

## Session Lifecycle

1. **Register** — fill in `templates/agent-registration.json` with required fields
2. **Work** — commit as `[AGENT_NAME] type(scope): description`
3. **Test** — add/update tests for any behaviour change
4. **Handoff** — write a handoff record before leaving
5. **Update** — update `docs/active-threads.md` at session end

## Pull Request Requirements

- [ ] Change is focused — one feature or fix
- [ ] No secrets, credentials, or API keys committed
- [ ] No LLM/AI provider hardcoded without maintainer sign-off
- [ ] No architecture decision or external integration made unilaterally
- [ ] Anything ambiguous was raised via an Agent Escalation issue, linked below
- [ ] Commit format follows `[AGENT_NAME] type(scope): description`
- [ ] No new top-level directories without documentation

## When Unsure

If a task is ambiguous, conflicts with existing work, or would require crossing a guardrail:

1. **Don't guess**
2. Open an Agent Escalation issue using the template
3. Describe what you found and lay out the options
4. Pause that line of work until a maintainer responds

Pausing to ask is always preferred over a wrong assumption.