# PT-BR Learnings

Coverage: 92.1% (5791/6291). ~500 remaining = legitimate English terms (CPU, RAM, Pods, Namespace, TLS, LDAP, product names). Do not translate.

YAML: quote values with `:` — `'Total:'`. HTML in double-quoted = use plain scalar. "Aviso: " = YAML key error; use "Aviso, ".

js-yaml available: `node -e "require('js-yaml')"`

Placeholders fixed (3ea2015): {vendor}→{appName} in rbac.globalRoles.types.global.description; {settingsPageUrl} in performance.deprecatedInactivitySetting; {ffUrl} in performance.serverPagination.featureFlag; {docsBase} in monitoring.receiver.tls.secretsBanner; {samplePods}/{sampleNamespaces} in networkpolicy matchesSome.

False positives: {other}→{outro}, {resource}→{recurso} in ICU plural are correct translations, not violations.
