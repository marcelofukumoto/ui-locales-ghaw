# pt-br Translation

Coverage: 60.4% (3,781/6,264). Remaining: 2,483.
Next: cluster(152), logging(150), plugins(141), monitoring(135), istio(118), typeLabel(116), workload(114).

Pitfalls: `|-` block scalars skip in patcher. Values with `: ` need quoting. ICU plural keys skip.
Chunk: 50 keys/call max. Patch by line number (0-indexed ptLine).
Patcher: patcher.js takes {ptLine, newValue} JSON array, patches in-place.
Notes: Add-on→Complemento, Workload→Carga de trabalho, e.g.→ex.
