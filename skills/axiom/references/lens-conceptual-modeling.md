# Lens: Conceptual / Ontological Modeling

Use when defining an unfamiliar or contested domain, cleaning up overloaded terminology, or establishing invariants before schema or system design.

## Modeling Procedure

1. **Bounded Context:** State what decisions or operations the model serves and where its boundary stops.
2. **Term Disambiguation:** Separate **entities** (identity across change), **values** (defined by structure), **roles** (context-bound capability), and **events** (immutable facts).
3. **Structural Relations:** Distinguish two relations routinely conflated in prose:
   - **Mereology (Part–Whole):** Ownership, containment, and cascade lifecycle when the whole changes or disappears.
   - **Taxonomy (Subtype–Supertype):** Behavioral substitutability (`is-a`) where every parent invariant holds for the subtype.
4. **Invariants & State Space:** Specify valid states and transitions. Use compact notation (`A -> B`, `f(g(x))`, `{x in S | invariant(x)}`) only where prose leaves edge cases ambiguous.
5. **Rule Provenance:** Derive constraints from evidence or stated premises; mark any gap-filling rule explicitly as an assumption.

## Reporting Economy

Do not impose full ontological scaffolding when two crisp definitions resolve the ambiguity. Emit only the definitions, relation boundaries, invariants, and unresolved edge cases that change downstream design.
