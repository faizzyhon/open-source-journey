# First PR Walkthrough: a real PR to a 389k-star repo

This is the end-to-end story of one contribution: how the repo was chosen, how the issue was picked, what got cut, what landed.

**Target repo:** [EbookFoundation/free-programming-books](https://github.com/EbookFoundation/free-programming-books) — 389k stars, one of the top five most-starred repositories on GitHub.

**Issue closed:** [#12348 — "enhancement: Add 'last updated' notation to cast/podcast lists"](https://github.com/EbookFoundation/free-programming-books/issues/12348)

**What landed:** Seven lines added to `docs/CONTRIBUTING.md` introducing an optional `last updated` notation for podcast/screencast entries that have gone dormant for 2+ years. Mirrors the existing `in process` and `archived` notation patterns exactly.

## Step 1: pick the repo first, not the issue

The instinct is to find a cool issue and then figure out the repo. Reverse it. Pick a repo where:

- **The maintainers are alive.** Check the commit graph — at least a few merged PRs per week is a good sign.
- **It has a bot that runs on PRs.** A bot doing automated checks means you get fast, mechanical feedback instead of waiting weeks for a human reviewer to point out you missed a lint rule.
- **The contribution surface area is broad.** Repos that accept docs, content additions, and code fixes give you more landing options than a small library that only accepts narrow bug fixes.

EbookFoundation/free-programming-books fits all three: thousands of merged PRs, an active `fpb-lint` GitHub Actions bot, and the contribution surface includes docs, content lists in 30+ languages, podcasts, courses, and the Python linter scripts.

## Step 2: read CONTRIBUTING.md before you do anything else

Not "before you write code" — before you even look at issues. The CONTRIBUTING file tells you what a maintainer-friendly PR looks like for *this specific repo*. For free-programming-books, that turned out to mean:

- Atomic commits (one change per commit)
- No emoji in resource titles
- No URL shorteners, no tracking parameters
- Lists must be in alphabetical order
- Format: `* [Title](URL) - Author (FORMAT) (LICENSE)` — with exact spacing rules
- Different rules for RTL-language files (Arabic, Hebrew, Farsi, Urdu)
- The `fpb-lint` bot enforces formatting; the `awesome_bot` only runs URL validation when the commit message contains `check_urls=`

That last point is what made the eventual PR low-risk: it was a docs-only edit to `CONTRIBUTING.md` itself, and `fpb-lint` only lints `books/`, `casts/`, `courses/`, and `more/` — not `docs/`. So the bot would be a no-op for this PR. Zero CI risk by construction.

## Step 3: triage open issues with a rubric

The repo had 34 open issues. I evaluated four before locking in #12348:

| Issue | What it asked | Verdict | Why |
|---|---|---|---|
| #13016 | Add a Kannada React YouTube series | Skip | Submitter gave a single-video `youtu.be/...?si=...` link with tracking params. CONTRIBUTING forbids both. The actual playlist couldn't be found via static scrape. High rejection risk. |
| #13248 | Remove a Trojan-flagged URL from the Chinese JavaScript list | Skip | Reporter only attached screenshots, no URL text. Without seeing them clearly, no way to locate the offending line. |
| #12500 | Fix `lint_file()` bug with `<div>` tags | Skip | Already fixed in `main` (the function now uses `re.findall` and no longer has the `continue` bug). Issue is stale; PR would be closed as duplicate. |
| #12348 | Add "last updated" notation for podcasts | **Take** | Docs-only change. Mirrors two existing notation patterns. No gating CI check examines `docs/`. Unambiguous "this would help users tell active from abandoned podcasts." |

See `02-finding-the-right-issue.md` for the rubric in detail.

## Step 4: write the smallest possible patch

Final diff was 7 lines added to one file. Two additions to `docs/CONTRIBUTING.md`:

1. **Guidelines section** — one new bullet describing *when* to apply the notation, parallel to the existing `in process` and `archived` bullets.
2. **Formatting section** — one new `<a id="last_updated"></a>` block with a worked example, slotted between the existing `archived` and `license` blocks.

```diff
+- if a podcast or screencast has not published a new episode in 2 or more years, add the "`last updated`" notation with the most recent publication month and year, as described [below](#last_updated).
```

```diff
+- <a id="last_updated"></a>Last updated podcast or screencast (use when the show has not published a new episode in 2 or more years; record the most recent publication month and year):
+
+    ```text
+    GOOD: * [An Awesome Podcast](https://example.com/podcast) - Jane Roe *( :calendar: last updated: June 2022)*
+    ```
```

Small. Verifiable. Mirrors existing structural patterns. Nothing to argue about.

## Step 5: prepare the PR like you're the maintainer

The PR description should make the maintainer's job trivial. Mine had:

- `Closes #12348` on the first line (auto-closes the issue on merge)
- A two-sentence summary
- "What changes" with the literal Markdown sections being edited
- A worked example
- "Why this approach" explaining the threshold choice and that no list files were touched
- A checklist showing every CONTRIBUTING rule was satisfied

The reviewer should be able to approve in under 60 seconds.

## Step 6: open the PR, watch CI, and don't panic

Even on a perfect-looking patch, CI can fail for reasons unrelated to your code (a flaky test, an upstream change that landed an hour ago, a self-inflicted typo). See `03-passing-ci-checks.md` for the iteration loop.

## What this taught me

- **Repos before issues, every time.** A perfect issue in an inactive repo is worth nothing.
- **The CONTRIBUTING file is the spec.** Read it before you write a line.
- **Most "good first issues" are bad first issues.** The easy ones get sniped within hours; what's left is often subtle, stale, or politically contested. Better to do a clean docs/content add that exactly satisfies CONTRIBUTING than to chase a `good first issue` label.
- **Small patches merge.** Aim for under 10 lines on your first PR. Save the ambitious refactor for your tenth.
