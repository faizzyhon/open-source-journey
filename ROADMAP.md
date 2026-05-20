# Roadmap

What's planned for this guide. Loose ordering, not commitments.

## Recently done

- Initial three docs (`01-first-pr-walkthrough`, `02-finding-the-right-issue`, `03-passing-ci-checks`)
- README reframed from personal log to public guide
- CONTRIBUTING with explicit scope

## Next

- **Walkthrough: contributing to a Python library** — pick a mid-sized library on PyPI (something like `httpx` or `pendulum`) and walk through a real bug fix or doc fix, end-to-end.
- **Walkthrough: contributing to an npm package** — same idea, JavaScript ecosystem. Probably a typed-API package so we can show how the TypeScript type checker becomes part of CI.
- **"Reading CONTRIBUTING.md like a maintainer"** — a checklist of the dozen things you should extract from any project's CONTRIBUTING file before you write a single line of code.

## Eventually

- **A small CLI** (`first-pr` or similar) that, given a target repo URL, scaffolds the fork-clone-branch-commit-push-PR sequence as a CMD/bash script tailored to that repo's conventions. Basically: automate the boring parts of this guide.
- **Translations** — at minimum a Spanish version, since several large OSS projects have Spanish-speaking maintainer bases.
- **A second case-study repo** — pick a repo with strict CI (e.g., requires DCO sign-off, conventional commits, multiple required reviewers) and walk through how to satisfy all of that on a first PR.

## Suggestions

Open an issue with the `idea` label. The bar is "does this help someone shipping their first or fifth OSS PR?". If yes, in scope.
