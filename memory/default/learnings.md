# PT-BR learnings (2026-03-16 run 3)
Keys:6349, parity OK. Coverage:~92% script/~100% human.
16 placeholder violations fixed (commit 840aece): truncated HTML (links,br,strong,pre).
Block scalar pitfall: splicing removes next key if it's the Nth line (promptSlo: was line 5 of scaling block).
Tool: npm install js-yaml (no yarn.lock commit). Max 50 keys/call.
