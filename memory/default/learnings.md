# pt-br Translation

Run 6: 91.6% (5,772/6,301). Remaining: 529 (all brand names/tech terms).
Run 5: 89% (5,577). Run 4: 74.1%. Run 3: 60.4%. Run 2: 46.5%. Run 1: 32%.

Tools: patcher.js (scalar+block). No npm needed.
Chunk: 40-50 keys/call max. JSON patch files.

True ceiling: ~92%. Remaining 529 = all legitimately English:
Amazon/Azure/Google, Longhorn/CoreDNS/etc., CPU/RAM/URL/TLS/etc.,
time units (5s/1m/etc.), pure placeholders.

Sections done: 90+ sections fully translated.
Pitfalls:
- Python yaml fails on `equal: =` (pre-existing). Use Node.js.
- Multi-line flow scalars: patcher replaces first line only, remove leftover lines.
- Block scalar keys: patcher converts |- to inline (fewer lines, OK).
Key parity: 6,347 keys ✅. ICU plurals work with patcher.
