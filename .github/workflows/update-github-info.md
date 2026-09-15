---
name: update-github-info
description: Keep the GitHub Info website current with practical updates from official GitHub sources.
on:
  schedule:
    - cron: "0 9 * * *"
  workflow_dispatch:
permissions:
  contents: read
strict: true
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
tools:
  github:
    mode: gh-proxy
    toolsets: [default]
  edit:
  web-fetch:
safe-outputs:
  create-pull-request:
    allowed-files:
      - site/content/github-info.md
    reviewers:
      - mona
    draft: true
    max: 1
---

# Update GitHub Info

Read `notes/mona-notes.md` before making any change.

Use the GitHub repository API tools to inspect relevant repository guidance and reference files. Do not use terminal, CLI, or sandboxed commands for repository guidance or reference-file reads.

Use web-fetch to read:

- https://github.blog/latest/
- https://github.blog/changelog/
- https://awesome-copilot.github.com/workflows/

Also add Awesome Copilot workflows to the sources:

- https://awesome-copilot.github.com/workflows/

Identify useful, recent GitHub updates that fit Mona's practical editorial angle. Update only `site/content/github-info.md` with concise summaries, and cite the GitHub Blog, GitHub Changelog, or Awesome Copilot workflows source for each update. Preserve the existing structure and avoid speculative or duplicate content.

When there is a supported update, use the configured `create-pull-request` safe output to open a draft pull request for Mona to review. Include a concise title and body that summarize the sources and changes. Never write directly to `main`.

If the sources contain no suitable new information, make no file changes and call `noop` with a short reason.