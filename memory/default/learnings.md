# PT-BR 2026-03-16 (updated)
Keys:6349 Coverage:~92% (5795/6297 translatable; ~502 "untranslated" are tech terms/cognates/correct)
All 7 placeholder violations FIXED in commit 5c8cdc7 (2026-03-16).
ICU false positives: {item}→{item_pt} inside plural=NOT missing placeholder.
YAML: bare% quoted, value-ending-colon quoted, HTML-in-doublequotes escaped.
Tool: npm install js-yaml --prefer-offline --no-save (no pypi).
Chunking: max ~50 keys/bash call; patch in-place with Node.js read/splice/write; do NOT commit yarn.lock.
Remaining ~502 "untranslated": K8s terms, cloud/auth provider names, time abbrevs, pure vars, CSS classes — all correct pt-br practice.
