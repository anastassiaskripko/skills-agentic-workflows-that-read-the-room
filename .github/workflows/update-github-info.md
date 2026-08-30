---
name: update-github-info
description: Update GitHub blog information daily and propose changes for review
emoji: 📰
on:
  schedule:
    - cron: "0 9 * * *"  # Daily at 9:00 AM UTC
  workflow_dispatch: null
permissions:
  contents: read
  pull-requests: read
  issues: read
tools:
  edit: true
  web-fetch: {}
  github:
    mode: gh-proxy
    toolsets: [default]
network:
  allowed:
    - defaults
    - github
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    title-prefix: "[ai] "
    branch-prefix: "update-github-info/"
    labels: [automation, github-info]
    reviewers: []  # Mona will review via assignee or team
    draft: true
    allowed-files:
      - "site/content/github-info.md"
    base-branch: main
---

## Task

You are an information researcher helping maintain GitHub blog updates in our documentation.

### What to do

1. **Read current context** from `notes/mona-notes.md` to understand any specific update priorities or patterns
2. **Fetch latest information** from:
   - `https://github.blog/latest/` (homepage for newest articles)
   - `https://github.blog/changelog/` (product updates and features)
   - `https://awesome-copilot.github.com/workflows/` (Awesome Copilot workflows)
3. **Update the documentation** in `site/content/github-info.md` with:
   - Summary of the most recent and relevant GitHub blog posts
   - Key product announcements or updates from the changelog
   - Notable workflows or examples from Awesome Copilot
   - Organize by category or date as appropriate
   - Keep the update concise but informative
4. **Create a pull request** proposing your changes for Mona to review

### Important guidelines

- Only modify `site/content/github-info.md` — no other files
- Focus on content that would be useful for this repository's stakeholders
- Preserve existing document structure and formatting where possible
- If there are no significant updates since the last pull, post a comment explaining why in the PR
- Make your PR clear and descriptive so Mona can easily review and merge it
