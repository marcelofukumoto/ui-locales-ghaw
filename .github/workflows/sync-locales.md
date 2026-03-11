---
description: |
  This workflow checks for changes in the en-us.yaml translation file from
  rancher/dashboard and opens a Pull Request in this repository with the diff
  when updates are found, so translations stay in sync with the upstream source.
  It also updates all other existing language files to reflect any new or changed
  keys introduced in en-us.yaml.

on:
  schedule: daily
  workflow_dispatch:

permissions:
  contents: read
  issues: read
  pull-requests: read
  discussions: read

network: defaults

timeout-minutes: 60

tools:
  github:
    lockdown: false
  bash: true

safe-outputs:
  create-pull-request:
    title-prefix: "chore: "
    labels: [translations, automated]
  add-comment: {}
---

# Sync Locales from rancher/dashboard

Keep the `en-us.yaml` translation file in sync with the upstream `rancher/dashboard` repository, and update all other language files to reflect any changes.

## Scripting constraint

Do **NOT** use Python or pip in any scripts. The runner does not have access to `pypi.org` and package installs will fail. Use **Node.js** or **pure bash** (with tools like `awk`, `sed`, `grep`, `sort`, `diff`) for all scripting needs including YAML parsing and validation.

## Learnings discussion

Before doing anything else, search for a discussion in this repository with the title `[learnings] Add New Language Translation`. This discussion accumulates knowledge from previous runs.

- If it exists, **read it carefully** — it contains chunking strategies, known structural pitfalls, and tips that apply when updating existing translation files.
- If it does not exist, that is fine — proceed without it.

## What to do

1. Fetch the latest `en-us.yaml` from `rancher/dashboard` master branch at:
   `https://raw.githubusercontent.com/rancher/dashboard/master/shell/assets/translations/en-us.yaml`

2. Compare it with the current contents of `pkg/ui-locales/l10n/en-us.yaml` in this repository (**on the default branch**, not a PR branch).

3. If there are **no changes** to `en-us.yaml` compared to the default branch, do nothing and report that translations are already up to date.

4. **Before creating a PR, check for existing open sync PRs**:

   a. Search for open pull requests in this repository with the label `translations` and title containing `sync en-us.yaml`. Use the GitHub tools to list open PRs.

   b. If an open sync PR exists, check out its branch and compare the upstream `en-us.yaml` you just fetched against the `en-us.yaml` **on that PR branch**.

   c. If the upstream `en-us.yaml` is **identical** to the one already on the PR branch, then the existing PR already covers these changes. Add a comment to the existing PR noting that the sync check ran and no new upstream changes were found. Then **stop** — do not create a new PR.

   d. If the upstream `en-us.yaml` has **additional changes** beyond what the existing PR branch has, proceed to step 5 to create a new PR with the latest changes. Mention in the new PR body that it supersedes the existing PR (reference it by number).

5. If there **are changes** to `en-us.yaml` and no existing PR already covers them:

   a. Identify what changed — keys added, removed, or values modified.

   b. Find all other language files in `pkg/ui-locales/l10n/` (any `.yaml` file that is not `en-us.yaml`, e.g. `pt-br.yaml`, `ja-jp.yaml`, `fr-fr.yaml`, etc.).

   c. For each other language file:
      - **New keys** added to `en-us.yaml`: translate the new English values into that language and add them at the **exact same position** in the YAML structure (same nesting level, same order relative to sibling keys)
      - **Removed keys** in `en-us.yaml`: remove the same keys from the language file
      - **Changed values** in `en-us.yaml`: re-translate the updated English value into that language and update it in the language file
      - Preserve all placeholders, ICU message format syntax, HTML tags, and YAML structure exactly — only translate the human-readable text portions
      - **Do NOT invent keys** that do not exist in `en-us.yaml`
      - **Do NOT duplicate keys** — every key must appear exactly once at its nesting level

   d. **Validate each updated language file** using bash: parse the YAML to confirm no duplicate keys, verify exact key parity with the new `en-us.yaml`, and check that all placeholders are preserved. Fix any issues before proceeding.

   e. Open a single Pull Request that includes:
      - The updated `pkg/ui-locales/l10n/en-us.yaml`
      - All updated language files
      - Title: `chore: sync en-us.yaml from rancher/dashboard and update translations`
      - A body that summarizes: what changed in `en-us.yaml`, which language files were updated, and validation results for each file
      - Labels: `translations`, `automated`

## Style

- Be precise and technical 🔍
- Summarize the diff clearly — highlight added keys, removed keys, and changed values
- Note in the PR body that AI-generated translations for other languages should be reviewed by a native speaker before merging
