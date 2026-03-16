# PT-BR Learnings

## File stats
- ~6,349 leaf keys, ~8,514 total keys, ~6,277 translatable, ~72 skipped

## YAML parsing
- Use js-yaml; line-by-line parsers produce false positives for long scalars with URLs
- Key count must match en-us.yaml (not line count — block scalars differ)

## Placeholder check false positives
- ICU plural/select display text that is translated (e.g. `{other}→{outro}`) is NOT a violation
- Use depth-tracking to extract only top-level ICU variable names

## Known violations (verify 2026-03-16)
1. `resourceDetail.masthead.managedWarning` — `{managedBy}` missing from trailing clause
2. `validation.conflict` — truncated; missing `{fieldCount}` and `{fields}`
3. `action.ariaLabel.hidePass` — `{area}` hardcoded to "senha"
4. `action.ariaLabel.showPass` — `{area}` hardcoded to "senha"
5. `advancedSettings.edit.agentConfigBanner.text` — truncated; missing `{agent}`
6. `performance.inactivity.authUserTTL` — truncated; missing `{current}`

## Strings correctly kept in English (~485)
Script flags ~112 as "untranslated" but after agent review all are fine:
cloud providers, addon names, storage drivers, auth providers, protocols, brand names, pure var templates, placeholders

## Previous fixes (2026-03-16)
Fixed: `drivers.deactivate.warningDrivers`, `istio.customOverlayFile.tip`, `monitoring.prometheus.warningInstalled`, `monitoringReceiver.webhook.modifyNamespace`
