# CI Standards Template Repo

Use this folder as the source for a dedicated GitHub repository, for example:

- `eyuel23/ci-standards`

This repo hosts reusable workflows. Each project repo then keeps tiny caller workflows that reference a tagged version (for example `@v1`).

## Structure

```text
ci-standards/
  .github/workflows/
    node-baseline.yml
    dependency-review.yml
    codeql-js-ts.yml
    secret-scan.yml
```

## Publish Process

1. Create repo `ci-standards`.
2. Copy this folder's contents into that repo root.
3. Commit and push.
4. Create a version tag:

```bash
git tag v1
git push origin v1
```

5. Project repos should reference `@v1` in `uses:`.

## Update Process

1. Make workflow changes in `ci-standards`.
2. Tag a new version (`v1.1`, `v2`, etc).
3. Bump caller references in each project repo when ready.
