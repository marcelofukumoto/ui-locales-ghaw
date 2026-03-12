# Rancher UI Locales

This repository contains a UI Extension that contains additional locales (translations) for the [Rancher Dashboard UI](https://github.com/rancher/dashboard).

The locales in this repository are maintained on a best-effort basis. 

## Agentic Workflows

This repository uses [GitHub Agentic Workflows](https://github.com/features/copilot) to automate common translation and documentation tasks. These workflows are AI-powered — always review AI-generated changes before merging.

---

### Add Language

**Trigger:** Create a GitHub issue with `[ADD]` in the title and specify the language name (e.g. "Portuguese") and/or locale code (e.g. `pt-br`).

**Description:** Translates the entire `en-us.yaml` file into the requested language. Checks whether the locale file already exists, translates all string values in chunks while preserving placeholders and YAML structure, self-validates the output, and opens a Pull Request with the new locale file.

**Labels added:** `translations`, `new-language`, `automated`

---

### Fix Translation

**Trigger:** Create a GitHub issue with `[FIX]` in the title and describe the wrong word or phrase, the affected language, and the correct replacement.

**Description:** Fixes a reported translation error in a locale file. By default, also checks for similar issues in the same file (opening a second PR) and checks the same keys in all other language files (opening separate PRs per language). Supports `--no-similar`, `--no-other-languages`, and `--simple` flags in the issue body to limit scope.

**Labels added:** `translations`, `fix`, `automated`

---

### Sync Locales

**Trigger:** Runs automatically on a daily schedule, or can be triggered manually via `workflow_dispatch`.

**Description:** Fetches the latest `en-us.yaml` from the upstream [`rancher/dashboard`](https://github.com/rancher/dashboard) repository and compares it with the current version in this repo. If changes are found, updates all other language files to reflect new, removed, or changed keys, then opens a single Pull Request with all updates.

**Labels added:** `translations`, `automated`

---

### Improve Translation

**Trigger:** Comment `/improve-translation` on an open Pull Request that adds or modifies a locale file.

**Description:** Finds all untranslated strings in the locale file (values still identical to `en-us.yaml`), translates them in chunks by top-level YAML section, pushes the improved file back to the PR branch, and posts a detailed coverage report. Can be run repeatedly until 100% coverage is reached.

---

### Verify Translation

**Trigger:** Comment `/verify-translation` on an open Pull Request that adds or modifies a locale file.

**Description:** Read-only validation of a translated locale file. Checks YAML validity, exact key parity with `en-us.yaml`, key ordering, structure parity, placeholder preservation, and translation coverage. Posts a detailed report as a PR comment. If all checks pass and coverage is 100%, adds the `ready-to-merge` label and submits an approving review. Does **not** modify any files — if issues are found, it recommends running `/improve-translation`.

---

### Update README

**Trigger:** Create a GitHub issue with `[README]` in the title.

**Description:** Reads all workflow `.md` files in `.github/workflows/`, generates structured documentation for each workflow, and updates `README.md` with an `## Agentic Workflows` section. Opens a Pull Request with the updated documentation and comments `/verify-readme` on the PR to trigger automated validation.

**Labels added:** `documentation`, `automated`

---

### Update README — Revision

**Trigger:** Comment `/update-readme` on an open Pull Request (typically triggered automatically by the Verify README workflow when improvements are needed).

**Description:** Reads feedback from the most recent Verify README comment, applies all requested improvements to `README.md`, pushes the updated file to the PR branch, and comments `/verify-readme` to trigger re-validation.

---

### Verify README

**Trigger:** Comment `/verify-readme` on an open Pull Request that modifies `README.md`.

**Description:** Validates that the README accurately and completely documents all agentic workflows. Checks completeness (all workflows documented), accuracy (descriptions match source files), formatting quality, and usability. If all checks pass, adds the `ready-to-merge` label. If improvements are needed, posts detailed feedback and comments `/update-readme` to trigger a revision. Enforces a maximum of 10 verification rounds per PR.

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
