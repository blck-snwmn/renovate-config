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

- **Security-first**: 7-day stabilization period + immediate vulnerability fixes
- **Noise reduction**: Auto-merge patches
- **Simplicity**: No grouping by default (prioritize error identification)

## Key Behaviors

- Patch updates → Auto-merged silently
- Minor/Major updates → Individual PRs
- Vulnerabilities → Immediate PRs (bypass 7-day wait)
- Lock files → Not maintained separately

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