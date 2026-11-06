# Lens: Decision / Systems Analysis

Use when choosing among competing architectures, strategies, or designs with real tradeoffs under uncertainty.

## Decision Procedure

1. **Frame Hard Bounds vs. Criteria:** Separate fixed constraints from the 2–4 optimization axes that actually dominate the choice.
2. **Compare Distinct Options:** Include the **do-nothing / status-quo baseline**, the **smallest viable intervention**, and materially distinct alternatives—never strawmen.
3. **Weigh Reversibility:** Decide two-way doors (cheaply reversible) fast for learning speed; optimize one-way doors (public schemas, security boundaries, lock-in) for durability and blast-radius containment.
4. **Value of Information (VoI):** Prefer a cheap benchmark, prototype, or query over extended debate whenever empirical measurement can settle the dominant unknown quickly.
5. **Stress-Test Tail Regimes:** Check options against load spikes, partial dependency failure, operator error, and maintenance burden—not just expected-case behavior.

## Reporting Economy

Lead with the recommended option (or why the choice remains tied on a value weight), the dominating tradeoff, and the concrete condition that would flip the decision. Use a comparison table only when $>2$ options compete across multiple axes.
