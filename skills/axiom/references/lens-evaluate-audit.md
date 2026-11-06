# Lens: Evaluate / Audit

Use when critiquing an idea, system design, argument, policy, or proposal. Act as a constructive adversary searching for structural entropy.

## Audit Checklist

1. **Steelman & Load-Bearing Premises:** Restate the strongest coherent version of the proposal first. Separate load-bearing assumptions (if false, the design fails) from incidental preferences.
2. **Ontological & Goal Contradictions:** Does the proposed mechanism actually optimize for the stated objective, or optimize a proxy that diverges under load?
3. **Incompatible Trilemmas:** Check whether the design simultaneously claims three mutually constrained properties without naming what gives under stress (e.g., CAP/PACELC under partitions, latency vs. throughput vs. batch cost, security vs. frictionless UX vs. operational simplicity, expressiveness vs. decidability).
4. **Systemic Fragility & Tight Coupling:** Hidden synchronous dependencies, shared mutable state across boundaries, distributed monoliths, or brittle Temporal/ordering assumptions.
5. **Process Interference & Contention:** Race conditions, lock/queue contention, head-of-line blocking, starvation, or competing claims on finite budgets.
6. **Single Points of Failure (SPOF):** Undocumented operational bottlenecks, single credentials/coordinators, or correlated failure domains masquerading as redundancy.
7. **Feedback Loops & Incentive Distortion:** Unbounded retries (retry storms), cascading failures, causal circularity, or Goodhart's Law / organizational incentives that undermine the intended rule.
8. **Missing Dampeners & Safeguards:** Absent idempotency keys, backpressure, rate limits, circuit breakers, timeouts, dead-letter paths, or rollback paths.

## Output Contract (`Architecture / Proposal Review`)

- **Scope & Load-Bearing Assumptions:** What is evaluated and what premises must hold.
- **Findings (Ordered by Consequence):** Concrete failure mechanism, trigger condition, and impact—not stylistic nitpicks.
- **Remediation Proposals (When Alternatives Exist):** Assign compact IDs (`SYS_001`, `ARCH_001`), coarse complexity (`Low` / `Medium` / `High`), and an explicit tradeoff table across the axes that actually dominate (e.g., Latency vs. Consistency, Cost vs. Resilience, Reversibility vs. Completeness).
- **Verdict & Reversal Condition:** Do not manufacture false balance. If the design is sound, say so clearly and state what scale, load, or threat shift would invalidate that verdict.
