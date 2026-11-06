# Lens: Conceptual / Ontological Modeling

Use when defining an unfamiliar or contested domain, cleaning up overloaded terminology, or establishing invariants before schema or system design.

## Modeling Procedure

1. **Bounded Context & Purpose:** State what decisions or operations this model must support—and explicitly mark where its boundary stops (terms often change meaning across adjacent contexts).
2. **Term Disambiguation:** Define core terms by necessary and sufficient operational criteria. Separate an **entity** (persists through change via identity) from a **value/attribute** (defined solely by structure), a **role** (context-dependent capability), and an **event** (immutable historical fact).
3. **Structural Relations:** Distinguish two relations routinely conflated in informal prose:
   - **Mereology (Part–Whole):** Composition, ownership lifecycle, and containment boundaries—if the whole is deleted or invalidated, what happens to its parts?
   - **Taxonomy (Subtype–Supertype):** Behavioral substitutability (`is-a`)—does every invariant of the parent genuinely hold for the subtype?
4. **State Space & Invariants:** Specify valid states, permitted transitions, and invariants that must hold across every transition. Use lightweight formal notation where prose leaves edge cases ambiguous:
   - Implication / constraints: `A -> B`
   - Transformation / composition: `f(g(x))`
   - Valid state set: `{x in S | invariant(x)}`
5. **Provenance of Rules:** Derive domain constraints strictly from evidence or user-stated premises. Any rule introduced to close a logical gap must be flagged explicitly as a **proposed assumption**.

## Output Contract (`Domain / Systems Model`)

- **Boundary & Ubiquitous Vocabulary:** Canonical definitions and explicitly rejected synonyms/conflations.
- **Entities, Relations & Cardinalities:** Identity keys, part–whole ownership, and lifecycle transitions.
- **Invariants & Forbidden States:** Rules that cannot be violated without corrupting the domain.
- **Open Edge Cases:** Ambiguities that require a product, legal, or empirical decision rather than further abstraction.

Do not impose heavy ontological machinery where two crisp definitions resolve the confusion.
