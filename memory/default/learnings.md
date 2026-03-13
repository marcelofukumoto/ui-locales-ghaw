# pt-br Learnings

Run 3-5 (2026-03-13): coverage improved to 100% after verify run.

ICU translated: fleet, limitrange, resourcequota, poddisruptionbudget, servicemonitor, podmonitor, prometheusrule, oidcclient. PT-BR: Dashboard=Painel, Login=Entrar.

## Tips
- js-yaml: `npm install --prefix /tmp/gh-aw/agent js-yaml`
- ICU arm text is translatable not a placeholder; angle brackets in CLI are not HTML
- cluster.provider.*, csi.drivers.*, model.authConfig.* = kept-in-English (product names)
- Multi-var templates ({subtype} {name}) are skippable; "(experimental)" same in PT
- diff tips: `grep "^[0-9].*[ad]"` for missing/extra keys; separate .js files not inline node -e
