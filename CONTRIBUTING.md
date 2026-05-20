# Contributing

This guide gets better with more worked examples and corrections. If you've shipped a first PR (or a tenth) to a major repo and learned something the existing docs don't cover, please send it.

## What fits

- **New worked-example walkthroughs** — full case studies of a real PR, in the style of `docs/01-first-pr-walkthrough.md`. Different ecosystem = high value (e.g., a Rust crate, a Go tool, a Python ML library).
- **Issue-evaluation rules of thumb** — additions to `docs/02-finding-the-right-issue.md`. Concrete: "I skipped this issue because X" with a link.
- **CI failure modes** — additions to `docs/03-passing-ci-checks.md`. Bonus points for a real log excerpt and the fix.
- **Typo fixes, link fixes, factual corrections.**

## What doesn't fit

- Generic "how to use git" tutorials — those already exist, and lots of them
- Lists of repos with "good first issue" labels — point to the curated boards instead
- Badge-farming strategies — this guide is the opposite of that
- Long opinion pieces about open source culture

## Process

1. Open an issue first if your change is more than ~50 lines or introduces a new doc. Quick fixes can go straight to a PR.
2. Fork → branch named for your change → commit → push → PR.
3. Atomic commits, please. One change per commit.
4. PR description should say what changed and why. Link any external evidence (issue you closed, blog post you read, etc.).

## Style

- Markdown only, no HTML unless unavoidable.
- Code blocks: triple backticks with the language tag (` ```bash `, ` ```python `).
- Real URLs, not `example.com`, unless the example is intentionally synthetic.
- Plain prose. No marketing voice. No emoji in headings.

## Code of conduct

Be respectful. Disagree about technical decisions in the PR; never about people.
