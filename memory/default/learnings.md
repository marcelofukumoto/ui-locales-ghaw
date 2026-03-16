# PT-BR Learnings

Outstanding placeholder violations (2026-03-16):
- `cluster.banner.machinePoolError`: other branch missing `{pool_name}`, `{fields}`
- `fleet.clusterGroup.selector.matchesSome`: other drops `{sample}`
- `monitoring.v1Warning`: truncated, missing second `{vendor}`
- `networkpolicy.selectors.matchingPods.matchesSome`: other drops `{sample}`
- `networkpolicy.selectors.matchingNamespaces.matchesSome`: other drops `{sample}`
- `featureFlags.warning`: truncated, missing `{vendor}` restart warning

ICU false positives: `{other}→{outro}`, `{items}→{itens}` etc. are text, not vars.
Coverage: 100% (345 "untranslated" are all tech terms/cognates).
Tools: js-yaml via npm; python3 yaml fails on `equal: =`.
