# 32851

First, read the [Renovate minimal reproduction instructions](https://github.com/renovatebot/renovate/blob/main/docs/development/minimal-reproductions.md).

Then replace the current `h1` with the Renovate Issue/Discussion number.

## Current behavior

If you have a group of packages configured, and at least one package in the group needs a package.json update while at least one other package in the group needs a lockfile-only update, Renovate re-runs will frequently lose all package.json updates from the PR.

More specifically: On the first run it creates the PR for the group normally. On the second run it finds no package.json updates are needed (because the PR already contains them) but still sees that there's a package with a lockfile-only update, so it redoes the PR with only the lockfile update (throwing away the package.json changes). A third re-run will redo the package.json updates.

## Expected behavior

Re-running Renovate is idempotent, unless actual changes are needed (e.g. an even newer version of something was released).

## Link to the Renovate issue or Discussion

https://github.com/renovatebot/renovate/discussions/32851
