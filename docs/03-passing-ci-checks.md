# Passing CI Checks

The bot is red. Now what.

## Before you open the PR

You can avoid most CI failures by:

1. **Running the linter locally.** If the repo's CI runs `npm install -g some-lint && some-lint files/`, run the same thing. Read `.github/workflows/*.yml` to see the exact commands — those are the source of truth, not the README.
2. **Reading the workflow files to learn which paths trigger which checks.** A docs change to `docs/foo.md` may not trigger the same checks as a code change to `src/foo.js`. Knowing this lets you scope your patch to minimize CI exposure.
3. **Running the project's test suite, even partially.** `pytest path/to/the/test/that/covers/your/change.py` beats `pytest` when the full suite takes 20 minutes.

## When CI fails

### Step 1: read the actual log, not the GitHub summary

Click into the failed check → click into the failed step → scroll to the first error (often near the bottom). The summary in the PR conversation tab is lossy.

### Step 2: classify the failure

Failures usually fall into one of four buckets:

- **Lint/format** — auto-fix or follow the rule exactly. Most repos have an `npm run lint --fix` or `ruff check --fix` equivalent.
- **Test failure caused by your change** — fix your code, push again.
- **Test failure unrelated to your change** — flaky test, pre-existing breakage, or an upstream dependency moved. Don't try to fix unrelated breakage in your PR. Comment on the PR noting the failure looks unrelated, and ask if a maintainer can rerun.
- **Procedural failure** — missing DCO sign-off, conventional-commit-shape commit message, missing changelog entry. Read the CI output; it usually tells you exactly what's missing.

### Step 3: iterate

```bash
# fix
git add path/to/changed/file
git commit --amend --no-edit         # or a new commit if maintainers prefer
git push --force-with-lease           # if you amended
# or
git push                              # if you added a new commit
```

`--force-with-lease` is safer than `--force` — it refuses to overwrite if anyone else pushed in the meantime. Use it.

CI auto-reruns on the new commit. Watch with:

```bash
gh pr checks --watch
```

## Common gotchas (Windows CMD specifically)

These bit me on a real PR. Now they won't bite you.

### `gh repo fork <repo> --remote=true` fails

```
the `--remote` flag is unsupported when a repository argument is provided
```

`--remote` only applies inside an *existing* clone, where it adds the new fork as a git remote. When you pass a `<repository>` argument, drop `--remote`. The fork-and-clone happens correctly without it.

**Correct:**
```cmd
gh repo fork EbookFoundation/free-programming-books --clone=true
```

The resulting clone already has `origin` (your fork) and `upstream` (the original) configured.

### CMD `^` line continuation only works inside .cmd files, not interactively in PowerShell

If you copy-paste a multi-line `gh pr create ... ^` command into a PowerShell prompt, the `^` becomes a literal character. Use backticks in PowerShell, or run the script as `.cmd` in `cmd.exe`.

### `gh pr create` complains "No commits between A and B"

You forgot to push the branch. Run `git push -u origin your-branch` first.

### `gh pr merge` says "the base branch policy prohibits..." 

Either:
- The repo requires a review before merging — find a reviewer
- Or you have admin rights on your own repo, in which case add `--admin` to override:
  ```cmd
  gh pr merge --squash --delete-branch --admin
  ```
  (Don't `--admin` on repos you don't own — that's how you become unpopular.)

### Commit message body in `git commit -m "..." -m "..."` — multiple `-m` flags create separate paragraphs

```cmd
git commit -m "subject line" -m "first body paragraph" -m "second body paragraph"
```

Each `-m` produces its own paragraph, separated by a blank line. Use this for commit messages with a subject + body without needing to open an editor.

## Don't do this

- **Don't squash a long iteration history into one commit silently.** If your PR had 15 "fix lint" commits, that's fine; tell the maintainer "happy to squash if you prefer" but let them decide.
- **Don't force-push after a maintainer has reviewed.** They lose their place. Add new commits instead, and squash on merge.
- **Don't argue with the linter.** Even if it's wrong. The PR is not the place to relitigate the project's style guide.
- **Don't disable a failing check.** That's not "fixing CI"; that's hiding evidence.
