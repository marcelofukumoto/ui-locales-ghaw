# Rancher UI Locales

This repository contains a UI Extension that contains additional locales (translations) for the [Rancher Dashboard UI](https://github.com/rancher/dashboard).

The locales in this repository are maintained on a best-effort basis. 

## Agentic Workflows

This repository uses [GitHub Agentic Workflows](https://github.com/features/copilot) to automate common contribution tasks. These workflows are AI-powered — always review the results before merging.

---

### Add Language

**Trigger:** Open a GitHub issue with `[ADD]` in the title, describing the language you want added (e.g. "Portuguese", "Japanese") and/or its BCP 47 locale code (e.g. `pt-br`, `ja-jp`).

**What it does:** Reads the full `en-us.yaml` source file, translates all string values into the requested language, validates the output, and opens a Pull Request creating the new locale file at `pkg/ui-locales/l10n/<locale-code>.yaml`.

**Labels added:** `translations`, `new-language`, `automated`

---

### Fix Translation

**Trigger:** Open a GitHub issue with `[FIX]` in the title, describing the wrong word or phrase, the language it appears in, and the correct replacement.

**What it does:** Locates and fixes the specific translation error in the locale YAML file. By default it also checks for similar mistakes in the same file (opening a second PR) and reviews the same keys across all other language files (opening additional PRs as needed). Use `--no-similar`, `--no-other-languages`, or `--simple` flags in the issue body to skip those steps.

**Labels added:** `translations`, `fix`, `automated`

---

### Sync Locales

**Trigger:** Runs automatically on a **daily schedule**. Can also be triggered manually via `workflow_dispatch`.

**What it does:** Fetches the latest `en-us.yaml` from the upstream `rancher/dashboard` repository and compares it with the copy in this repo. If changes are found, it updates `en-us.yaml` and propagates additions, removals, and value changes to all other language files, then opens a single Pull Request with all updates.

**Labels added:** `translations`, `automated`

---

### Improve Translation

**Trigger:** Comment `/improve-translation` on a translation Pull Request.

**What it does:** Identifies all untranslated strings in the locale file (values still identical to `en-us.yaml`) and translates them in chunks by YAML section. Pushes the improved file back to the PR branch and reports coverage progress. Can be run repeatedly until 100% coverage is reached.

**Usage tip:** Run `/improve-translation` as many times as needed; each run picks up where the last one left off.

---

### Verify Translation

**Trigger:** Comment `/verify-translation` on a translation Pull Request.

**What it does:** Performs a **read-only** audit of the locale file — checks structural integrity (valid YAML, exact key parity, key ordering, type parity), placeholder preservation, and translation coverage. Produces a detailed report. If all checks pass and coverage is 100%, adds the `ready-to-merge` label and approves the PR. Does **not** modify any files; if issues are found, it recommends running `/improve-translation`.

---

### Update README

**Trigger:** Open a GitHub issue with `[README]` in the title requesting documentation updates.

**What it does:** Reads all workflow files in `.github/workflows/`, generates comprehensive documentation for each one, updates `README.md` with an `## Agentic Workflows` section, and opens a Pull Request. After creating the PR, it comments `/verify-readme` on the issue to trigger automated validation.

**Labels added:** `documentation`, `automated`

---

### Verify README

**Trigger:** Comment `/verify-readme` on a Pull Request or issue.

**What it does:** Validates the README documentation against the actual workflow source files — checks that every workflow is documented, descriptions are accurate, formatting is consistent, and usage instructions are clear. If all checks pass, adds the `ready-to-merge` label. If improvements are needed, posts detailed feedback and triggers `/update-readme`. Runs up to 10 verification rounds per PR.

---

### Update README — Revision

**Trigger:** Comment `/update-readme` on a Pull Request (typically triggered automatically by the Verify README workflow).

**What it does:** Reads the feedback from the most recent Verify README comment, addresses every listed improvement, updates the README on the PR branch, and comments `/verify-readme` to re-trigger validation. Keeps iterating until the README passes all checks.

---

> **Note:** All AI-generated content (translations, documentation) should be reviewed by a human before merging. Translations should ideally be reviewed by a native speaker of the target language.

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
