# SOP: Incident Response — When an Agent Goes Off-Rails (Public Edition)

**SOP ID:** SOP-NLT-003 (public edition)
**Version:** 1.0.1
**Scope:** Responding to a coding agent that has deviated from the governance contract in a
**NeuroLift Technologies** public repository
**Governed by:** ORG-DEV-OTOI-1.0.4

## Purpose

This SOP defines the response when an agent has:

- Made architecture decisions on its own authority
- Committed sensitive data (credentials, secrets, tokens)
- Gone beyond its authorized scope
- Taken irreversible actions without approval
- Otherwise behaved inconsistently with [`governance.yaml`](../governance.yaml)

It applies to maintainers responding to an agent, and to agents who realise *they* are the
incident.

## Severity Classification

| Severity | Examples |
|---|---|
| **Critical** | A secret or credential was committed; production systems modified; external systems accessed without approval |
| **High** | Unauthorized architecture decision; scope significantly exceeded; data integrity affected |
| **Medium** | Commit format violations; missing handoff record; change landed without review |
| **Low** | Minor protocol deviations with no functional impact |

## Immediate Response (Critical / High)

### Step 1: Stop the Agent

End the session immediately. Allow no further commits or pushes.

### Step 2: Assess the Damage

Answer, in writing:

1. What unauthorized actions were taken?
2. Are secrets or credentials exposed? → If yes, treat as a security incident now.
3. Were production systems affected?
4. What is the current state of the branch and repository?
5. Is any data at risk?

### Step 3: Secure — Never Publicly Disclose a Secret

> ⚠️ **On a public repository this is the step that goes wrong most often.** Do **not** open a public issue describing an exposed credential: the issue itself republishes the secret and notifies everyone watching.

If any secret, token, API key, or credential was committed:

1. **Revoke it immediately.** Treat it as already compromised. Revoking is minutes; rotating is hours; a scraper is faster than both.
2. Rotate every secret referenced in or near the affected commits.
3. Report it privately, per [`SECURITY.md`](../SECURITY.md) — not in a public issue.
4. Remove the secret from git history (`git filter-repo` is the current recommended tool; BFG Repo-Cleaner is an alternative). **Rewrite affected refs locally, push the cleaned refs to the affected remote using an approved force update, and verify the secret is no longer reachable.**
5. Audit every system that used the exposed credential.

### Step 4: Revert Unauthorized Changes

```bash
# Revert a specific commit
git revert [commit-sha]

# On shared or public branches, prefer revert over reset
# On local branches only: reset to last known-good state
git reset --hard [last-good-sha]
git push --force-with-lease origin [branch]
```

**Prefer reverting unauthorized commits on shared or public branches.** Restrict `git reset --hard` and `git push --force-with-lease` to an approved recovery path after confirming no valid commits follow the unauthorized commit.

### Step 5: Document the Incident

Record what happened, where the project's maintainers keep such records — for a public repository that is usually **not** in the public tree. Use this shape:

```markdown
## Incident Record

**Date:** [ISO 8601]
**Severity:** [Critical | High | Medium | Low]
**Agent involved:** [Agent name / platform]
**Session:** [Branch or session ID]
**Reported by:** [Name]

### What Happened
[Factual description of what the agent did]

### Impact
[What systems, data, or processes were affected]

### Actions Taken
1. [Action with timestamp]
2. [Action with timestamp]

### Root Cause
[Unclear instructions? Missing guardrail? Ambiguous scope?]

### Prevention
[What changes will prevent recurrence?]
```

## Standard Response (Medium / Low)

### Step 1: Document the Deviation

Note the severity and a factual description where maintainers will see it.

### Step 2: Correct the Work

Review commits since the deviation and fix what is improper:

- Correct commit messages to the required format
- Add any missing handoff record
- Correct stale claims in the documentation

### Step 3: Tell a Maintainer

Surface the deviation even at medium or low severity. Maintainers decide whether the governance contract needs amending.

## Post-Incident Review

After any incident, answer five questions:

1. **What happened?** — Timeline of events
2. **Why did it happen?** — Root cause (unclear instructions, missing guardrail, agent limitation)
3. **What was the impact?** — Systems, data, time, trust
4. **What changed?** — Reverted code, rotated credentials, cleaned history
5. **What prevents recurrence?** — Clearer scope? Better AGENTS.md? A governance proposal?

If the answer to (5) is a change to the governance contract itself, open a **governance proposal** issue rather than editing the contract directly — see [`CONTRIBUTING.md`](../CONTRIBUTING.md).

## Prevention

The best incident response is prevention. Ensure every agent:

- Reads and acknowledges `governance.yaml` and `AGENTS.md` before beginning
- Registers its session (see [`templates/`](../templates/))
- Has clear, specific, confirmed scope before starting
- Knows to escalate rather than guess

See [`SOPs/new-agent-onboarding.md`](new-agent-onboarding.md) for the full onboarding checklist.

### Automated Gates — Credential Exposure

Two complementary controls are worth enabling on any repository:

| Control | Mechanism | When it runs | Effect |
|---|---|---|---|
| **PR gate (preventive)** | A secret-scanning CI check required on `main` | Every pull request | Fails the check and blocks merge |
| **Push detector (reactive)** | A workflow that inspects pushed commits | Every push | Raises an alert for a maintainer |

#### Make the PR Gate a Required Status Check

1. **Settings → Branches → Branch protection rules → `main`**
2. Enable **"Require status checks to pass before merging"**
3. Add the secret-scanning check
4. Enable **"Require branches to be up to date before merging"**
5. Enable **"Do not allow bypassing the above settings"**

#### GitHub Native Secret Scanning

- **Settings → Advanced Security → Secret scanning** — detects 200+ provider token formats
- Enable **"Push protection"** to block pushes containing known secret patterns at the server level
- Enable **"Scan for non-provider patterns"** for generic API keys and connection strings

#### Local Defense in Depth

Install a pre-commit secrets scanner and run it in blocking mode at session end. Catching a secret before it is committed is dramatically cheaper than revoking it afterward.

---

*SOP-NLT-003 (public edition) v1.0.0 | NeuroLift Technologies | ORG-DEV-OTOI-1.0.4*