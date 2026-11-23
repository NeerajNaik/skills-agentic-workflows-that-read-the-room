---
name: update-github-info
description: Propose concise, source-backed updates to Mona's GitHub Info page.
intent: Keep Mona's GitHub Info page current with practical updates from official GitHub sources.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
checkout:
  fetch-depth: 1
tools:
  edit: 
  web-fetch: 
network:
  allowed:
    - github.blog
    - github.com
engine:
  id: copilot
  copilot-sdk: true
safe-outputs:
  create-pull-request:
    allowed-files:
      - site/content/github-info.md
    draft: false
---

# Update GitHub Info

Read `notes/mona-notes.md` and the current `site/content/github-info.md` before editing. Treat Mona's notes as the editorial requirements and preserve existing useful content.

Use web fetch to read both:

- https://github.blog/latest/
- https://github.blog/changelog/

Select up to three recent, useful, non-duplicate updates that help developers learn GitHub faster or fit the page's current themes. Only state facts supported by those pages. Keep each entry short and practical, and include its publication date and a direct link to its GitHub Blog or Changelog source.

Update only `site/content/github-info.md`, keeping its current structure and editorial angle. If there are no relevant new updates, the source pages cannot be read, or the evidence is insufficient, make no changes and call `noop` with a brief reason.

When the page has meaningful changes, use the configured `create-pull-request` safe output to open one reviewable pull request for Mona. Summarize the updates and include their source links in the PR description. Do not write directly to the default branch or change any other files.
