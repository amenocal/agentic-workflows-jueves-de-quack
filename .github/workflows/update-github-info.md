---
name: update-github-info
description: Refresh site/content/github-info.md from Mona's notes and the latest GitHub Blog and Changelog, then open a pull request for review.
on:
  schedule:
    - cron: "0 13 * * *"
  workflow_dispatch:
permissions:
  contents: read
tools:
  edit:
  web-fetch:
  github:
    mode: gh-proxy
    toolsets: [default]
network:
  allowed:
    - github.blog
    - github.changelog
    - github.com
safe-outputs:
  create-pull-request:
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

## Task

Refresh the GitHub Info page with the latest official GitHub news, following Mona's editorial guidance.

1. Read `notes/mona-notes.md` for Mona's editorial preferences. Use the GitHub repository API tools to read repository files — do not use terminal, CLI, or sandboxed shell commands.
2. Web-fetch the latest posts from:
   - https://github.blog/latest/
   - https://github.blog/changelog/
3. Update `site/content/github-info.md` with short, practical summaries of noteworthy updates. Always cite whether each item came from the GitHub Blog or the GitHub Changelog.
4. Open a pull request with the changes so Mona can review them before they go live.

## Safe Outputs

- Use the `create-pull-request` safe output to propose changes to `site/content/github-info.md`. Do not write directly to `main`.
- Use `noop` with a short explanation if there is no meaningful update to publish.
