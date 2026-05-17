# Contributing

Thanks for considering a contribution! A few things to keep in mind:

## Project shape

The project is deliberately **one HTML file** — no build, no bundler, no dependencies. Please don't introduce a package manager, a framework, or split the source into multiple files. PRs that move us toward "just open it in a browser and it works" are welcome.

## Running locally

Just open `github-team-arena.html` in a browser, or serve the directory:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000/github-team-arena.html
```

## Style

- Vanilla JS, no TypeScript.
- Use the existing `el(tag, attrs, ...children)` helper for DOM construction.
- State lives in the top-level `state` object; mutate and call `render()`.
- Match the surrounding code's terseness — this is a small project, not a framework.

## Before opening a PR

- Test against at least one real repo with a token.
- If you change the data-fetching path, test both a cold cache and a warm cache.
- Update the README if behavior or limitations change.

## Reporting bugs

Open an issue with:

- The repo size category (small / medium / large — number of branches and rough commit volume).
- Lookback window and exclude prefixes.
- Browser + version.
- Whether the issue reproduces with a cleared cache (use the link on the setup screen).
- Anything in the browser console.

## Security

Don't paste real GitHub tokens into issues. If you find a security issue with token handling or the cache, please email the maintainer rather than filing a public issue.
