# .github — NeuroLift Technologies Organization Configuration

This repository is the central configuration hub for all repositories in the **NeuroLift Technologies** GitHub organization. GitHub treats this repository specially, using its contents as organization-wide defaults.

## What's in This Repository

### 🏠 Organization Profile
| File | Description |
|------|-------------|
| [`profile/README.md`](profile/README.md) | Public-facing organization profile displayed on the [NeuroLift Technologies GitHub page](https://github.com/NeuroLift-Technologies) |

### 🤝 Community Health Files
These files apply as defaults to **all repositories** in the organization that don't define their own version.

| File | Description |
|------|-------------|
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Guidelines for contributing to our projects |
| [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md) | Community standards and enforcement |
| [`SECURITY.md`](SECURITY.md) | How to report security vulnerabilities |
| [`SUPPORT.md`](SUPPORT.md) | Where to get help |

### 📋 Issue & PR Templates
Default templates used across all repositories in the organization.

| File | Description |
|------|-------------|
| [`ISSUE_TEMPLATE/bug_report.md`](ISSUE_TEMPLATE/bug_report.md) | Template for reporting bugs |
| [`ISSUE_TEMPLATE/feature_request.md`](ISSUE_TEMPLATE/feature_request.md) | Template for suggesting features |
| [`ISSUE_TEMPLATE/config.yml`](ISSUE_TEMPLATE/config.yml) | Issue template chooser configuration |
| [`PULL_REQUEST_TEMPLATE.md`](PULL_REQUEST_TEMPLATE.md) | Default pull request template |

### 🤖 GitHub Copilot Instructions
| File | Description |
|------|-------------|
| [`.github/copilot-instructions.md`](.github/copilot-instructions.md) | Custom coding instructions for GitHub Copilot across all org repos |

### ⚙️ Reusable Workflows
Workflows stored here can be called from any repository in the organization using `uses: NeuroLift-Technologies/.github/.github/workflows/<workflow>.yml@main`.

| File | Description |
|------|-------------|
| [`.github/workflows/reusable-ci.yml`](.github/workflows/reusable-ci.yml) | Reusable CI workflow (lint + test for Python and Node.js projects) |

## How to Use the Reusable CI Workflow

In any repository within this organization, create `.github/workflows/ci.yml`:

```yaml
name: CI
on: [push, pull_request]

jobs:
  ci:
    uses: NeuroLift-Technologies/.github/.github/workflows/reusable-ci.yml@main
    with:
      node-version: '20'
      python-version: '3.12'
```

## References

- [GitHub Docs: Default community health files](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)
- [GitHub Docs: Organization profile README](https://docs.github.com/en/organizations/collaborating-with-groups-in-organizations/customizing-your-organizations-profile)
- [GitHub Docs: Reusable workflows](https://docs.github.com/en/actions/sharing-automations/reusing-workflows)
- [GitHub Docs: Copilot custom instructions](https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot)
