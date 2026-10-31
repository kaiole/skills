---
name: gcmsg
description: Draft or review commit messages using repository conventions.
---

# Commit messages

## Workflow

1. Inspect repository instructions, commit conventions, and the intended
   diff. Default to staged changes (`git diff --cached`); if nothing is
   staged and the user hasn't specified a scope, inspect `git status` and
   ask which changes to cover. Do not silently combine staged and unstaged
   changes. For a review, compare the supplied message against its diff.
2. Establish the purpose from the diff, conversation, and available issue
   context. Never invent rationale or test results; ask when missing
   context is necessary for an accurate message.
3. Draft or revise the message using the rules below. Flag unrelated
   changes that should be split rather than disguising them with a broad
   subject. Return the proposed message in a plain-text code block; keep
   questions and caveats outside it.
4. Do not stage files, change repository contents, or create or amend
   commits unless explicitly requested. Invoking this skill alone only
   authorizes drafting or reviewing a message.

## Commit message rules

Write for a reader who has only `git log`, `blame` or `bisect`, years from
now, without the ticket, chat, PR or author.

## Convention: match the repo

Check, in order: commitlint/`.czrc` config, `CONTRIBUTING.md`, commit
template, then `git log --no-merges -n 50 --format=%s` (and `-- <path>` for
the area name). Match the dominant prefix style (`type(scope):`, `area:`,
`[Tag]`, none), case after the prefix, and trailer usage. Never introduce a
convention the repo doesn't use. If history is empty or inconsistent:
`area: lowercase summary` when a clear area exists, otherwise a capitalized
plain summary.

## Scope: one logical change

One logical change may have multiple related effects. An "and" in the
subject is a warning to check cohesion, not an automatic reason to split.
Split changes with unrelated motivations. Keep unrelated reformatting,
renames and moves apart from behavior changes. Every commit should build
and pass applicable tests; do not claim verification without evidence.
Tests and docs go in the commit they cover.

## Subject

- Imperative, completing "If applied, this commit will ___".
- Name the specific effect someone would grep for (`Fix off-by-one in ring
  buffer wraparound`), not the file (`Update buffer.c`) or the process
  (`Address review comments`, `Fix CI`, `WIP`, `Phase 1`).
- Aim for 50 characters or fewer, 72 at most. No trailing period.
- Conventional Commits: use the most specific type. `refactor` means no
  behavior change. Never use `chore` for a behavior change. Mark breaking
  changes with `!` and a `BREAKING CHANGE:` footer that says how to migrate.

## Body

Omit it when the subject fully explains the change (typo, version bump,
pure rename). Otherwise, wrap at 72 and cover only what the diff can't
show:

1. **Problem:** what's wrong without this change. Describe it as current
   behavior, in the present tense, with no "Currently". Give the
   user-visible impact; quote exact error messages, which makes them
   searchable.
2. **Why this approach:** name the rejected alternatives a reviewer would
   ask about.
3. **Consequences:** side effects, risks, migration, costs, known
   limitations. Performance claims need numbers.

Rules:

- **Never invent the why.** If the diff, conversation or issue doesn't
  establish the reason, ask, or leave it out. A guessed rationale is worse
  than none.
- Don't restate the diff. No per-file lists, no "This commit…", no
  development diary. Root-cause findings are the exception.
- Self-contained: summarize linked discussions instead of only linking them.
- Write reasoning as prose. Use bullets only for list-shaped content.
- Plain text, no Markdown emphasis or headers. Don't wrap URLs, code or
  error output.
- Use concrete words. Avoid "robust", "seamless", "comprehensive",
  "enhance", "improve" with no object, and "various".
- Cite commits as `git show -s --pretty=reference <rev>` produces them:
  `abc1234 (subject, date)`.

## Trailers

They go last, after a blank line, one per line. Use them only when they're
true and the repo uses them: `Fixes #N` / `Closes #N` (or `Refs #N`),
`Fixes: <sha> ("subject")`, `Co-authored-by: Name <email>`. Never add
`Reviewed-by`, `Tested-by`, `Acked-by` or `Signed-off-by` on someone's
behalf.

## Calibration

Bad:

```
Update cache.ts

- Modified getEntry function
- Updated tests
This commit enhances cache reliability.
```

Good:

```
fix(cache): expire entries by insertion time, not access time

The cache refreshes an entry's timestamp on every read, so a key read
in a tight loop never expires. Rotated credentials stayed cached for
hours after rotation.

Store the insertion time separately and use it for TTL checks; access
time now drives LRU ordering only. Shortening the TTL instead would
raise backend load and leave the bug in place.

Fixes #412
```

Good (no body needed): `docs: fix typo in install steps`
