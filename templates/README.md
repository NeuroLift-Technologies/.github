# Session Templates

Two small JSON files that make the public governance contract actionable.

[`governance.yaml`](governance.yaml) (ORG-DEV-OTOI-1.0.3) asks every contributor — human or agent — for two things that this repository previously described but never gave you a shape for:

| Requirement in `governance.yaml` | Template |
|---|---|
| "Register your session before significant work." | [`agent-registration.json`](agent-registration.json) |
| "Write a handoff record before you leave." | [`handoff-record.json`](handoff-record.json) |

## How to use them

Copy the JSON into the repository you are actually working in, and fill in the bracketed placeholders:

```docs/agent-log/registrations/[YYYY-MM-DD]-[agent]-[topic].json
docs/agent-log/handoffs/[YYYY-MM-DD]-[agent]-[topic].json
```

If the repository you are working in has no `docs/agent-log/` directory, create it — or put the files wherever that repository's own `AGENTS.md` or `CLAUDE.md` says they belong. When the two disagree, the working repository's conventions win.

## Keep them honest

These records are a courtesy to the next contributor, not paperwork for its own sake. Write them so a human who has never seen your session can pick up the work:

- **Scope** (in registration) — say what you will *not* touch, not just what you will.
- **Blockers** (in handoff) — name the person or decision you are waiting on.
- **`next_agent_notes`** — the single most useful field. Spend real thought on it.

## What these are not

This is not the internal NeuroLift governance contract. `governance.yaml` is the authority for public repositories; if anything here contradicts it, `governance.yaml` wins. Internal and private repositories are governed separately.

If you are unsure whether something needs an escalation, open an issue using the **Agent Escalation** template rather than guessing — see `AGENTS.md`.

---

*NeuroLift Technologies | ORG-DEV-OTOI-1.0.3 | public repository templates*