# pt-br Translation

Run 5: 89% (5,577/6,296). Remaining: 719 (mostly brand names).
Run 4: 74.1% (4,669). Run 3: 60.4%. Run 2: 46.5%. Run 1: 32%.

Tools: patcher.js (scalar), block_patcher.js (|-). No npm needed.
Chunk: 40-50 keys/call max. JSON patch files.

Remaining: cluster(126), logging(41), typeLabel(37), workload(34), fleet(32),
persistentVolume(32), model(26), tableHeaders(25), authConfig(22).
Most remaining = brand names (Calico, LDAP, Amazon) = legitimately English.

Sections done: 90+ sections fully translated.
Pitfalls: Python yaml fails on `equal: =` (pre-existing). Use Node.js checker.
Key parity: 8,515 keys ✅. ICU plurals in block scalars work with block_patcher.
