# Pull Requests

Pull requests are squashed into a single commit on merge, so the PR title becomes the commit message on `main`. Treat the title with the same care as the commit itself.

## Title equals commit message

The PR title must be a valid conventional commit message:

```
feat(billing): add usage-based pricing tier
```

Reviewers reject PRs with titles like "Updates" or "Fix stuff". If a PR contains work of several types, retitle it by the most user-visible change and split the rest into follow-ups.

## Size

- One logical change per PR; two features means two PRs.
- Aim for under 400 changed lines, generated files excluded. Larger PRs need a written rollout plan in the description.

## Description template

```markdown
## What

<one paragraph: what changes, for whom>

## Why

<link to issue or ADR, one paragraph of motivation>

## How tested

<commands or environments where the change was verified>

## Release notes

<the changelog line consumers will read; "none" for internal-only changes>
```

## Merging

- Squash merge only; merge commits and rebase-and-merge are disabled.
- At least one approval from a code owner of each touched area.
- All required checks green; flaky-check retries need a comment.
- The squash body is auto-filled from the PR description; trim boilerplate before confirming.

## Drafts

Open as draft while CI is expected to fail or the shape is still up for debate. Prefixing a title with "WIP:" is not allowed, since it would land in the changelog; use the draft flag instead.

## Why

Because the PR title is the commit message, changelog generation stays fully automatic and the history of `main` reads as a curated log rather than a chat transcript.
