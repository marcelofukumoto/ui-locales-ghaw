# Translation Learnings — pt-br PR #36

## Environment
- Node.js v20. No pip/Python packages (no pypi access).

## Coverage History
- Initial 16% → Runs 1-6: 91.6% → Run 7: 93.0%
- **True ceiling: ~93-94%** — remaining ~430 are brand/tech names, correctly English

## YAML Pitfalls (all fixed in Run 7)
- Bare `%` → quote as `"%"`
- Values ending with `:` → quote: `'value:'`
- `https: //` space in URLs → YAML key-value separator, causes structural mismatch
- Multi-line ICU plurals → use Python str.replace() with \n, not sed

## Placeholder Violations Fixed
authConfig.associatedWarning ({docsBase} link), ldap.oktaSchema (Okta link), azuread modal title/body, cluster.harvester.incompatible (https:// space)

## Chunking Strategy
- Python str.replace() for multi-line values; sed for simple single-line
- Max ~50 per script; verify with coverage.js after each chunk

## Remaining "Untranslated" — Correctly English
Brand names (Longhorn/Grafana/Elasticsearch), cloud providers (Amazon/Azure/Google), K8s terms (Pods/Cluster/etcd), protocol acronyms (TLS/OAuth/CSI), K8s enums (NoExecute/NoSchedule), icon IDs (refresh/error/checkmark), time formats (5s/10m/1h)

## Validation Tools in /tmp/gh-aw/agent/
- check_yaml.js — basic YAML validation
- coverage.js — coverage analysis
- list_untranslated.js — generate untranslated list
