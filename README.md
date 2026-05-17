# GitHub Team Arena

A single-file dashboard that turns a GitHub repo into a friendly leaderboard. Track commits, review comments, and merged PRs across **all branches** and see who's on fire this week.

![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)

## Features

- **Leaderboards** — top contributors for commits, review comments, and merged PRs, with medals for the top 3 and a 🔥 badge for users who are over the daily threshold today.
- **Heatmap tables** — commits and reviews per user per day, plus merged PRs per user per week.
- **Drill-down drawer** — click any highlighted cell or leader card to see the underlying commits, review comments, or PRs with links back to GitHub.
- **All branches** — commits are fetched across every non-`staging/` branch and deduplicated by SHA, so feature-branch work isn't missed.
- **Merge-noise filter** — "Merge branch 'main'" style commits are excluded from counts.
- **Adjustable lookback** — 7, 14, 30, or 60 days.
- **Zero install** — one HTML file, no build step, no server. Your token is sent only to `api.github.com` and nothing is stored.

## Quick start

1. Open [github-team-arena.html](github-team-arena.html) in any modern browser (double-click works, or serve it locally).
2. Paste a GitHub personal access token with `repo` scope.
3. Enter the repository as `owner/repo` (e.g. `octocat/hello-world`).
4. Pick a lookback window and hit **⚡ Launch Arena**.

### Creating a token

A classic personal access token with the `repo` scope is enough. For fine-grained tokens, grant read access to *Contents*, *Pull requests*, and *Metadata* on the target repository.

## How it works

The page is a self-contained vanilla-JS app (no framework, no bundler). On launch it:

1. Lists every branch in the repo (skipping `staging/*`).
2. Fetches commits from each branch since the lookback date, deduplicating by SHA and tracking which branches each commit appears on.
3. Fetches closed PRs and review comments in parallel.
4. Aggregates by user × day (commits, reviews) and user × week (merged PRs), then renders the dashboard.

All GitHub API calls are paginated client-side (100 per page, up to 10 pages per endpoint).

## Limitations

- API rate limits apply — a 5000/hour authenticated quota is shared across all calls. Large repos with many branches can chew through this quickly.
- Pagination is capped (5 pages of branches/commits-per-branch, 10 pages of PRs/review comments). Very active repos over long lookback windows may be undercounted.
- "Reviews" counts inline review comments (`/pulls/comments`), not top-level PR comments or review approvals.
- Only merged PRs count toward the PR leaderboard. Open and closed-unmerged PRs are ignored.
- PRs targeting a `staging/*` base branch are excluded.

## License

[MIT](LICENSE)
