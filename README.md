# First OSS PR — A Tested Playbook

A practical, opinionated guide for shipping your **first open source pull request to a major repository**, written by someone who just did it. Every step is taken from a real, working contribution — no hypotheticals.

## The guide

- **[docs/01-first-pr-walkthrough.md](./docs/01-first-pr-walkthrough.md)** — Full case study: picking the repo, reading CONTRIBUTING.md, writing the patch, opening the PR, surviving CI.
- **[docs/02-finding-the-right-issue.md](./docs/02-finding-the-right-issue.md)** — Seven-step rubric for evaluating open issues *before* you sink time into them, with four real worked examples.
- **[docs/03-passing-ci-checks.md](./docs/03-passing-ci-checks.md)** — Debugging CI failures, common Windows CMD gotchas, and how to iterate without making it worse.

## Receipts — every repo, PR, and badge

- **[PR_LOG.md](./PR_LOG.md)** — Every PR opened across every repo. Numbered, dated, with status and bot results.
- **[ACHIEVEMENTS.md](./ACHIEVEMENTS.md)** — Honest log of which GitHub achievements were earned, on what date, and how. Includes notes on which ones not to fake.
- **[case-studies/](./case-studies/)** — Full per-PR records.
  - **[2026-05-ebookfoundation-12348.md](./case-studies/2026-05-ebookfoundation-12348.md)** — The first real external PR: 7-line patch to EbookFoundation/free-programming-books (389k★) closing issue #12348. Full diff, design decisions, CI risk analysis, what got hit during execution.
  - **[2026-05-badge-session.md](./case-studies/2026-05-badge-session.md)** — The badge-earning run, honestly recorded. Pull Shark + YOLO + Quickdraw in one CMD script, plus what's legitimate about it and what isn't.

## Repos involved

| Repo | Role | Why |
|---|---|---|
| [faizzyhon/open-source-journey](https://github.com/faizzyhon/open-source-journey) | Owned | This guide. |
| [EbookFoundation/free-programming-books](https://github.com/EbookFoundation/free-programming-books) | External (389k★) | First real-world contribution target. |

## Who this is for

- You've never had a PR merged outside your own org
- You can read code in at least one language, or you're comfortable in Markdown and want to start with docs
- You want to contribute to a real, used project — not just a "first-contributions" practice repo

## Who this isn't for

- You're farming achievements. There are faster ways, but they don't make you a contributor. ([ACHIEVEMENTS.md](./ACHIEVEMENTS.md) has the honest take.)
- You want a curated list of "good first issue" labels — see [Awesome for Beginners](https://github.com/MunGell/awesome-for-beginners) or [goodfirstissue.dev](https://goodfirstissue.dev).

## Quick start

1. Read **[docs/01-first-pr-walkthrough.md](./docs/01-first-pr-walkthrough.md)** end-to-end. ~10 minutes.
2. Pick **one** target repo from your stack.
3. Run through the rubric in **[docs/02-finding-the-right-issue.md](./docs/02-finding-the-right-issue.md)**. Skip anything that fails — don't romance hard ones.
4. Write the smallest possible patch. Read CONTRIBUTING.md *before* you write code.
5. When CI fails, use **[docs/03-passing-ci-checks.md](./docs/03-passing-ci-checks.md)**.

## Contributing to this guide

See [CONTRIBUTING.md](./CONTRIBUTING.md).

## License

MIT — see [LICENSE](./LICENSE).
