---
name: Weekly Report Status
description: Generate a concise weekly activity report for commits, issues, and pull requests.
engine: copilot
on:
  schedule:
    - cron: "0 9 * * 1"
  workflow_dispatch:
permissions:
  contents: read
  issues: read
  pull-requests: read
  copilot-requests: write
strict: true
tools:
  github:
    mode: gh-proxy
    toolsets: [default]
safe-outputs:
  create-issue:
    title-prefix: "[weekly-report] "
    max: 1
---

# Weekly Report Status

Create one new issue containing a concise activity report for the previous seven full days ending at workflow start time in UTC. Use GitHub read tools to collect repository activity for that window:

- Commits, including a count and concise references to the most relevant changes.
- Issues opened or closed, including counts and concise references.
- Pull requests opened, merged, or closed, including counts and concise references.

Structure the issue with `### Summary`, `### Commits`, `### Issues`, `### Pull Requests`, and `### Reporting Window` sections. Keep the report brief and group related activity where useful. Clearly state `No activity occurred during this reporting window.` when there were no commits, issues, or pull requests in the window, while still creating the issue. Do not invent activity or metadata that GitHub does not provide. Publish the report using the configured `create-issue` safe output with a descriptive title such as `Weekly activity report - YYYY-MM-DD`.
