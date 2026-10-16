# github-actions versioning reports major updates as non-breaking

## Current behavior

Renovate proposes a major update of `actions/checkout` from `v3`, but the `matchIsBreaking: true` rule in `renovate.json` does not match it, so the pull request has no `breaking` label.

The `github-actions` versioning declares `isBreaking(version, current)` while Renovate calls it with `(currentVersion, newVersion)`, so it compares every upgrade in reverse and reports it as non-breaking.

## Expected behavior

The major update is breaking, so the rule matches and the pull request has the `breaking` label.

## Link to the Renovate issue or Discussion

The fix is proposed in a pull request; this section will link to it.
