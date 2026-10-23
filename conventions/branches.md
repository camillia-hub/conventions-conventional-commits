# Branch Naming

Branch names are derived from the commit type they will land as, so reviewers can predict the changelog impact from the branch list alone.

## Format

```
<type>/<scope>-<topic>
```

- `type`: one of the allowed commit types (see commit-messages.md).
- `scope`: the primary module touched, kebab-case.
- `topic`: two to five kebab-case words describing the change.

Lowercase only, hyphens as separators, and exactly one slash between type and the rest.

## Examples

```
feat/billing-usage-tiers
fix/api-duplicate-order-409
docs/onboarding-quickstart
refactor/auth-token-service
test/payments-retry-matrix
chore/deps-quarterly-bump
```

No scope applies cleanly? Omit it and use `<type>/<topic>`:

```
ci/kind-cache-tuning     (right)
ci/kinD-cache-tuning     (wrong: uppercase)
chore/license-year-bump  (right: no scope, plain topic)
```

## Long-lived branches

Only two branches live longer than a sprint:

- `main`: always releasable; every commit passes CI.
- `release/x.y`: short-lived stabilization branch cut from `main` when a minor release needs soak time; deleted after the tag is pushed.

Hotfixes branch from the latest tag, not from `main`:

```
fix/api-timeout-regression    (branched from tag v2.4.1)
```

## Lifespan

A topic branch lives for days, not weeks. Rebase onto `main` before opening the pull request; delete the branch after merge.

## Why

A predictable branch namespace lets automation map branches to pipelines (test packs for `test/...`, deploy previews for `feat/...`) and keeps `git branch` output scannable during release triage.
