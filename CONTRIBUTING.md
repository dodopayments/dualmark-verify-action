# Contributing

This repository hosts the **Dualmark Verify** GitHub Action, published to the
GitHub Marketplace. The Marketplace requires the action manifest (`action.yml`)
to live at the repository **root**, which is why this Action lives in its own
repo rather than in the [`dodopayments/dualmark`](https://github.com/dodopayments/dualmark)
monorepo.

## Source of truth

The canonical implementation and the rest of the Dualmark toolchain
(the `@dualmark/cli` this Action wraps, the AEO Specification, adapters, and
docs) live in the monorepo:

> https://github.com/dodopayments/dualmark

Behavioural changes to AEO verification belong there. This repo should only
carry the Action wrapper (`action.yml`), its listing `README.md`, and a
self-test workflow.

## How the Action works

The Action is a **composite action**. It installs Bun and runs the published
CLI from npm:

```bash
bunx @dualmark/cli verify "$URL" --json
```

It does **not** depend on any monorepo-local paths, so it is fully
self-contained.

## Releasing (maintainers)

1. Merge the change to `main`.
2. Cut a release and tag `vX.Y.Z`.
3. Move the floating major tag (e.g. `v1`) to the new release commit.
4. On the GitHub Release, tick **"Publish this Action to the GitHub
   Marketplace"**. GitHub validates the `name:` uniqueness at this step.
