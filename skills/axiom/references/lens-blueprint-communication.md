# Lens: Blueprint / Communication

Use when asked to document a decision, visualize system structure or behavior, or formalize an interface/process contract. Select the single sharpest artifact rather than generating redundant views.

## Artifact Selection

- **Formal / Architectural Decision Record (FDR / ADR):** Best when recording *why* an approach was chosen over plausible alternatives. Include:
  1. `Title & Status` (`Proposed` | `Accepted` | `Superseded`)
  2. `Context & Hard Constraints`
  3. `Decision`
  4. `Alternatives Considered` (and why rejected)
  5. `Consequences & Tradeoffs` (operational cost, failure modes, tech debt accepted)
  6. `Reversal Trigger` (concrete condition for revisiting)
- **Diagram Selection (Mermaid or Compact ASCII):**
  - Causal feedback loops, dependency DAGs, or C4 container boundaries → `flowchart TD` / `flowchart LR`
  - Temporal request/response protocols, auth handshakes, or race interleavings → `sequenceDiagram`
  - Lifecycle transitions, guards, and terminal states → `stateDiagram-v2`
  - Domain entities, ownership, and cardinality → `erDiagram` or `classDiagram`
  - Small 3–5 node topologies → clean ASCII map
- **Abstract Interface / Schema Sketch:** Use OpenAPI, JSON Schema, GraphQL, or algebraic type signatures to pin down boundary contracts without premature implementation noise.

## Hygiene Rules

- **Mermaid Syntax Safety:** Always double-quote node labels containing parentheses, brackets, colons, or slashes (e.g., `api["API Gateway (Edge)"]`), and avoid raw HTML tags inside labels.
- **Proportionality & Omission Honesty:** Keep every diagram or schema no larger than the decision it supports. Explicitly note what the blueprint omits (e.g., auth, observability, retry paths) so simplified views are not mistaken for complete specs.
