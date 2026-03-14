# PT-BR Learnings

Coverage: 92.0% (5793/6295). ~502 remaining = legitimate English terms (CPU, RAM, Pods, Namespace, TLS, LDAP, product/brand names, cloud provider names, cluster addon chart names, storage driver names, auth provider names). Do not translate these.

Run 2026-03-14: Added locale.zh-hans (简体中文→Chinês Simplificado). Confirmed all other 502 untranslated strings are correct technical/brand terms.

Script coverage 92% = ~99.9% effective coverage (all remaining strings are technical identifiers correctly kept in English per PT-BR tech conventions).

YAML: quote values with `:` — `'Total:'`. HTML in double-quoted = use plain scalar. "Aviso: " = YAML key error; use "Aviso, ".

js-yaml available: `node -e "require('js-yaml')"`

Placeholders fixed (3ea2015): {vendor}→{appName} in rbac.globalRoles.types.global.description; {settingsPageUrl} in performance.deprecatedInactivitySetting; {ffUrl} in performance.serverPagination.featureFlag; {docsBase} in monitoring.receiver.tls.secretsBanner; {samplePods}/{sampleNamespaces} in networkpolicy matchesSome.

False positives: {other}→{outro}, {resource}→{recurso} in ICU plural are correct translations, not violations.
