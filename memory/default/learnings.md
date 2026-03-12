# pt-br Translation Learnings

## File Stats
- en-us.yaml: 6,348 leaf keys; pt-br.yaml matches exactly

## Placeholder False Positives
ICU plural inner text (e.g. `{items}` in `{count, plural, =1 {item} other {items}}`) is falsely flagged. Skip any "missing" placeholder containing `,` or spaces.
`<Empty>` → `<Vazio>` is correct (bracket-word display convention, not HTML).

## Coverage (final)
Total: 6,348 | Skipped: 53 | Translated: 5,795 | Kept-in-English: ~500 | Untranslated: 0 → **100%**

## Kept-in-English (500 strings, all confirmed correct)
Cloud providers, CSI storage drivers, auth providers (LDAP/SAML/OIDC/Keycloak/etc), K8s resources, time/size units, tech acronyms, product names, icon CSS class names (asyncButton: checkmark/refresh/error), words identical in PT-BR (Total/Normal/Status/Global/etc), locale names (简体中文).

## Run History
- 2026-03-11 Run 1: Fixed `{currentLabel}` placeholder in `promptRollback.revisionOption`
- 2026-03-11 Run 2: All structural checks pass; 89.5% coverage
- 2026-03-11 Run 3: improve-translation → 91.9%
- 2026-03-12 Run 4: All checks pass; 100% coverage; PR approved + ready-to-merge
