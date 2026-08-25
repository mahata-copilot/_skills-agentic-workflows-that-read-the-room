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
    toolsets:
      - repos
  web-fetch:
  edit:
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    max: 1
    base-branch: main
---

# Update GitHub Info

Refresh the GitHub Info content for Mona's website and propose the changes in a pull request for Mona to review.

## Sources and repository context

1. Read `notes/mona-notes.md` using the repository file or GitHub repository API tools.
2. Read the current `site/content/github-info.md` using the repository file or GitHub repository API tools.
3. Web fetch https://github.blog/latest/.
4. Web fetch https://github.blog/changelog/.
5. Web fetch https://awesome-copilot.github.com/workflows/.

Use only the official GitHub Blog, Changelog, and Awesome Copilot workflows pages as sources for new updates. Keep summaries short and practical, focus on helping developers learn GitHub faster, and mention the source for every update.

Update `site/content/github-info.md` with useful, accurate content that fits its existing editorial angle. Preserve the existing structure unless a small structural change is needed for clarity. Do not modify unrelated files.

After editing the content, use the `create-pull-request` safe output to open one pull request against `main` with a concise title and summary for Mona to review. Do not write directly to `main`.