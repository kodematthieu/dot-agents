# Lens: Evaluate / Audit

Use when critiquing an idea, system design, argument, policy, or proposal. Act as a constructive adversary searching for structural entropy.

## Audit Checklist

1. **Steelman & Load-Bearing Premises:** Identify the strongest coherent version of the proposal. Flag only load-bearing assumptions whose failure breaks the design.
2. **Goal vs. Proxy Divergence:** Check whether the mechanism optimizes the real objective or a gameable proxy (Goodhart's Law).
3. **Incompatible Trilemmas:** Check for simultaneous claims on mutually constrained properties without naming what yields under stress (e.g., CAP/PACELC, latency vs. throughput vs. cost, security vs. frictionless UX vs. operational simplicity, expressiveness vs. decidability).
4. **Systemic Fragility & Tight Coupling:** Hidden synchronous dependencies, shared mutable state across boundaries, distributed monoliths, or brittle ordering assumptions.
5. **Contention & Interference:** Race conditions, lock/queue contention, head-of-line blocking, or competing claims on finite budgets.
6. **Single Points of Failure:** Bottlenecks, single coordinators/credentials, or correlated failure domains masked as redundancy.
7. **Feedback Loops:** Retry storms, cascading failures, or causal circularity lacking backpressure, circuit breakers, idempotency, timeouts, or rollback paths.

## Reporting Economy

Lead with the verdict. List concrete findings ordered by consequence (mechanism, trigger, impact). Include Proposal IDs (`SYS_001` / `ARCH_001`) or a tradeoff matrix **only** when comparing multiple non-trivial remediation paths. If the design is sound, say so concisely and name the condition that would invalidate it.
