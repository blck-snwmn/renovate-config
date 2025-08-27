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

- **Security-first**: 14-day stabilization period + immediate vulnerability fixes
- **Noise reduction**: Auto-merge patches + scheduled updates
- **Simplicity**: No grouping by default (prioritize error identification)

## Key Behaviors

- Patch updates → Auto-merged silently
- Minor/Major updates → Individual PRs
- Vulnerabilities → Immediate PRs (bypass 14-day wait)
- Lock files → Auto-updated Monday mornings

## Customization Example

Add grouping for your project if needed:

```json
{
  "extends": ["github>blck-snwmn/renovate-config"],
  "packageRules": [
    {
      "matchPackagePatterns": ["eslint"],
      "groupName": "eslint"
    }
  ]
}
```