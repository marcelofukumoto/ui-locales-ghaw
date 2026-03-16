# PT-BR Learnings

Fixes (2026-03-16): `drivers.deactivate.warningDrivers` `{names}`, `istio.customOverlayFile.tip` `{vendor}`, `monitoring.prometheus.warningInstalled` 2nd para, `monitoringReceiver.webhook.modifyNamespace` URL, `resourceDetail.masthead.managedWarning` trailing `{managedBy}`, `validation.conflict` 3-line block `{fieldCount}/{fields}`, `action.ariaLabel.hidePass/showPass` `{area}`, `advancedSettings.edit.agentConfigBanner.text` `{agent}`, `performance.inactivity.authUserTTL` `{current}`.

Coverage: 100%. ~502 kept in English. Tricky: `validation.conflict` is 3-line `|-` block. python3 yaml fails on `equal: =` (pre-existing) — use custom constructor.
