# Rancher UI Locales

This repository contains a UI Extension that contains additional locales (translations) for the [Rancher Dashboard UI](https://github.com/rancher/dashboard).

The locales in this repository are maintained on a best-effort basis. 

## Agentic Workflows

This repository uses [GitHub Agentic Workflows](https://github.com/features/copilot) to automate translation management and documentation tasks. These workflows are AI-powered — results should always be reviewed by a human (and by a native speaker for translation work) before merging.

---

### Add Language

**Trigger:** Open an issue with `[ADD]` at the start of the title (e.g. `[ADD] Add Portuguese Brazil translation`).

**Description:** Translates the entire `en-us.yaml` source file into the requested language. The workflow identifies the correct BCP 47 locale code, checks whether the locale file already exists, performs a full translation in chunks, validates the output (key parity, placeholder preservation, valid YAML), and opens a Pull Request with the new locale file.

**Key behaviors:**
- Labels the PR with `translations`, `new-language`, `automated`
- Comments on the issue with a link to the PR
- Notes in the PR that the translation is AI-generated and needs native speaker review

---

### Fix Translation

**Trigger:** Open an issue with `[FIX]` at the start of the title (e.g. `[FIX] Wrong word in pt-br for "Delete"`).

**Description:** Fixes a reported translation error in a specific locale file. By default it also scans the same file for similar issues and checks other language files for the same problem, opening a separate PR for each case.

**Key behaviors:**
- Opens up to one PR per affected locale file
- Supports `--no-similar`, `--no-other-languages`, and `--simple` flags in the issue body to limit scope
- Labels PRs with `translations`, `fix`, `automated`

---

### Sync Locales

**Trigger:** Runs automatically on a **daily schedule**, or can be triggered manually via `workflow_dispatch`.

**Description:** Fetches the latest `en-us.yaml` from the upstream `rancher/dashboard` repository and compares it with the copy in this repo. If changes are found, it updates `en-us.yaml` and re-translates all other language files to match, then opens a single PR with all changes.

**Key behaviors:**
- Skips if a sync PR already covers the latest upstream changes
- Validates each updated language file before opening the PR
- Labels the PR with `translations`, `automated`

---

### Improve Translation

**Trigger:** Comment `/improve-translation` on a translation PR.

**Description:** Finds all untranslated strings in the locale file on the PR (values still identical to `en-us.yaml`), translates them in chunks by top-level YAML section, pushes the improved file back to the PR branch, and posts a detailed progress report. Can be run repeatedly until 100% coverage is reached.

**Key behaviors:**
- Works in priority order: UI text first, long-form text next, technical strings last
- Reports coverage before and after each run, broken down by YAML section
- Pushes changes directly to the PR branch

---

### Verify Translation

**Trigger:** Comment `/verify-translation` on a translation PR.

**Description:** Read-only audit of a locale file. Checks structural integrity (valid YAML, exact key parity with `en-us.yaml`, key ordering, type parity, placeholder preservation) and calculates translation coverage. Posts a detailed report as a PR comment. Adds the `ready-to-merge` label and submits an approving review when all checks pass and coverage is 100%.

**Key behaviors:**
- Never modifies files — report only
- Recommends running `/improve-translation` if issues are found
- Adds `ready-to-merge` label on 100% pass

---

### Update README

**Trigger:** Open an issue with `[README]` in the title (e.g. `[README] Update workflow documentation`).

**Description:** Reads all workflow `.md` files in `.github/workflows/`, generates structured documentation for each workflow, inserts (or replaces) the `## Agentic Workflows` section in `README.md`, and opens a Pull Request. After creating the PR, comments `/verify-readme` to trigger automated validation.

**Key behaviors:**
- Preserves all existing README content outside the workflows section
- Labels the PR with `documentation`, `automated`
- Triggers the Verify README workflow automatically after PR creation

---

### Verify README

**Trigger:** Comment `/verify-readme` on a README PR.

**Description:** Validates that the README accurately and completely documents all workflows. Checks completeness (all workflow files documented), accuracy (descriptions match source files), formatting, and usability. If all checks pass, adds the `ready-to-merge` label. If not, posts specific feedback and comments `/update-readme` to trigger a revision.

**Key behaviors:**
- Stops after 10 verification rounds on any single PR
- Adds `ready-to-merge` label on a full pass
- Never modifies files — report and label only

---

### Update README — Revision

**Trigger:** Comment `/update-readme` on a README PR (typically triggered automatically by the Verify README workflow).

**Description:** Reads the feedback from the most recent Verify README comment, applies all requested improvements to `README.md`, pushes the changes to the PR branch, and comments `/verify-readme` to re-trigger validation.

**Key behaviors:**
- Addresses every item in the "Required Improvements" list from the verify feedback
- Hides its own older comments to keep the PR thread clean
- Re-triggers verification automatically after each revision

---

License
=======
Copyright (c) 2014-2025 [SUSE](https://www.suse.com)

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
