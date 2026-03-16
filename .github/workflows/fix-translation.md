---
description: |
  This workflow is triggered when a GitHub issue with [FIX] in the title reports
  a translation error — a specific word or phrase that is wrong in a specific
  language file. It fixes the reported translation, then optionally checks for
  similar issues in the same file and across other language files, opening
  separate PRs for each.

on:
  issues:
    types: [opened, reopened]

if: startsWith(github.event.issue.title, '[FIX]')

permissions:
  contents: read
  issues: read
  pull-requests: read

network: defaults

tools:
  github:
    lockdown: false
  repo-memory:
    branch-name: memory/default
    max-file-size: 32768
    file-glob: ["memory/default/*.md"]
  bash: true

safe-outputs:
  create-pull-request:
    title-prefix: "fix: "
    labels: [translations, fix, automated]
  add-comment: {}
---

# Fix Translation Error

When a GitHub issue reports a wrong word or phrase in a translation file, fix it and optionally find and fix similar issues in the same file and other language files — each as a separate Pull Request.

## Shared rules

**Before doing anything else**, read the file `.github/workflows/shared/translation-rules.md` from this repository. It contains the canonical scripting constraints, translation rules, YAML validation procedures, bash size limits, chunking strategy, and learnings instructions that you MUST follow throughout this workflow.

## Trigger condition

Only act if the issue title starts with `[FIX]` and the body reports a translation mistake — a wrong word, incorrect phrase, or bad translation — identifying the language, the wrong text, and ideally the correct replacement.

If the issue does not meet these criteria, do nothing and stop.

## What to do

### Step 1 — Fix the reported translation and similar cases

1. Identify from the issue:
   - The **language** and its locale code (e.g. Portuguese Brazil → `pt-br`)
   - The **wrong word/phrase** as currently in the file
   - The **correct replacement** as requested in the issue

2. Read `pkg/ui-locales/l10n/<locale-code>.yaml` from the repository.

3. Find the exact line(s) containing the wrong text and replace with the correct translation.

4. Scan the **entire file** for similar issues — other occurrences of the same wrong word/phrase, or translations that appear similarly incorrect based on the context of the fix (e.g. same root word, same mistranslation pattern). Fix all of them.

5. **Validate the file** after all fixes: use bash to parse the YAML and confirm no duplicate keys, no structural breakage, and all placeholders are still intact. Fix any issues before proceeding.

6. Open a **single PR**:
   - File changed: `pkg/ui-locales/l10n/<locale-code>.yaml`
   - Title: `fix(<locale-code>): correct "<wrong text>" → "<correct text>"`
   - Body: references the issue, explains the specific fix requested, lists any additional similar fixes found in the same file, closes the issue
   - Label: `translations`, `fix`, `automated`

7. Add a comment to the issue confirming the PR was opened, with a link. If similar cases were also fixed, mention them in the comment.

---

### Important — Only fix the requested language

Do **NOT** check or modify other language files. Only fix the specific language file identified in the issue. Each language has its own ownership and should be fixed through its own dedicated issue.

---

## Style

- Be surgical — only change what needs changing, preserve everything else exactly
- Preserve all YAML structure, keys, placeholders `{var}`, ICU message syntax, and HTML tags
- In PR bodies, be clear and concise about what was changed and why
- Always note when a fix is AI-generated and recommend native speaker review
- If unsure about a translation, flag it explicitly in the PR body rather than guessing silently
