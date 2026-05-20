# Finding the Right Issue

A rubric for evaluating an open issue *before* you sink an evening into it.

## The rubric, in one screen

Go through these in order. The first **No** kills the issue. Don't try to rescue it.

1. **Is the issue still open and unassigned, with no draft PR open against it?**
   Use the GitHub search filters: `is:open is:issue no:assignee -linked:pr`. If a PR is already linked, your work duplicates someone else's.

2. **Was it opened within the last ~12 months, or has it been touched (commented on, labeled) recently?**
   Issues older than a year with no activity are often "we don't care enough to close it" issues. Maintainers may not engage.

3. **Is the acceptance criterion concrete?**
   A good issue says "do X and the result should be Y". A bad issue says "the docs feel confusing" or "we should rethink the API". Skip the latter unless you're already a contributor.

4. **Can you write the patch in under 50 lines of changed code (or one new doc page)?**
   Big patches require maintainer buy-in *before* you write them. Without that, you'll get "thanks but we want to think about this differently" after spending a week.

5. **Will the change touch only files where you understand the conventions?**
   If the file lives in an area governed by rules you haven't read (formatting standards, naming conventions, public API contracts), pause and read those first — or pick a different issue.

6. **Does the repo's CI gate any of the files you'd be touching?**
   If yes, you need to be able to run that CI locally (or be willing to iterate via push-and-wait). If you can't run the linter, you'll be guessing.

7. **Has the maintainer publicly said "PRs welcome" on this issue or the issue's label?**
   The `good first issue` / `help wanted` / `accepting PRs` labels are signal. A maintainer comment saying "feel free to send a PR" is even better signal. Bare unanswered issues are weaker signal.

If all seven are Yes, take the issue. If any are No, move on. There's no shortage of issues.

## Worked examples (free-programming-books, May 2026)

These are real evaluations from one triage session.

### #13016 — "Add Kannada React series link" → SKIP

| Step | Check | Result |
|---|---|---|
| 1 | Open, unassigned, no linked PR | Pass |
| 2 | Opened Nov 2025, no activity | Borderline |
| 3 | Acceptance criterion concrete | **Fail** — submitter gave a `youtu.be/VIDEO?si=TRACKING` URL, but CONTRIBUTING forbids shortlinks and tracking params, and discourages single videos. No clear path to a CONTRIBUTING-compliant entry without the submitter re-supplying data. |

**Verdict:** Skip. The issue isn't actionable without back-and-forth with the submitter, which makes it a multi-week play, not a first-PR play.

### #13248 — "Trojan website, search with javascript in chinese language" → SKIP

| Step | Check | Result |
|---|---|---|
| 1 | Open, unassigned, no linked PR | Pass |
| 2 | Opened May 2026 | Pass |
| 3 | Acceptance criterion concrete | **Fail** — reporter attached screenshots showing the offending link "marked yellow" but provided no URL text in the issue body. |

**Verdict:** Skip. Without the screenshot being legible enough to identify the line in the Chinese JavaScript file, you'd be guessing. A "remove malware" PR that targets the wrong line is worse than no PR.

### #12500 — "Fix lint_file() fails to process lines containing both opening and closing <div> tags" → SKIP

| Step | Check | Result |
|---|---|---|
| 1 | Open, unassigned, no linked PR | Pass |
| 2 | Opened Oct 2025, stale | Borderline |
| 3 | Acceptance criterion concrete | Pass — "remove premature `continue` statements" |
| 4 | Under 50 lines | Pass |
| 5 | Understand conventions | Pass |
| 6 | Can run CI | Possible (Python script, has tests) |
| 7 | "PRs welcome" signal | Pass — labeled `bug` |

But: **a quick read of the current `scripts/rtl_ltr_linter.py` showed the function already uses `re.findall` and no longer has the bug.** The issue is stale; the fix has landed but the issue was never closed. Submitting a "fix" PR would get closed as duplicate.

**Verdict:** Skip. Always check whether the current main-branch code actually has the bug before writing the fix.

### #12348 — "Add 'last updated' notation to cast/podcast lists" → TAKE

| Step | Check | Result |
|---|---|---|
| 1 | Open, unassigned, no linked PR | Pass |
| 2 | Opened Oct 2025 | Pass |
| 3 | Acceptance criterion concrete | Pass — proposed format given: `*(last updated: June 2022)*` |
| 4 | Under 50 lines | Pass (turned out to be 7 lines) |
| 5 | Understand conventions | Pass — existing `in process` and `archived` notations are templates to mirror |
| 6 | Can run CI | Pass — `fpb-lint` doesn't lint `docs/`, so CI is a no-op |
| 7 | "PRs welcome" signal | Pass — labeled `enhancement` |

**Verdict:** Take. All seven Yes. Patch turned out to be a 7-line docs change with zero CI risk.

## When in doubt

Bias toward the smallest, most boring issue that passes the rubric. Boring issues merge. Exciting issues stall.
