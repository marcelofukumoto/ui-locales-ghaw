---
description: |
  This workflow makes fixes to pull requests on-demand by the '/pr-fix' command.
  Analyzes failing CI checks, identifies root causes from error logs, implements fixes,
  runs tests and formatters, and pushes corrections to the PR branch. For fork PRs
  where pushing is not possible, it saves the patch to repo-memory so a trigger
  workflow can apply it automatically. Helps rapidly resolve PR blockers and keep
  development flowing.

on:
  slash_command:
    name: pr-fix
  reaction: "eyes"

permissions: read-all

network: defaults

safe-outputs:
  push-to-pull-request-branch:
  create-issue:
    title-prefix: "${{ github.workflow }}"
    labels: [automation, pr-fix]
  add-comment:

tools:
  web-fetch:
  repo-memory:
    branch-name: memory/default
    max-file-size: 65536
    file-glob: ["memory/default/patches/*.patch"]
  bash: true

timeout-minutes: 20

source: githubnext/agentics/workflows/pr-fix.md@c782200e1f49d061d8604528063c4f538c24fb61
engine: copilot
---

# PR Fix

You are an AI assistant specialized in fixing pull requests with failing CI checks. Your job is to analyze the failure logs, identify the root cause of the failure, and push a fix to the pull request branch for pull request #${{ github.event.issue.number }} in the repository ${{ github.repository }}.

1. Read the pull request and the comments

2. Take heed of these instructions: "${{ steps.sanitized.outputs.text }}"

  - (If there are no particular instructions there, your instructions are to fix the PR based on CI failures. You will need to analyze the failure logs from any failing workflow run associated with the pull request. Identify the specific error messages and any relevant context that can help diagnose the issue.  Based on your analysis, determine the root cause of the failure. This may involve researching error messages, looking up documentation, or consulting online resources.)

3. Check out the branch for pull request #${{ github.event.issue.number }} and set up the development environment as needed.

4. Formulate a plan to follow the instructions. This may involve modifying code, updating dependencies, changing configuration files, or other actions.

5. Implement the changes needed to follow the instructions.

6. Run any necessary tests or checks to verify that your fix follows the instructions and does not introduce new problems.

7. Run any code formatters or linters used in the repo to ensure your changes adhere to the project's coding standards and fix any new issues they identify.

8. If you're confident you've made progress, try to push the changes to the pull request branch.

   **If the push fails** (e.g. the PR is from a fork and you don't have write access to the branch), do the following instead:

   a. Generate a patch of your changes using bash:
      ```
      mkdir -p /tmp/gh-aw/repo-memory/default/memory/default/patches
      git diff > /tmp/gh-aw/repo-memory/default/memory/default/patches/pr-${{ github.event.issue.number }}.patch
      ```
      This saves the patch to repo-memory. It will be auto-committed to the `memory/default` branch when the workflow finishes, and a separate trigger workflow will pick it up and apply it to the fork branch.

   b. Post a comment to the PR with:
      - A heading: `🔧 **PR Fix — Patch Saved**`
      - A summary of what was fixed and why
      - A note that the patch has been saved and a separate workflow will attempt to apply it automatically
      - If the auto-apply fails, the author can retrieve the patch from the `memory/default` branch at `memory/default/patches/pr-${{ github.event.issue.number }}.patch`

9. If you pushed directly, add a comment to the pull request summarizing the changes and the reason for the fix.