# 47102: github-actions versioning reports major updates as non-breaking

## Current behavior

Renovate proposes a major update of `actions/checkout` from `v3`, but reports it as non-breaking, so the `matchIsBreaking: true` rule in `renovate.json` does not match it and a pull request for it would get no `breaking` label. A lookup with Renovate 44.155.2 (`LOG_LEVEL=debug renovate --platform=local --dry-run=lookup`) logs:

```
"depName": "actions/checkout"
"currentValue": "v3"
"newVersion": "v7.0.1"
"updateType": "major"
"isBreaking": false
```

The `github-actions` versioning declares `isBreaking(version, current)` while Renovate calls it with `(currentVersion, newVersion)`, so it compares every upgrade in reverse and reports it as non-breaking.

## Expected behavior

The major update is breaking, so the rule matches and the pull request has the `breaking` label.

## Link to the Renovate issue or Discussion

The fix is proposed in [renovatebot/renovate#47102](https://github.com/renovatebot/renovate/pull/47102).
