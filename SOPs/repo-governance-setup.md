# SOP: Repository Governance Setup (Public Edition)

**SOP ID:** SOP-NLT-002 (public edition)
**Version:** 1.0.0
**Scope:** Setting up governance files in a NeuroLift Technologies **public** repository
**Governed by:** ORG-DEV-OTOI-1.0.3

## Purpose

This SOP explains how to give a public NeuroLift Technologies repository the governance files that coding agents need — without duplicating what the organization already provides.

## First: Know What You Already Inherit

GitHub treats [`NeuroLift-Technologies/.github`](https://github.com/NeuroLift-Technologies/.github) specially: its community health files are **org-wide defaults** for every public repository that does not define its own. You already get, for free:

- `AGENTS.md` — the agent-facing contributor guide
- `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SECURITY.md`, `SUPPORT.md`
- `GOVERNANCE.md`, `governance.yaml`, `governance.json`
- `ISSUE_TEMPLATE/` (including the Agent Escalation form) and `PULL_REQUEST_TEMPLATE/`

**So most repositories need nothing beyond what they inherit.** Add a local copy only when the repository genuinely deviates, and remember: **a local file overrides the org default for that repository.** Duplicating a file you agree with is how defaults drift out of sync.

## When to Use This SOP

- Creating a new public NLT repository
- Auditing a public repository's governance coverage
- A repository needs conventions that differ from the org defaults

## Minimum Files for a Public Repository

| File / Directory | Why | Needed if… |
|---|---|---|
| `AGENTS.md` | Agent guide and commit format | The repo deviates from the org default |
| `CLAUDE.md` | Session directive pointing at the governance contract | You want repo-specific context for agents |
| `REVIEW.md` | Canonical review format | Maintainers want a consistent review shape |
| `templates/` | Session registration + handoff schemas | Agents will register and hand off |
| `docs/active-threads.md` | Current work state | More than one contributor works in parallel |
| `SECURITY.md` | **Private** channel for vulnerability reports | **Always** — never accept secret reports in public issues |

## Step-by-Step Procedure

### Step 1: Create `CLAUDE.md` (optional but recommended)

```markdown
# CLAUDE.md — [REPO NAME]

You are working in a NeuroLift Technologies public repository.

**Read first:**
1. Governance contract (machine-readable, ORG-DEV-OTOI-1.0.3):
   https://github.com/NeuroLift-Technologies/.github/blob/main/governance.yaml
2. Agent guide:
   https://github.com/NeuroLift-Technologies/.github/blob/main/AGENTS.md
3. Review format:
   https://github.com/NeuroLift-Technologies/.github/blob/main/REVIEW.md
4. Project context: `README.md` (this repo)
5. Active threads: `docs/active-threads.md` (this repo, if present)

**Non-negotiable:** maintainers decide architecture, dependencies, and deployment.
Escalate by opening an Agent Escalation issue. Do not guess.

**Governed by:** ORG-DEV-OTOI-1.0.3
```

### Step 2: Copy `REVIEW.md` and `templates/` If You Use Them

Take them from the public hub rather than rewriting them, so the whole organization reviews against one format. Link to them rather than inlining copies where you can.

### Step 3: Add `docs/active-threads.md`

If more than one contributor works in parallel, a short shared file beats guesswork:

```markdown
# Active Threads

| Thread | Owner | Status | Notes |
|---|---|---|---|
| [what] | [who] | in progress / blocked / review | [context] |
```

### Step 4: Confirm `SECURITY.md` Exists

The org default supplies one. If you override it, it **must** still route security reports to a private channel. A public issue describing a leaked credential republishes the secret.

### Step 5: Verify Every Link Resolves

> **This step prevents the most common governance failure.** Governance docs that point at URLs which do not exist are worse than no docs: they send agents down dead ends and look authoritative while doing it.

Before merging any governance file:

```bash
# Extract URLs and report any that do not resolve
grep -ohE 'https://[^ )>\"]+' AGENTS.md CLAUDE.md REVIEW.md SOPs/*.md 2>/dev/null \
  | sort -u \
  | while read -r u; do
      code=$(curl -s -o /dev/null -w '%{http_code}' -L "$u")
      [ "$code" = "200" ] || echo "$code  $u"
    done
```

Any non-`200` is a defect. Fix the link or remove the claim — never leave it "aspirational."

### Step 6: Audit Checklist

Before calling a repository governed:

- [ ] `SECURITY.md` resolves and routes reports to a **private** channel
- [ ] Every governance URL in every governance file returns `200`
- [ ] `AGENTS.md` (inherited or local) states the commit format and the escalation route
- [ ] `CLAUDE.md`, if present, points at `governance.yaml` and the agent guide
- [ ] `templates/` are reachable if the docs tell agents to use them
- [ ] No local copy of an org default exists "for clarity" — link instead
- [ ] No credentials, tokens, or internal-only URLs appear in any governance file

## What This SOP Deliberately Leaves Out

This is the public edition. It does **not** cover internal-only machinery — session hook templates, automated propagation workflows, internal repository setup, or internal escalation contacts. Those live in the internal governance repository, which governs internal and private repositories.

If you are looking for instructions on configuring Claude Code session hooks or org-wide propagation across internal repositories, you are reading the wrong edition.

## Why There Is No Automatic Sync

The public governance hub is **hand-authored**, not mirrored from any internal repository. That is a deliberate decision: internal governance describes internal machinery (bot configuration, branch protection, internal file maps) that has no business in a public repository, and an automatic mirror would publish it.

The practical consequence: public governance is maintained here, by hand, and reviewed like any other change. See [`CONTRIBUTING.md`](../CONTRIBUTING.md) for how to propose a change to it.

---

*SOP-NLT-002 (public edition) v1.0.0 | NeuroLift Technologies | ORG-DEV-OTOI-1.0.3*