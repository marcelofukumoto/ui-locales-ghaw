# Rancher UI Locales

This repository contains a UI Extension that contains additional locales (translations) for the [Rancher Dashboard UI](https://github.com/rancher/dashboard).

The locales in this repository are maintained on a best-effort basis. 

## Agentic Workflows

This repository uses [GitHub Agentic Workflows](https://docs.github.com/en/copilot/using-github-copilot/using-copilot-coding-agent-in-github) to automate common maintenance tasks — adding new languages, fixing translations, syncing with upstream, and keeping documentation up to date. All workflows are AI-powered; results should be reviewed before merging.

---

### Add Language

**Trigger:** Open a GitHub issue with `[ADD]` in the title (e.g. `[ADD] Add Portuguese translation`).

**Description:** Reads the `en-us.yaml` source file, translates all values into the requested language, and opens a Pull Request with the new locale file under `pkg/ui-locales/l10n/`.

**Usage:**
1. Open an issue with `[ADD]` in the title.
2. In the body, specify the language name (e.g. "Portuguese") and/or locale code (e.g. `pt-br`).
3. The workflow will translate the file in chunks and open a PR labelled `translations`, `new-language`, `automated`.

---

### Fix Translation

**Trigger:** Open a GitHub issue with `[FIX]` in the title (e.g. `[FIX] Wrong word in German translation`).

**Description:** Fixes a reported translation error in a specific locale file. Optionally scans for similar issues in the same file and across other language files, opening separate PRs for each fix.

**Usage:**
1. Open an issue with `[FIX]` in the title.
2. In the body, describe the wrong word/phrase, the language, and ideally the correct replacement.
3. Add `--no-similar` in the body to skip scanning for similar cases.
4. The workflow opens one or more PRs labelled `translations`, `fix`, `automated`.

---

### Sync Locales

**Trigger:** Runs on a **daily schedule** or can be triggered manually via `workflow_dispatch`.

**Description:** Fetches the latest `en-us.yaml` from the upstream `rancher/dashboard` repository and compares it with the version in this repo. If changes are found, it updates `en-us.yaml` and adjusts all other existing language files to reflect new or changed keys, then opens a PR labelled `translations`, `automated`.

**Usage:** No manual action needed — runs automatically each day. Can also be triggered manually from the Actions tab.

---

### Verify Translation

**Trigger:** Comment `/verify-translation` on a Pull Request.

**Description:** Performs a **read-only** audit of the locale YAML file in the PR. Checks structural integrity, translation coverage (untranslated strings), placeholder preservation, and key ordering. Reports findings as a PR comment. Does **not** modify any files.

**Usage:**
1. On a PR that adds or modifies a locale file, comment `/verify-translation`.
2. The workflow posts a detailed quality report as a PR comment.
3. If issues are found, run `/improve-translation` to apply fixes.

---

### Improve Translation

**Trigger:** Comment `/improve-translation` on a Pull Request.

**Description:** Finds all untranslated strings (values still identical to `en-us.yaml`) in the locale file, translates them in chunks, and pushes the improved file back to the PR branch. Can be run repeatedly until 100% coverage is reached. Progress is reported as a PR comment.

**Usage:**
1. On a PR that adds or modifies a locale file, comment `/improve-translation`.
2. Optionally include additional instructions in the comment body.
3. The workflow pushes the improved translations directly to the PR branch and posts a progress report.

---

### Update README

**Trigger:** Open a GitHub issue with `[README]` in the title.

**Description:** Reads all workflow `.md` files in `.github/workflows/`, generates documentation describing each workflow, updates `README.md` with the new documentation section, and opens a Pull Request labelled `documentation`, `automated`.

**Usage:**
1. Open an issue with `[README]` in the title.
2. The workflow updates this README and opens a PR for review.

---

### Verify README

**Trigger:** Comment `/verify-readme` on a Pull Request (typically auto-posted after an "Update README" run).

**Description:** Validates that the README accurately and completely documents all agentic workflows. Checks formatting, content quality, and accuracy against the actual workflow files. If confident the documentation is correct, adds a `ready-to-merge` label. If not, posts `/update-readme` with detailed feedback to trigger a revision. Will not run more than 10 verification rounds per PR.

**Usage:**
1. On a PR that modifies `README.md`, comment `/verify-readme`.
2. The workflow either approves the documentation (adds `ready-to-merge`) or requests improvements.

---

### Update README — Revision

**Trigger:** Comment `/update-readme` on a Pull Request (typically posted by the Verify README workflow).

**Description:** Reads feedback from the Verify README workflow, applies the requested improvements to `README.md`, pushes the changes to the PR branch, and comments `/verify-readme` to re-trigger validation. Tracks review history to avoid repeating already-addressed feedback.

**Usage:** This workflow is typically invoked automatically by the Verify README workflow. It can also be triggered manually by commenting `/update-readme` on a README documentation PR.

---

> **Note:** All agentic workflows are AI-powered. Please review generated content carefully before merging.

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
