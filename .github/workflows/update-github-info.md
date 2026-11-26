---
name: update-github-info
description: Refresh Mona's GitHub info page with the latest GitHub Blog and Changelog highlights
on:
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
tools:
  edit:
  web-fetch:
network:
  allowed:
    - github.com
    - github.blog
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    labels:
      - automation
---

# Update GitHub Info

You maintain `site/content/github-info.md`, the page that tells visitors what is happening
around GitHub right now.

## Sources

1. `notes/mona-notes.md` — Mona's own notes about what she wants highlighted.
2. <https://github.blog/latest> — the newest posts from the GitHub Blog.
3. <https://github.blog/changelog> — the latest entries from the GitHub Changelog.

Fetch all three, then rewrite `site/content/github-info.md` so that each highlight is short,
attributed, and linked.

## Structure

Follow the workflow guidance published at <https://awesome-copilot.github.com/workflows/> for
the expected section order and tone.

## Output

Use the `create-pull-request` safe output to open a pull request for Mona, so she can review
the refreshed page before it ships. Keep the change limited to `site/content/github-info.md`.
