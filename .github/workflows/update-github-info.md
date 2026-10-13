---
name: update-github-info
description: Refresh the GitHub Info page with useful updates from the GitHub Blog, Changelog, and Awesome Copilot workflows.
intent: Propose concise, source-linked updates to the GitHub Info page for Mona to review.
model: gpt-4.1
on:
  schedule:
    - cron: "0 9 * * *"
  workflow_dispatch:
permissions:
  contents: read
tools:
  edit: true
  web-fetch: {}
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    draft: false
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

## Task

1. Read `notes/mona-notes.md` and `site/content/github-info.md`.
2. Fetch `https://github.blog/latest/`, `https://github.blog/changelog/`, and `https://awesome-copilot.github.com/workflows/`.
3. Identify recent, useful developments that help developers learn GitHub faster. Keep summaries short and practical, and cite the relevant GitHub Blog, Changelog, or Awesome Copilot workflows source link whenever using it.
4. Update only `site/content/github-info.md`, preserving its existing purpose and editorial angle. Do not add unsupported claims or repeat information that is already covered unless a source provides a meaningful update.
5. Use the configured `create-pull-request` safe output to open one pull request for Mona to review. Do not merge it or write directly to the default branch. If none of the sources contains a meaningful, verifiable update, make no file changes and use `noop` with a brief reason.
