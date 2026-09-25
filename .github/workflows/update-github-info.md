---
name: update-github-info
description: Keep the GitHub Info page current with practical updates from the GitHub Blog and Changelog.
on:
  schedule:
    - cron: "17 9 * * *"
  workflow_dispatch:
permissions:
  contents: read
tools:
  edit:
  web-fetch:
  github:
    mode: local
    toolsets:
      - repos
network:
  allowed:
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: true
    fallback-as-issue: false
    max: 1
---

# Update GitHub Info

Maintain the GitHub Info website content for Mona.

1. Use the GitHub repository API tools to read `notes/mona-notes.md` and the current `site/content/github-info.md`. Use those API tools for repository guidance and reference files; do not use terminal commands, the GitHub CLI, or sandboxed commands to read them.
2. Use `web-fetch` to read the latest public guidance at `https://raw.githubusercontent.com/github/gh-aw/main/.github/aw/github-agentic-workflows.md`.
3. Use `web-fetch` to read `https://github.blog/latest/` and `https://github.blog/changelog/`.
4. Select only useful, current items that help developers learn GitHub faster. Keep summaries short and practical, and identify whether each item came from the GitHub Blog or GitHub Changelog.
5. Use the `edit` tool to update only `site/content/github-info.md`. Preserve its existing format and avoid unrelated changes. If there are no worthwhile updates, make no edit and do not open a pull request.
6. When changes are worthwhile, use the `create_pull_request` safe output to propose them for Mona to review. Use a concise title, explain the sources and updates in the body, target the repository's default branch, and do not write directly to the default branch.
