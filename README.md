# Reusable GitHub Actions Workflows

![CI](https://github.com/Kishore2488/github-actions-reusable-workflows/actions/workflows/ci.yml/badge.svg)

A small library of `workflow_call` workflows — the kind of paved-road tooling I'd set up so every repo on a team doesn't reinvent its own Docker-build-and-push or Python-test job.

## What's here

- `reusable-docker-build-push.yml` — build a Docker image and optionally push it to GHCR, parameterized by image name and Dockerfile path.
- `reusable-python-test.yml` — install deps, lint, and run pytest, parameterized by the app directory.
- `ci.yml` — a working example in this same repo: it calls `reusable-python-test.yml` against the sample app in `examples/sample-app/`, so the reusable workflow is proven out, not just declared.

## Using one of these from another repo

```yaml
jobs:
  test:
    uses: Kishore2488/github-actions-reusable-workflows/.github/workflows/reusable-python-test.yml@main
    with:
      app-path: app
```

## Why reusable workflows over copy-paste

When ten repos each hand-roll their own "install, lint, test" job, fixing a flaky step means ten PRs. A reusable workflow means one change in one place, and every caller picks it up on their next run.
