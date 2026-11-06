# Lens: Formal Verification

Use when reasoning about concurrency, distributed protocols, state-machine correctness, security invariants, or subtle relational constraints where informal intuition fails.

## Selecting the Right Formalism

- **TLA+ (Temporal Logic of Actions):** Choose for concurrent algorithms, distributed state machines, message reordering/loss, crash recovery, safety invariants, and temporal liveness properties.
- **Alloy (Relational First-Order Logic):** Choose for structural constraints, access-control policies, ontology consistency, graph/topology rules, and bounded counterexample search over static relations.
- **SMT / Z3 or Property-Based Specs:** Choose when checking arithmetic/bitvector bounds, scheduling/routing constraints, or executable state-machine invariants directly against implementation code.

## Verification Structure

1. **System Model:** Define state variables, initial states (`Init`), and atomic state transitions (`Next`), explicitly modeling nondeterminism (partial failure, duplicate delivery, reordering, concurrent actors).
2. **Properties (Falsifiable Form):**
   - **Type / Structural Invariants:** State variables remain within well-formed bounds.
   - **Safety Properties** (*nothing bad ever happens*): Mutual exclusion, conservation laws, no unauthorized read/write, monotonic commit history.
   - **Liveness Properties** (*something good eventually happens*): Termination, eventual convergence, starvation freedom—always paired with explicit **fairness assumptions** (`WF`/`SF`), without which liveness typically fails trivially.
3. **Environment Assumptions:** State what faults are modeled vs. excluded (e.g., crash-recovery vs. Byzantine actors; bounded vs. unbounded network delay).
4. **Counterexample Trace:** Show concrete step-by-step interleavings where an invariant breaks when a guard or assumption is weakened.

## Honesty Gate

Formal notation is **not** proof on its own. Distinguish clearly between:
- a specification **actually checked** by a model checker/solver in the current session (report exact tool command, bounds/constants, states explored, and result); and
- an **unchecked specification** drafted for human clarity or external execution (provide suggested `tlc` / Alloy / solver invocation commands and state the finite bounds still unverified).
