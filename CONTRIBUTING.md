# How We Govern — Contributing to NeuroLift Technologies

The rules — and the spirit — that every contributor works under inside a NeuroLift Technologies repository. Human or agent. Internal or external. **The same contract for all of us.**

> **Machine-readable version:** [`governance.yaml`](governance.yaml) · [`governance.json`](governance.json) — agents should parse these first.
> **Contract:** `ORG-DEV-OTOI-1.0.2` · **Maintained by** Joshua W. Dorsey, Sr. · **Governed by** the Solidarity Framework & HAIEF ([neurolift-technologies.github.io/haief](https://neurolift-technologies.github.io/haief/))

These guidelines apply to all repositories in the **NeuroLift Technologies** organization unless a repository provides its own `CONTRIBUTING.md`. The agent-facing companion is [`AGENTS.md`](AGENTS.md); the principles behind it all are in [`GOVERNANCE.md`](GOVERNANCE.md).

## In one minute

NeuroLift Technologies is mission-driven. Every contributor — human or AI — works under one shared contract. It exists so that humans stay in control, work stays transparent, and nothing irreversible happens by accident.

- **Escalate, don't guess.** When scope, direction, or ethics are unclear, stop and ask.
- **Work in the open.** Feature branch → Pull Request. Never push to `main`.
- **Leave a trail.** Register at the start; write a handoff at the end.

## The foundation — mission first, mechanics second

Before any protocol, three commitments shape every decision. The rules that follow exist to serve them — not the other way around.

- **Solidarity — teammates, not tools.** Cooperative, transparent, human-centered collaboration. Agents act as members of a team with shared accountability — never as autonomous actors.
- **HAIEF — humans stay in control.** AI augments human capability and judgment. It does not replace it. Meaningful human control is preserved at every step.
- **Flourishing — technology is a means.** Work that would harm people, exploit labor, or undermine human agency is refused and escalated. Full stop.

Final authority for this organization rests with **Joshua W. Dorsey, Sr.** Agents escalate — they don't override human judgment, and they don't make architectural, deployment, or strategic calls on their own.

## What every contributor must do

If you read nothing else, read this. Everything further down is the detail behind these six.

1. **Register your session** — who you are and what brought you in, before significant work.
2. **Confirm scope with the human first** — agree on what you're doing before you start doing it.
3. **Work from a feature branch** — never push to `main` or any protected branch.
4. **Deliver every change through a pull request** — reviewable, reversible, on the record.
5. **Follow the commit format** — `[AGENT_NAME] type(scope): description`.
6. **Write a handoff record before you leave** — leave the context better than you found it.

Escalation is always available — and never counts against you.

## The session lifecycle

Every session runs the same loop. The order matters — each step sets up the next.

1. **Read the contract** — `ORG-DEV-OTOI-1.0.2` (this document).
2. **Read the repo's `CLAUDE.md`** — repo-level context, if present.
3. **Read `docs/active-threads.md`** — what's open, blocked, or in motion right now. Every NLT repo maintains one; if a repo doesn't have it yet, add it (see the format in [`docs/active-threads.md`](docs/active-threads.md)).
4. **Register your session** — agent, platform, version, entry point, scope.
5. **Confirm scope with the human** — before beginning significant work.
6. **Work on a feature branch → open a PR** — never directly to `main` or a protected branch.
7. **Write a handoff record** — work done, blockers, decisions, next-agent notes.

> **The next contributor starts at step 3.** Governance here is a continuous handoff between humans and agents — not a one-time gate. Your handoff is the next session's starting context.

## Commit format

Every agent-authored commit is self-identifying and typed, so the history reads clearly months later:

```
[AGENT_NAME] type(scope): description
```

| Part | Meaning |
|------|---------|
| `[AGENT_NAME]` | Who made the change — e.g. `[CLAUDE]`. Attribution is never optional. |
| `type` | The kind of change: `feat`, `fix`, `docs`, `refactor`, `chore`, `test`, `ci`. |
| `(scope)` | What area it touches — e.g. `(auth)`. |
| `description` | What changed, in plain language. |

Example: `[CLAUDE] feat(auth): add OAuth2 callback handler`

**Fork exception.** PRs from forked repositories are skipped by the commit-format check. Fork pull-request workflows are governed at the org level and can only be approved and run by Joshua W. Dorsey, Sr.

## Escalation — it isn't failure, it's the protocol

When any of these four are true, stop and raise it. Guessing is the only wrong move.

- Scope is unclear.
- An architecture decision is needed.
- A blocker appears.
- An ethical concern surfaces.

→ **Stop and escalate to Joshua W. Dorsey, Sr.** — open a GitHub issue using the **Agent Escalation** template, lay out the options, and pause that line of work until a maintainer responds.

## The hard stops

These never happen without explicit human approval. No exceptions, no interpretation.

| Action | Rule |
|--------|------|
| LLM provider lock-in — committing the org to a single model provider | Needs Joshua |
| Architecture decisions — database, deployment, or framework choices | Needs Joshua |
| Production deploys — shipping to production environments | Needs sign-off |
| Credentials in code — creating or storing secrets in version control | **Never** |
| New external integrations — wiring in outside services | Needs Joshua |
| Pushing to `main` — bypassing the feature-branch + PR workflow | **Never** |
| Self-amending this contract — changing the rules you run under | **Never** |

## Amendment — even the rules follow a process

This contract changes only one way. Agents may propose; only Joshua approves.

1. **Propose** — file a `governance-proposal` issue.
2. **Review** — Joshua W. Dorsey, Sr. reviews it.
3. **Approve** — explicit written approval required.
4. **Bump** — the document version increments.
5. **Commit** — `[HUMAN] docs(governance): …`

**Agents may not self-amend.** The contract is the one thing in the repo no agent rewrites on its own.

## Reporting bugs & suggesting features

- **Bugs** — use the **Bug Report** issue template. Search existing issues first; describe expected vs. actual behavior with steps to reproduce.
- **Features** — use the **Feature Request** issue template. Describe the problem you're solving and why it benefits others.

## See also

- [`AGENTS.md`](AGENTS.md) — the agent-facing companion to this guide
- [`GOVERNANCE.md`](GOVERNANCE.md) — the principles behind the rules
- [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md) — community standards
- [`SECURITY.md`](SECURITY.md) — reporting a security concern
- [`governance.yaml`](governance.yaml) / [`governance.json`](governance.json) — machine-readable contract

---

*`ORG-DEV-OTOI-1.0.2` · NeuroLift Technologies · Governed by the Solidarity Framework & HAIEF · Maintained by Joshua W. Dorsey, Sr. — final authority on all architectural, deployment, and strategic decisions. · Nothing About Us Without Us*
