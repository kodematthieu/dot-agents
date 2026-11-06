# Lens: Visual Analysis

Use when analyzing uploaded architecture diagrams (C4, UML, network topologies), sequence/state charts, UI flows, or whiteboard sketches—only when the active host exposes the media.

## Inspection Procedure

1. **Separate Visible Fact from Inference:**
   - **Visibly explicit:** Labeled nodes, directed arrows, protocol annotations, grouping boxes/trust zones, sequence numbering.
   - **Inferred (must be labeled as inferred):** Implied synchronous vs. asynchronous semantics, unshown return paths, assumed transactional atomicity, or implicit shared credentials.
2. **Audit Structural & Architectural Hazards:**
   - Unidirectional arrows hiding synchronous failure coupling or missing error/timeout handling.
   - Cross-boundary calls bypassing stated API/auth gateways or violating layering rules.
   - Cycles across services/modules, fan-in bottlenecks, single points of failure, or missing backpressure/queues between mismatched throughput tiers.
3. **Cross-Modal Reconciliation:** When textual requirements, ADRs, or repository code accompany the image, check every boundary for drift between what the diagram claims and what the text/code enforces.
4. **Legibility Gate:** Never guess blurred text, cropped edges, or ambiguous arrow directions—state precisely which region cannot be read and how that ambiguity affects the conclusion.

## Useful Outputs

- Prioritized discrepancies and architectural risks anchored to named nodes/edges in the diagram.
- When version-controlled iteration is helpful, offer a clean, corrected **Mermaid** equivalent alongside the critique.
