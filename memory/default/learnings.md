# Translation Learnings

## Environment
- Node.js v20. Run `npm install js-yaml` in `/tmp/gh-aw/agent/`.

## pt-br PR #36 Issues (2026-03-13)
YAML errors: line 344 `percent: %`→`"%"`, line 6435 helmPrefix ends with `:`, line 9033 `max: Total:`.
Structure: `cluster.harvester.warning.cloudProvider.incompatible` has `https: //` space → mismatch.
Placeholders dropped: authConfig.associatedWarning, ldap.oktaSchema, azuread modal, backupRestoreOperator (2), catalog.install.steps.basics.description ({vendor} lost).

## Tips
- Fix YAML errors with loop: `while(!parse) fix line N`
- ICU word changes (outros/recurso) are false positives in placeholder check
- Most "untranslated" strings are tech terms; expect ~99.8% real coverage after agent review
