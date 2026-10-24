# Commit Messages

All commits on shared branches follow the Conventional Commits 1.0.0 specification. The message drives the changelog and the SemVer bump, so the format is machine-checked in CI.

## Format

```
<type>(<optional scope>): <subject>

<optional body>

<optional footer(s)>
```

## Allowed types

| Type | Use for | Release impact |
| --- | --- | --- |
| `feat` | A new capability visible to users | minor |
| `fix` | A bug fix visible to users | patch |
| `docs` | Documentation only | none |
| `refactor` | Behavior-preserving restructuring | none |
| `perf` | A measurable performance improvement | patch |
| `test` | Adding or correcting tests | none |
| `build` | Build system or dependency changes | none |
| `ci` | Pipeline and automation changes | none |
| `chore` | Maintenance touching no source or tests | none |
| `revert` | Reverting an earlier commit | patch |

## Scope

The scope names the module, package, or bounded context in parentheses: lowercase, kebab-case, exactly one. If a change spans many scopes, omit the scope rather than stacking several.

## Subject

- Imperative, present tense: "add", not "added" or "adds".
- No trailing period.
- 72 characters or fewer, counting the type and scope prefix.
- Say what changes for the reader of a changelog, not how it was implemented.

## Body

- Wrap at 100 characters.
- Explain the motivation and contrast with the previous behavior.
- Separate from the subject with exactly one blank line.

## Footers

- One per line, token style: `Refs: ABC-123`, `Co-authored-by: ...`.
- The exception is `BREAKING CHANGE:` (see breaking-changes.md), which may contain spaces in the value.

## Examples

```
feat(billing): add usage-based pricing tier
```

```
fix(api): return 409 on duplicate order submission

Previously the server retried internally and occasionally created two
orders. The handler now checks the idempotency key first and returns
409 Conflict with a stable error code when a duplicate is detected.

Refs: ORD-2314
```

```
refactor: extract token refresh into its own service
```

## Why

Consistent messages let release tooling compute version bumps and generate changelogs without human editing, and make `git log --oneline` readable under pressure.
