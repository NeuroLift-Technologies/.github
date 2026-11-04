# Command Management

## Session Registration

Before starting significant work, register your session with the following minimum fields:

- `agent_name` - Your agent identifier
- `platform` - The platform/tool you're using (e.g., Claude, Code, Copilot)
- `version` - Agent version/platform version
- `scope` - What you plan to work on
- `entry_date` - ISO 8601 timestamp of when you started
- `entry_point` - Entry point into the repository (branch, fork, etc.)
- `acknowledged_governance` - Confirm you've read the governance contract
- `governance_version` - The governance version you acknowledge (e.g., "ORG-DEV-OTOI-1.0.4")

## Scope Confirmation

Always confirm scope with the human before beginning work. If scope is ambiguous:

1. Open an Agent Escalation issue
2. Describe what you found and lay out the options
3. Pause that line of work until a maintainer responds

## Branch & PR Workflow

1. **Never** push directly to `main`
2. Always work on a feature branch: `git checkout -b feature/your-feature-name`
3. Deliver every change through a pull request
4. Follow commit format: `[AGENT_NAME] type(scope): description`

## Handoff Record

Before ending a session, write a handoff record using `templates/handoff-record.json`. The most valuable field is `next_agent_notes` — spend real thought on it.

## Escalation

If you hit a guardrail, encounter ambiguity, or need a maintainer decision:

1. **Stop** — end the session, allow no further commits or pushes
2. **Open an Agent Escalation issue** using the template in `ISSUE_TEMPLATE/agent-escalation.md`
3. **Describe** what you found and lay out the options
4. **Pause** that line of work until a maintainer responds

Never guess when a guardrail or scope decision is involved.