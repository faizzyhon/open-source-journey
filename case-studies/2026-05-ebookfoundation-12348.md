# Case Study: EbookFoundation/free-programming-books #12348

**Date:** 2026-05-19
**Repo:** [EbookFoundation/free-programming-books](https://github.com/EbookFoundation/free-programming-books) (389k★)
**Issue closed:** [#12348 — enhancement: Add "last updated" notation to cast/podcast lists](https://github.com/EbookFoundation/free-programming-books/issues/12348)
**Status:** PR open, CI pending

## The issue

> Cast/podcast lists can become outdated when shows stop publishing new episodes, but it's not always clear which podcasts are still active versus abandoned. This makes it difficult for users to know if they're starting a podcast that's still producing content or one that hasn't released episodes in years.
>
> **Proposed Solution:** Add optional "last updated" notations to cast entries that haven't been updated in 2-3 years (timeframe to be determined).

Filed October 2025, labeled `enhancement`, unassigned, no draft PR linked.

## Why this issue (vs. 33 others)

I screened four issues. Three failed the rubric in `docs/02-finding-the-right-issue.md`:

| Issue | Why skipped |
|---|---|
| #13016 (Add Kannada React playlist) | Submitter gave `youtu.be/...?si=...` URL; CONTRIBUTING forbids shortlinks and tracking params. Real playlist not findable via scrape. |
| #13248 (Trojan website removal) | Reporter only attached screenshots; URL text not in the issue body. |
| #12500 (lint_file `<div>` bug) | Already fixed in current `main` (uses `re.findall`, no longer has the `continue` bug). Issue is stale. |

\#12348 passed all seven rubric checks.

## The patch

7 lines added to `docs/CONTRIBUTING.md`. Two atomic additions:

### Addition 1 — Guidelines section

```diff
 - include the author name or names where appropriate. You can shorten author lists with "`et al.`".
 - if the book is not finished, and is still being worked on, add the "`in process`" notation, as described [below](#in_process).
 - if a resource is restored using the [*Internet Archive's Wayback Machine*](https://web.archive.org) (or similar), add the "`archived`" notation, as described [below](#archived). The best versions to use are recent and complete.
+- if a podcast or screencast has not published a new episode in 2 or more years, add the "`last updated`" notation with the most recent publication month and year, as described [below](#last_updated).
 - if an email address or account setup is requested before download is enabled, add language-appropriate notes in parentheses, e.g.: `(email address *requested*, not required)`.
```

### Addition 2 — Formatting section

```diff
 - <a id="archived"></a>Archived link:

     ```text
     GOOD: * [A Way-backed Interesting Book](https://web.archive.org/web/20211016123456/http://example.com/) - John Doe (HTML) *( :card_file_box: archived)*
     ```
+
+- <a id="last_updated"></a>Last updated podcast or screencast (use when the show has not published a new episode in 2 or more years; record the most recent publication month and year):
+
+    ```text
+    GOOD: * [An Awesome Podcast](https://example.com/podcast) - Jane Roe *( :calendar: last updated: June 2022)*
+    ```

 - <a id="license"></a>Free Licenses (While we include resources that are "All Rights Reserved" but free to read, we encourage the use of free licenses, such as Creative Commons):
```

## Design choices

| Decision | Why |
|---|---|
| Use `:calendar:` as the emoji | Thematically appropriate, GitHub-supported shortcode, not yet used in CONTRIBUTING.md (so it doesn't collide with `:construction:` or `:card_file_box:`) |
| Mirror existing `<a id="..."></a>` anchor pattern | The Guidelines bullet's `[below](#last_updated)` link needs the anchor to exist, and the existing notations (`#in_process`, `#archived`, `#license`) use the same pattern |
| Pick "2+ years" as the threshold | Issue suggested "2-3 years". 2 is the more aggressive end; maintainers are free to bikeshed it during review |
| Only touch `docs/CONTRIBUTING.md`, no list files | Keeps the PR scope minimal and avoids triggering `fpb-lint` (which lints `books/`, `casts/`, `courses/`, `more/` — not `docs/`) |

## CI risk analysis (done before opening the PR)

The repo runs 7 GitHub Actions workflows. Of those, only 3 gate a PR:

| Workflow | Triggers on this PR? | Why |
|---|---|---|
| `fpb-lint.yml` | No-op | Lints `books casts courses more` — not `docs/` |
| `rtl-ltr-linter.yml` | No-op | Only runs on changed RTL files (`*-ar.md`, `*-he.md`, `*-fa.md`, `*-ur.md`) |
| `check-urls.yml` | No-op | Only fires when commit message contains `check_urls=` |
| `comment-pr.yml` | Posts comment after `fpb-lint` runs (just metadata) |
| `detect-conflicting-prs.yml` | Labels conflicts (not gating) |
| `issues-pinner.yml`, `stale.yml` | Housekeeping (unrelated) |

**Expected outcome:** all checks pass on first push because no gating check actually examines the file being modified.

## Commit message

```
docs(CONTRIBUTING): add 'last updated' notation for podcasts/screencasts

Closes #12348

Adds a new optional notation that contributors can apply to podcast or
screencast entries whose shows have not published a new episode in 2 or
more years. The notation follows the same structural pattern as the
existing 'in process' (:construction:) and 'archived' (:card_file_box:)
notations and uses ':calendar:' as its visual marker.

Two changes in docs/CONTRIBUTING.md:

  1. Guidelines section: adds a bullet describing when to apply the
     notation (parallel to the existing 'in process' / 'archived'
     bullets).

  2. Formatting section: adds an example block with an anchor id of
     'last_updated' so the new Guidelines bullet can link to it
     (mirroring the existing #in_process and #archived anchors).
```

## What got hit during execution

The first `gh repo fork` command failed with:

```
the `--remote` flag is unsupported when a repository argument is provided
```

Cause: I used `--remote=true` together with a `<repository>` argument. `--remote` only makes sense inside an existing clone. Removing the flag fixed it. Logged in `docs/03-passing-ci-checks.md` under "Common gotchas (Windows CMD)".

## Outcome

(To be updated once the PR resolves.)

- [ ] CI checks green
- [ ] PR merged
- [ ] Issue #12348 auto-closed
