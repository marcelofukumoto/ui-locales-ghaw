# PT-BR Learnings (2026-03-16)
Coverage: 5789/6349 keys translated (93.1%). 426 same-as-EN, 134 skipped. YAML valid, 0 parse errors, perfect key parity.
The 426 "untranslated" are all legitimate: K8s terms, product/brand names, cloud providers, abbreviations, cognates.
Do NOT translate: Namespace/Pod/Cluster/etcd, product names (Longhorn/Rancher/Fleet/Istio/NeuVector/Grafana/Prometheus/Elasticsearch/Redis/Kafka), cloud providers (Amazon/Azure/Google/DigitalOcean), abbreviations (CPUs/RAM/MiB/IPv4/IPv6/TLS/CSI), auth providers (GitHub/GitLab/Keycloak/Okta), log levels (Info/Debug/Trace), icon CSS class names.
Tooling: js-yaml in project node_modules; run scripts FROM project dir not /tmp; never `npm install`.
Previous fixes: suffix.percent bare % → "%", cloudProvider.incompatible double-quote+HTML, 21 placeholder violations.
ICU note: {other}→{outro} and {items}→{itens} are word-form changes not missing placeholders.
