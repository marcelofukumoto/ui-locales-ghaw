# Translation Learnings — pt-br

## Setup
- Locale: `pkg/ui-locales/l10n/pt-br.yaml` (9514 lines fixed)
- Node.js only (no pip). Patcher: `/tmp/gh-aw/agent/patch.js`
- Call: `node patch.js file.yaml '{"key":"value",...}'` (max 50/call)
- Analyzer: `/tmp/gh-aw/agent/analyze.js` → untranslated.json

## Pitfalls
- Keys with `'true'` in path may not be found by patcher
- ICU plurals: translate text only, preserve syntax
- Auto-quoting handles special chars in values

## Coverage
- Initial: 16% (985). Run 1: 32% (1983, +998). Remaining: ~4135

## Priority next run
cluster(312), fleet(226), persistentVolume(206), storageClass(198), workload(173), catalog(168), tableHeaders(157), logging(155), plugins(141)

## Run 1 coverage
authConfig(complete), cluster(credentials/machineConfig/rke2/k3s/providers/tabs), workload(security/scheduling/networking/jobs), fleet(settings/dashboard/gitRepo), logging(flows/elasticsearch), generic/about/nav
