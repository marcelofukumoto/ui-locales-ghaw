---
description: |
  This workflow is triggered when a GitHub issue with [ADD] in the title requests
  a new language translation. It reads the en-us.yaml file, translates all values
  into the requested language, and opens a Pull Request with the new locale file.

on:
  issues:
    types: [opened, reopened]

if: startsWith(github.event.issue.title, '[ADD]')

permissions:
  contents: read
  issues: read
  pull-requests: read

network: defaults

timeout-minutes: 120

tools:
  github:
    lockdown: false
  repo-memory:
    branch-name: memory/default
    max-file-size: 32768
    file-glob: ["memory/default/*.md"]
  bash: true

safe-outputs:
  max-patch-size: 32
  create-pull-request:
    title-prefix: "feat: "
    labels: [translations, new-language, automated]
  add-comment: {}
---

# Add New Language Translation

When a GitHub issue requests a new language to be added to the UI locales extension, translate the entire `en-us.yaml` file into the requested language and open a Pull Request.

## Scripting constraint

Do **NOT** use Python or pip in any scripts. The runner does not have access to `pypi.org` and package installs will fail. Use **Node.js** or **pure bash** (with tools like `awk`, `sed`, `grep`, `sort`, `diff`) for all scripting needs including YAML parsing and validation.

## Learnings (repo-memory)

Before doing anything else, read the file `/tmp/gh-aw/repo-memory-default/memory/default/learnings.md` if it exists. This file accumulates knowledge from all previous translation runs — chunking strategies, known pitfalls, character/token limits, and tips. Apply this knowledge throughout your work.

If the file does not exist yet, that is fine — you will create it at the end.

## Trigger condition

Only act if the issue title starts with `[ADD]` and the body clearly requests a new language translation mentioning a specific language name (e.g. "Portuguese", "Japanese", "French") and/or a locale code (e.g. `pt-br`, `ja-jp`, `fr-fr`).

If the issue does not meet these criteria, do nothing and stop.

## What to do

1. **Identify the language** requested in the issue — extract both the language name and the correct BCP 47 locale code (e.g. Portuguese Brazil → `pt-br`, Japanese → `ja-jp`, Simplified Chinese → `zh-hans`, French → `fr-fr`).

2. **Check if the locale file already exists** by looking for `pkg/ui-locales/l10n/<locale-code>.yaml` in the repository. If it already exists, add a comment to the issue saying the language is already supported and stop.

3. **Read the full contents** of `pkg/ui-locales/l10n/en-us.yaml` from this repository.

4. **Translate all string values** in chunks to stay within output limits. Rules:
   - **Mirror the source exactly**: the output file must have the exact same keys, in the exact same order, at the exact same nesting depth as `en-us.yaml` — only leaf values change
   - **Do NOT invent keys**: never add keys that do not exist in `en-us.yaml`
   - **Do NOT skip keys**: every key in `en-us.yaml` must appear in the output
   - **Do NOT duplicate keys**: every key must appear exactly once at its nesting level — YAML forbids duplicate keys and parsers will reject the file
   - Preserve all placeholders as-is: `{variableName}`, `{count, plural, ...}`, `&hellip;`, HTML tags like `<b>`, `<a href=...>`, `<code>`, etc.
   - Preserve all ICU message format syntax (plurals, selects) — only translate the human-readable text portions inside them
   - Do not translate YAML comments (lines starting with `#`) — preserve them in the same positions
   - Empty values must remain empty; special values like `'—'` must be preserved exactly
   - If a key's value is a mapping (has children) in `en-us.yaml`, it must also be a mapping in the output — never flatten a nested structure into a scalar
   - Use chunking sizes and strategies noted in the learnings file (if available), otherwise split at top-level YAML keys to keep each chunk manageable

5. **Self-validate before opening the PR**. Use bash to write and run a validation script that checks:
   - The output file is valid YAML (no parse errors, no duplicate keys)
   - Every key in `en-us.yaml` exists in the output and vice-versa (exact key parity)
   - Key order matches `en-us.yaml`
   - All placeholders (`{...}`, `&hellip;`, HTML tags) from `en-us.yaml` are present in the corresponding translated values
   - If any issues are found, fix them and re-validate until the file is clean

   **Fixing YAML parse errors**: If the generated file has YAML parse errors, identify the broken key from the parser error (line number), look up that key in `en-us.yaml` to get the original value and formatting, re-translate it preserving the exact same YAML quoting and formatting style (single quotes, block scalars `|`/`>`, etc.), replace the broken line, and re-validate. Common causes: unescaped colons/hashes in translations, broken quoting, mangled ICU `{count, plural, ...}` syntax. Always mirror `en-us.yaml`'s formatting.

6. **Open a Pull Request** that:
   - Creates the new file at `pkg/ui-locales/l10n/<locale-code>.yaml` with the translated content
   - Has the title: `feat: add <Language Name> (<locale-code>) translation`
   - Has a body that mentions the issue number, the language added, and a note that the translation was AI-generated and should be reviewed by a native speaker
   - Includes the validation results (total keys, any issues found and fixed)
   - References and closes the original issue

7. **Add a comment** to the original issue letting the requester know a PR has been opened with the translation, linking to it, noting it needs native speaker review before merging, and that `/verify-translation` can be run on the PR for additional structural checks.

## Update learnings

After completing the work (or after hitting any significant obstacle), write your learnings to `/tmp/gh-aw/repo-memory-default/memory/default/learnings.md`. This is the most important step for improving future runs.

If the file already exists, **merge** your new observations into the existing content — do not discard previous learnings. If it does not exist, create it.

The file should be written in Markdown and cover:

- **Chunking strategy**: how you split `en-us.yaml` (e.g. by top-level key, how many keys per chunk, approximate line count per chunk) and what worked well
- **Output size limits**: any limits you hit (token/character limits per PR file, per commit) and how you worked around them
- **Performance tips**: what made the run faster (e.g. reading only the keys you needed, avoiding re-reads)
- **Known pitfalls**: keys or sections that are tricky (ICU plurals, nested HTML, very long values) and how to handle them
- **Anything that caused errors or timeouts** and how to avoid them next time

Keep the file concise and actionable — it is read at the start of every future run. The file auto-commits to the `memory/default` branch when the workflow finishes.

## Style

- Be thorough — translate every string value, no skipping
- Be accurate with locale codes — use the correct BCP 47 standard code for the language
- Flag in the PR description if any strings were uncertain or left in English due to technical constraints
