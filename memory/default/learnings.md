# PT-BR learnings (2026-03-16 run 7)
Keys:6349, parity OK. Coverage:100% (agent review).
Python3+pyyaml works (no pip). node_modules js-yaml broken (PnP worktree issue).
YAML fix: `equal: =` needs custom constructor for tag:yaml.org,2002:value.
ICU false positives: branch text {item}/{items} flagged as missing vars. 19 false positives in pt-br.
All 281 "untranslated" = keep-in-English (providers, K8s addons, cognates, icon IDs, tech labels).
6 violations from run 5 all fixed by improve-translation.
Block scalar pitfall: splicing removes next key if it's the Nth line (promptSlo: was line 5 of scaling block).
Max 50 keys/call.
