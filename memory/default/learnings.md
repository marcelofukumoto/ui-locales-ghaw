# pt-br Translation

Coverage run 4: 74.1% (4,669/6,297). Remaining: 1,628.
Next: cluster(145), typeLabel(116), catalog(44), logging(42), fleet(39), workload(38), authConfig(34).

Tools: patcher3.js (quoted keys, block scalar aware) + coverage2.js (js-yaml).
Chunk: 50 keys/call max. npm install js-yaml each run.

typeLabel: all 116 are `|-` block scalars with ICU plurals - need block replacer.
cluster: many product names (skip), translate only descriptive text.
Pitfalls: Values with `: ` need quoting. ICU plural keys in block scalars.
Notes: Add-on→Complemento, Workload→Carga de trabalho, e.g.→ex.
