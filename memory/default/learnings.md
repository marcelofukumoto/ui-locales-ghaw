# PT-BR 2026-03-16 (updated)
Keys:6349 Coverage:~92% (5795/6297 translatable; ~502 "untranslated" are tech terms/cognates/correct)
All 7 placeholder violations FIXED in commit 5c8cdc7 (2026-03-16).
ICU false positives: {item}→{item_pt} inside plural=NOT missing placeholder.
YAML: bare% quoted, value-ending-colon quoted, HTML-in-doublequotes escaped.
Tool: npm install js-yaml --prefer-offline --no-save (no pypi).
Chunking: max ~50 keys/bash call; patch in-place with Node.js read/splice/write; do NOT commit yarn.lock.
Remaining ~502 "untranslated": K8s terms, cloud/auth provider names, time abbrevs, pure vars, CSS classes — all correct pt-br practice.
HTML-truncation pattern: AI drops <a>,<pre>,<strong>,<br/> when truncating long strings. setup.eula left in English. 16 open violations as of 2026-03-16T16:38 run (see PR#36 comment). False positives: URL-template <registry-host>, semantic <Empty>→<Vazio>, ICU branches {other}→{outro}.
Fixed (commit 164a6e5): cluster.banner.machinePoolError, fleet.clusterGroup.selector.matchesSome, monitoring.v1Warning, networkpolicy.selectors.matchingPods/Namespaces.matchesSome, featureFlags.warning, servicesPage.selectors.matchingPods.matchesSome.
