# CI Standards

Reusable GitHub Actions workflows that each project repo can call with:

- `uses: eyuel23/ci-standards/.github/workflows/<workflow>.yml@<tag>`

## Workflows

```text
.github/workflows/
  node-baseline.yml
  dependency-review.yml
  codeql-js-ts.yml
  secret-scan.yml
```

## Versioning

Tag releases and pin callers to tags (not `main`):

```bash
git tag v2.1
git push origin v2.1
```

## v2 Notes

1. `dependency-review.yml` is private-repo-safe by default:
   - private repos skip dependency review unless `run_on_private: true` is set.
2. `secret-scan.yml` uses direct `gitleaks` CLI scanning, which is PR-safe in private repos.
3. Check names remain stable:
   - `baseline / quality`
   - `dependency-review / dependency-review`
   - `secret-scan / gitleaks`
   - `codeql / analyze`

## Using Dependency Review In Private Repos

By default, private repos do:

- skip dependency review (green status with explicit skip log)

If your private repo supports dependency review and you want it enforced:

```yaml
jobs:
  dependency-review:
    uses: eyuel23/ci-standards/.github/workflows/dependency-review.yml@v2
    with:
      run_on_private: true
```
