# Rancher UI Locales

This repository contains a UI Extension that contains additional locales (translations) for the [Rancher Dashboard UI](https://github.com/rancher/dashboard).

The locales in this repository are maintained on a best-effort basis. 

## Agentic Workflows

This repository uses [GitHub Agentic Workflows](https://docs.github.com/en/copilot/github-copilot-in-github/using-github-copilot-in-github-issues) to automate translation management tasks. These workflows are AI-powered — always review the generated results before merging.

---

### Add Language

**Trigger:** Open a GitHub issue with `[ADD]` at the start of the title.

**Description:** Translates the entire `en-us.yaml` file into the requested language and opens a Pull Request with the new locale file.

**Usage:** Create an issue with a title like `[ADD] Add Portuguese (Brazil) translation`. Include the language name and/or BCP 47 locale code (e.g. `pt-br`) in the body. The workflow will translate all strings, validate the output, and open a PR tagged with `translations`, `new-language`, and `automated`.

**Key behaviors:**
- Checks whether the locale file already exists before translating
- Validates key parity, YAML structure, and placeholder preservation
- Adds a comment to the issue linking to the opened PR

---

### Fix Translation

**Trigger:** Open a GitHub issue with `[FIX]` at the start of the title.

**Description:** Fixes a reported translation error in a specific language file. By default, it also scans for similar issues in the same file and checks other language files for the same pattern.

**Usage:** Create an issue with a title like `[FIX] Wrong word in Portuguese translation`. Describe the wrong text, the correct replacement, and the affected language. Optional flags in the body: `--no-similar` (skip similar-case scan), `--no-other-languages` (skip other language files), `--simple` (only fix the specific reported error).

**Key behaviors:**
- Opens a separate PR for each fix scope (reported fix, similar cases, other languages)
- Validates YAML structure after each fix
- Labels PRs with `translations`, `fix`, and `automated`

---

### Improve Translation

**Trigger:** Comment `/improve-translation` on a translation Pull Request.

**Description:** Finds all untranslated strings in the PR's locale file (values still identical to `en-us.yaml`) and translates them in chunks, pushing the improved file back to the PR branch.

**Usage:** Comment `/improve-translation` on a PR that adds or modifies a locale file. Run it multiple times until 100% coverage is reached. Additional instructions can be appended to the slash command.

**Key behaviors:**
- Reports coverage before and after (total keys, translated, untranslated, skipped)
- Works section by section through the YAML file
- Validates YAML structure and placeholder preservation after each chunk
- Does not modify files that do not need translation

---

### Sync Locales

**Trigger:** Runs automatically on a **daily schedule**, or can be triggered manually via `workflow_dispatch`.

**Description:** Checks for changes to `en-us.yaml` in the upstream `rancher/dashboard` repository. When updates are found, it updates all existing language files to reflect new or changed keys and opens a Pull Request.

**Usage:** No manual action required — the workflow runs daily. It can also be triggered manually from the Actions tab.

**Key behaviors:**
- Skips if no upstream changes are detected
- Detects and avoids duplicate sync PRs
- Updates all existing language files (adds new keys, removes deleted keys, re-translates changed values)
- Labels the PR with `translations` and `automated`

---

### Update README

**Trigger:** Open a GitHub issue with `[README]` in the title.

**Description:** Reads all workflow `.md` files, generates documentation for each workflow, and opens a Pull Request updating `README.md` with an `## Agentic Workflows` section.

**Usage:** Create an issue with `[README]` in the title to request a README update. The workflow documents all workflows found in `.github/workflows/`.

**Key behaviors:**
- Preserves all existing README content outside the workflows section
- Inserts the workflow section before the License section (or replaces an existing one)
- Opens a PR with labels `documentation` and `automated`

---

### Update README (Revision)

**Trigger:** Comment `/update-readme` on a README documentation Pull Request (typically triggered automatically by the Verify README workflow).

**Description:** Reads feedback from the Verify README workflow, applies all requested improvements to the README on the PR branch, and re-triggers validation by commenting `/verify-readme`.

**Usage:** Comment `/update-readme` on a README PR to address verification feedback. Additional instructions can be appended to the slash command.

**Key behaviors:**
- Addresses every issue listed in the most recent verify-readme feedback comment
- Pushes changes directly to the PR branch
- Always ends by commenting `/verify-readme` to trigger re-validation

---

### Verify README

**Trigger:** Comment `/verify-readme` on a README documentation Pull Request.

**Description:** Validates that the README accurately and completely documents all agentic workflows. Checks completeness, accuracy, formatting quality, and usability. Adds `ready-to-merge` if all checks pass; otherwise requests improvements via `/update-readme`.

**Usage:** Comment `/verify-readme` on a PR that modifies `README.md`. Capped at 10 verification rounds per PR.

**Key behaviors:**
- Verifies every workflow in `.github/workflows/` is documented
- Checks trigger accuracy, description correctness, and Markdown formatting
- Adds the `ready-to-merge` label when all checks pass
- Posts structured feedback with specific improvement requests when checks fail

---

### Verify Translation

**Trigger:** Comment `/verify-translation` on a translation Pull Request.

**Description:** Read-only audit of a locale YAML file. Checks structural integrity (valid YAML, key parity, key ordering, placeholder preservation) and calculates translation coverage. Does **not** modify any files — findings are reported as a PR comment.

**Usage:** Comment `/verify-translation` on a PR that adds or modifies a locale file. If issues are found, run `/improve-translation` to apply fixes.

**Key behaviors:**
- Checks YAML validity, key parity with `en-us.yaml`, key ordering, and placeholder preservation
- Calculates coverage broken down by top-level YAML section
- Adds `ready-to-merge` label and submits an approving review when all checks pass and coverage is 100%
- Never modifies files — strictly read-only

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
