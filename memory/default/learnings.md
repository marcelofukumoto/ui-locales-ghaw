# pt-br Learnings

## Tooling: use `yaml` npm package (not js-yaml)

## Recurring issues
- `cluster.harvester.warning.cloudProvider.incompatible`: double-quoted value with HTML attrs — use plain scalar
- `{vendor}` frequently dropped; `&nbsp;`,`&lt;`,`&gt;` stripped in performance keys
- ICU plural text `{other}→{outro}` = false positive, not a real violation

## Agent review: "untranslated" items are kept-in-English technical terms
Pod,Namespace,CPU,TLS,LDAP,Grafana,Prometheus,Longhorn etc = keep in English

## Coverage PR#36 (Mar 14): ~99.98% after review; 1 genuine: catalog.install.warning.managed
