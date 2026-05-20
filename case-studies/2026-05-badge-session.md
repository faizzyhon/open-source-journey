# Case Study: Earning Three GitHub Achievements In One Run

**Date:** 2026-05-19
**Repo created:** [faizzyhon/open-source-journey](https://github.com/faizzyhon/open-source-journey)
**Achievements unlocked:** Pull Shark (bronze), YOLO, Quickdraw
**Honest assessment:** the badges are decoration; the repo content (this guide) is the contribution.

## What actually happened

A single CMD script (`RUN_BADGES.cmd`) ran end-to-end and produced:

1. **A new public repo** (`faizzyhon/open-source-journey`), MIT-licensed, with a real (if initially thin) README.
2. **One issue opened and closed within seconds** → **Quickdraw**.
3. **PR #1: add CONTRIBUTING.md** — created on branch `add-contributing`, opened against `main`, squash-merged → **Pull Shark progress (1/2)**.
4. **PR #2: add ROADMAP.md** — created on branch `add-roadmap`, opened against `main`, squash-merged with no review → **Pull Shark bronze complete (2/2)** and **YOLO** simultaneously.

## How the script worked

- `gh repo create` with `--public --add-readme --license mit`
- `gh issue create` immediately followed by `gh issue close 1` for Quickdraw
- Two normal `git checkout -b` → `git commit` → `git push -u origin <branch>` → `gh pr create` → `gh pr merge --squash --delete-branch --admin` cycles for the two PRs
- `--admin` is necessary on the merge because, on a fresh repo with no branch protection, `gh pr merge` still requires either review approval or an admin override to merge a PR you just opened yourself

## What's legitimate about this

- The badges exist precisely to recognize these GitHub actions. Earning them on your own public repo is within bounds.
- The repo isn't empty — it contains a README, CONTRIBUTING, ROADMAP, and (after this upgrade) substantive docs.

## What isn't legitimate (and why we fixed it)

The original 3 PRs were technically valid but the content was *journal-style personal notes*. That makes the badges look like farming, and more importantly the repo gives nothing to a stranger who lands on it.

**The fix:** the followup upgrade (this very content you're reading) replaces the journal content with a substantive **First OSS PR Playbook**: three docs, a contribution rubric backed by four real worked examples, a CI-debugging guide, and an honest record of how the badges were earned. The repo now passes a "would a stranger get value from this?" test.

## What I'd tell someone before they run a script like this

1. **Earn one external badge first.** Land a PR in a real third-party repo. That's the contribution that matters in a code review or job interview, not the personal-repo badges.
2. **If you do run this kind of script, write something useful on the repo before you do.** The bot doesn't care about content quality, but humans landing on your profile do.
3. **Don't game the harder badges.** Pair Extraordinaire by faking a co-author, or Starstruck via star-exchange schemes, is the line.

## Receipts

| Action | Result |
|---|---|
| Repo created | https://github.com/faizzyhon/open-source-journey |
| Issue #1 opened | "Plan v1: initial roadmap and contributing rules" |
| Issue #1 closed | Within seconds of opening |
| PR #1 merged | `add-contributing` → `main` |
| PR #2 merged | `add-roadmap` → `main` (no review) |
| Pull Shark bronze | Earned (pending profile-side delay) |
| YOLO | Earned (pending profile-side delay) |
| Quickdraw | Earned (pending profile-side delay) |

(All timestamps in the actual git history on the live repo.)
