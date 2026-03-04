# Migration to v2

Use this when upgrading project repos from `@v1` to `@v2`.

## Important patch

If you are using `@v2`, upgrade to `@v2.1` for `secret-scan`.
`@v2` uses a removed gitleaks install script URL and can fail with HTTP 404.

## 1) Update Workflow References

In each project repo:

1. `@v1` -> `@v2` (or `@v2.1`) for all `eyuel23/ci-standards` workflow calls.

## 2) Dependency Review Behavior

`dependency-review` now defaults to private-repo-safe mode:

1. Private repos skip dependency review unless `run_on_private: true`.
2. Public repos run dependency review as normal.

If your private repo supports dependency review and you want enforcement:

```yaml
jobs:
  dependency-review:
    uses: eyuel23/ci-standards/.github/workflows/dependency-review.yml@v2.1
    with:
      run_on_private: true
```

## 3) Secret Scan Behavior

`secret-scan` runs `gitleaks` via CLI, stable for private PRs and avoids GitHub API PR commit permission issues.

## 4) Re-check Branch Protection

After first run, verify required checks on `main`:

1. `baseline / quality`
2. `dependency-review / dependency-review`
3. `secret-scan / gitleaks`
4. `codeql / analyze` (JS/TS repos only)
