# pt-br Learnings

Run 3 (2026-03-13): 89.78%->90.33% (35 new strings, 6348 total keys)
Run 4 (2026-03-13): Added noPods key + 7 blank lines to sync structure.

ICU plurals already translated: fleet, limitrange, resourcequota, poddisruptionbudget, servicemonitor, podmonitor, prometheusrule, oidcclient

YAML: js-yaml strips comments. Use extractLeafPaths() for dotted-key types.

PT-BR: Dashboard=Painel, Login=Entrar, Download=Baixar

## UPDATE workflow diff tips
- `diff en-us locale | grep "^[0-9].*[ad]"` = missing/extra keys
- Asymmetric c-hunks = missing blank lines; fix all to get identical line counts
- Avoid simple regex key parsing on YAML with ICU content (false positives)
- Use separate .js files, not inline node -e (arrow fn/template literal issues)
