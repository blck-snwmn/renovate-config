# renovate-config

Shareable Renovate config with language-agnostic best practices.

## Usage

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>blck-snwmn/renovate-config"]
}
```

## Design Principles

- **Security-first**: Every dependency is pinned to an exact version, and new releases wait 7 days before Renovate proposes them, so a malicious or broken version published right after release is not picked up. Vulnerability fixes skip the wait.
- **Noise reduction**: Low-risk updates (patches, and minor updates of dev tools) are auto-merged once checks pass; everything else gets its own PR for review.
- **Simplicity**: No custom grouping (prioritize error identification). Only Renovate's recommended monorepo groups apply.

## Key Behaviors

- Versions → Pinned exactly (`:pinAllExceptPeerDependencies`); `peerDependencies`, `engines` and Python `requires-python` stay as ranges
- New releases → Proposed after 7 days (`minimumReleaseAge`)
- Patch updates → Auto-merged when checks pass
- Minor updates → Auto-merged when checks pass for:
  - Tools managed by aqua, and aqua itself
  - GitHub Actions (runtime versions passed via `with:`, such as `node-version`, still get a PR)
  - Linters, formatters, type definitions and package managers (`oxlint`, `oxfmt`, `ruff`, `pnpm`, `@types/**`, etc.)
- Other minor and all major updates → Individual PRs
- Vulnerabilities → Immediate PRs labeled `security` (bypass the 7-day wait)
- `.python-version` → Exact versions are looked up on python.org, so they stay in step with the Python version in `pyproject.toml` / uv
- Post-update cleanup → `go mod tidy` for Go, dedupe for npm / pnpm
- Lock file maintenance → Disabled; lock files change only alongside dependency updates
- Schedule → None; PRs are created whenever updates become available (up to 10 open at a time)

## Customization Example

Add grouping for your project if needed:

```json
{
  "extends": ["github>blck-snwmn/renovate-config"],
  "packageRules": [
    {
      "matchPackageNames": ["/eslint/"],
      "groupName": "eslint"
    }
  ]
}
```
