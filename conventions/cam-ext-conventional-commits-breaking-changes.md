# Breaking Changes

A breaking change is any change that can force a consumer, integrator, or operator to modify their code, configuration, or workflow. Breaking changes are announced in the commit message and always trigger a major SemVer bump.

## Marking a breaking change

Two equivalent markers:

1. An exclamation mark after the type or scope: `feat(api)!: drop v1 endpoints`
2. A `BREAKING CHANGE:` footer at the end of the message.

Use both when the change deserves a detailed explanation: the `!` flags it in log views, the footer explains the migration.

## Footer format

```
feat(api)!: require authentication on all read endpoints

Anonymous read access is removed. Clients must send an access token
with every request.

BREAKING CHANGE: anonymous read access is removed; clients must send
an access token with every request. Migrate by adding the
Authorization header before upgrading to v3.0.0.
```

The footer text must describe the impact and the migration path, not just restate the title.

## What counts as breaking

- Removing or renaming a public endpoint, field, event, or CLI flag.
- Changing the type or meaning of an existing field.
- Tightening validation on previously accepted input.
- Dropping support for a platform, runtime version, or configuration.
- Changing default behavior in a way users can observe.

Not breaking: adding optional fields, adding new endpoints, widening accepted input, fixing a bug that restores documented behavior.

## SemVer mapping

| Commit signal | Bump | Example |
| --- | --- | --- |
| `BREAKING CHANGE` or `!` | major | 2.4.1 -> 3.0.0 |
| `feat` | minor | 2.4.1 -> 2.5.0 |
| `fix`, `perf`, `revert` | patch | 2.4.1 -> 2.4.2 |
| everything else | none | no release |

## Reverts

```
revert: feat(api): require authentication on all read endpoints

This reverts commit 9f1e2ab. Mobile builds older than two weeks were
locked out; re-shipping behind a migration window.
```

## Why

Downstream teams plan upgrades from the changelog alone. An accurate breaking-change signal is the difference between a safe automated patch update and a 2 a.m. incident.
