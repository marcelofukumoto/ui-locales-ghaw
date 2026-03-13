# pt-br Learnings

Run 3-5 (2026-03-13): coverage improved to 100% after verify run.

ICU translated: fleet, limitrange, resourcequota, poddisruptionbudget, servicemonitor, podmonitor, prometheusrule, oidcclient. PT-BR: Dashboard=Painel, Login=Entrar.

## Tips
- js-yaml: `npm install --prefix /tmp/gh-aw/agent js-yaml`
- ICU arm text is translatable not a placeholder; angle brackets in CLI are not HTML
- cluster.provider.*, csi.drivers.*, model.authConfig.* = kept-in-English (product names)
- Multi-var templates ({subtype} {name}) are skippable; "(experimental)" same in PT
- diff tips: `grep "^[0-9].*[ad]"` for missing/extra keys; separate .js files not inline node -e

## Run (Issue #35, 2026-03-13)
- 1018 strings in ~30 Node.js chunks (50 keys each)
- Sections done: generic, nav, product, suffix, layouts, about, accountAndKeys, asyncButton, catalog, changePassword, authConfig, growl, landing, login, logout, validation, footer, errors, component, user, resourceDetail, resourceList, sortableTable, setup, tableHeaders(partial), workload(partial), promptRemove
- Validation: line count=9514 (matches EN), structure OK, no YAML errors
- Pitfall: Multiline ICU plurals need exact template literal matching
- Use surrounding context to disambiguate duplicate keys (e.g. "age:", "default:", "title:")
