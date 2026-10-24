# Versioning and Releases

Releases follow Semantic Versioning 2.0.0 and are tagged in git. The tag, the release notes, and the version bump are all derived from the conventional commits since the previous tag.

## SemVer rules

Given `MAJOR.MINOR.PATCH`, bump the first applicable:

- MAJOR: any commit with `BREAKING CHANGE` or `!` since the last release.
- MINOR: otherwise, at least one `feat` commit exists.
- PATCH: otherwise, at least one `fix`, `perf`, or `revert` commit exists.
- No release: only `docs`, `test`, `chore`, `build`, `ci`, `refactor` commits.

Before 1.0.0 the contract is not yet stable: breaking changes bump MINOR and features bump PATCH.

## Tag format

```
v<MAJOR>.<MINOR>.<PATCH>
```

Lowercase `v`, no zero-padding, no suffixes on final tags: `v1.0.0`, `v2.4.1`. Pre-releases append a dot-separated identifier:

```
v2.5.0-rc.1
v2.5.0-beta.2
```

Tags are created by the release automation on `main`, annotated and signed. Nobody pushes tags by hand.

## Release cadence

- Patch: on demand, whenever a `fix` worth shipping lands.
- Minor: every second Wednesday (the release train). Miss the train, wait for the next one.
- Major: scheduled, announced at least four weeks ahead, shipped with a migration guide.

## Release notes

Generated from conventional commits, grouped in this order:

1. Breaking changes
2. Features
3. Fixes
4. Performance
5. Reverts
6. Miscellaneous (docs, chores, ci), collapsed by default

## Hotfixes

1. Branch `fix/<topic>` from the affected tag.
2. Land the fix with a `fix:` commit.
3. Tag the next patch version on that branch.
4. Merge the fix back into `main`.

## Why

A boring, clockwork release process means consumers can subscribe to patch updates with confidence, and the team never negotiates "is this worth a release" in a chat thread.
