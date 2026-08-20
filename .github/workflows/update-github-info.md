---
name: update-github-info
on:
  schedule: daily
  workflow_dispatch:

permissions:
  contents: read

engine: copilot

tools:
  github:
    toolsets: [repos]
  web-fetch:
  edit:

network:
  allowed:
    - github.blog
    - github.com

safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    draft: true
    max: 1
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Refresh Mona's GitHub Info content with the latest practical updates from official GitHub sources.

1. Use GitHub repository API tools to read `notes/mona-notes.md` and `site/content/github-info.md`. Do not use terminal, CLI, or sandboxed commands for repository guidance or reference files.
2. Use `web-fetch` to read `https://github.blog/latest/` and `https://github.blog/changelog/`.
3. Select a small set of recent, developer-relevant updates. Keep summaries short and practical, and include the official source URL and publication date for every selected item.
4. Update only `site/content/github-info.md`, preserving its existing Markdown structure and Mona's editorial angle.
5. Use the `create_pull_request` safe-output tool to open one draft pull request for Mona to review. State the sources reviewed and summarize the content changes in the pull request body.

If the sources do not provide any worthwhile new information, do not edit the file and use the appropriate no-op safe output instead.---
name: update-github-info
description: Keep Mona's GitHub Info content current from official GitHub sources.
on:
  schedule: daily
  workflow_dispatch:

permissions:
  contents: read
  pull-requests: read

engine: copilot
strict: true

tools:
  edit:
  web-fetch:
  github:
    mode: remote
    toolsets: [repos, pull_requests]

network:
  allowed:
    - github.blog
    - github.com

safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: true
    max: 1
    if-no-changes: warn
---

# Update GitHub Info

Refresh `site/content/github-info.md` with concise, practical updates for Mona's website.

## Research first

1. Read `notes/mona-notes.md` with the GitHub repository API tools and follow its editorial guidance.
2. Read the current `site/content/github-info.md` with the GitHub repository API tools so existing themes and entries are preserved where still useful.
3. Use `web-fetch` to read https://github.blog/latest/.
4. Use `web-fetch` to read https://github.blog/changelog/.
5. Use `web-fetch` to read the public GitHub Agentic Workflows guidance at https://github.com/github/gh-aw/blob/main/.github/aw/github-agentic-workflows.md.
6. Use the GitHub repository API tools to read any other repository guidance or reference files needed to make the update consistent with the site.

## Update

Use the `edit` tool to update only `site/content/github-info.md`. Add or revise short summaries that help developers learn GitHub faster, and include the source URL or source name whenever an item comes from the GitHub Blog or GitHub Changelog. Keep the Markdown structure compatible with the Astro page that imports this file.

Do not modify any other file. Do not use terminal, CLI, bash, or sandboxed commands to read repository guidance or reference files. Do not publish changes directly to the default branch.

## Review

After editing, use the `create-pull-request` safe output to open a pull request containing the `site/content/github-info.md` change for Mona to review. Give the pull request a clear title and summarize the sources and updates in its body. If there are no worthwhile changes, do not open a pull request.