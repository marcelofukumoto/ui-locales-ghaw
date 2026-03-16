# PT-BR Learnings

Coverage: 100% after agent review. ~503 kept in English (brand/tech terms), ~55 skipped.

YAML: quote values with `:` — `'Total:'`. HTML in double-quoted = use plain scalar. "Aviso: " = YAML key error; use "Aviso, ".

js-yaml NOT available globally in Node.js. Python yaml.safe_load fails on `equal: =` (YAML 1.1 tag) — not a real error.

`monitoring.prometheus.warningInstalled` multi-line value contains `Warning:` — grep falsely counts as YAML key.

ICU block `|-` vs flow scalar — both valid, not a structural violation.

## Persistent violations (3+ verify runs, still unfixed as of 2026-03-16)
1. `drivers.deactivate.warningDrivers`: `{names}` → `{name}` (lost 's')
2. `istio.customOverlayFile.tip`: missing `{vendor}` + 2nd link
3. `monitoring.prometheus.warningInstalled`: missing 2nd paragraph with `{vendor}`
4. `monitoringReceiver.webhook.modifyNamespace`: URL with HTML entities → "ajuste conforme necessário"
