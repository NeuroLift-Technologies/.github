# REVIEW.md — Review Format

This file defines the canonical format for agent-conducted reviews in NeuroLift Technologies **public** repositories. Agents performing code, content, or security review should follow this structure so reviews are consistent and easy for a maintainer to act on.

> **Start here:** [`governance.yaml`](governance.yaml) is the authoritative machine-readable contract (`ORG-DEV-OTOI-1.0.4`) and [`AGENTS.md`](AGENTS.md) is the agent-facing guide. If anything in this file disagrees with `governance.yaml`, `governance.yaml` wins.

## Review Metadata

**Reviewer:** [Agent name / platform]
**Review Date:** [ISO 8601 date]
**Review Type:** [Code | Content | Security]
**Scope:** [Files, pages, or sections reviewed]
**Governance Version:** ORG-DEV-OTOI-1.0.4

## Pre-Review Checklist

- [ ] Read `governance.yaml` and `AGENTS.md`, and understood the guardrails
- [ ] Identified the review scope and what is being evaluated
- [ ] Checked the linked issue and prior discussion for context and intent
- [ ] Verified the review format matches this template

## Review Findings

### Summary

[One paragraph: overall assessment of what was reviewed, key themes, and general verdict.]

### Strengths

- [What works well — be specific]
- [What's technically sound]
- [How it serves the people this project is for]

### Issues

#### 🔴 Critical (must fix before merge)

| # | File:Line | Issue | Recommended Fix |
|---|---|---|---|
| — | — | _No critical issues_ | — |

> 💡 **Note:** Remove all placeholder rows before submitting a final review. Placeholder rows (marked with `_No ... issues_`) must not be treated as real findings. If no issues exist at a severity level, leave the table with a single "No issues" row or omit the table entirely.

#### 🟡 High Priority (should fix soon)

| # | File:Line | Issue | Recommended Fix |
|---|---|---|---|
| — | — | _No high-priority issues_ | — |

> 💡 **Note:** See above — remove placeholder rows before final submission.

#### 🟢 Low Priority / Observations

- [Non-blocking suggestions, style notes, future improvements]

### Factual Accuracy

- [ ] All external claims (names, dates, statistics) verified against authoritative sources
- [ ] No hallucinated organizations, numbers, or URLs
- [ ] Sources cited where applicable

### Governance Compliance

- [ ] No credentials or secrets exposed
- [ ] No LLM or AI provider lock-in introduced
- [ ] No architecture decisions made unilaterally by an agent
- [ ] No new external integrations added without maintainer approval
- [ ] Commit format follows `[AGENT_NAME] type(scope): description`
- [ ] Session registration and handoff record written, if the change was agent-authored (see [`templates/`](templates/))

## Verdict

**Status:** [APPROVED / CHANGES REQUESTED / BLOCKED]

**Rationale:** [One paragraph explaining the verdict and what needs to happen next.]

## Handoff Notes

**Next reviewer / agent needs to know:**
- [What was reviewed and what wasn't]
- [Any outstanding items or follow-ups]
- [Where to find related context]

---

*Review format for NeuroLift Technologies public repositories | ORG-DEV-OTOI-1.0.4*