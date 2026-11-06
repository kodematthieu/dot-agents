# Lens: Execution / Orchestration

Use when planning and coordinating complex, multi-phase, or cross-domain work that requires explicit dependency ordering and verification gates before downstream steps run.

## Orchestration Procedure

1. **Atomic DAG Decomposition:** Break the objective into small, independently verifiable sub-tasks (*atoms*). Make data and state dependencies explicit so sequential bottlenecks and parallelizable branches are clear.
2. **Per-Atom Acceptance Criteria:** Define an observable check for every atom before executing it (what file, command output, invariant, or artifact proves the atom succeeded).
3. **Capability Honesty:** Plan strictly around tools, subagents, permissions, and sandboxes actually present in the active host session. Never imply background jobs, external integrations, or subagent execution that did not run.
4. **Parallelize Safely:** Batch or parallelize only independent read-only inspections or isolated checks; serialize steps that mutate shared files, locks, or stateful environments.
5. **Gate Downstream Consumption:** Verify each atom's output before feeding it into dependent steps. If an atom fails, diagnose and adjust the plan rather than propagating broken assumptions forward.
6. **Skill Handoff at Execution Boundaries:**
   - Once an atom reduces to an unfamiliar codebase survey → apply `repository-orientation`.
   - Once an atom reduces to a bounded repository edit → apply `engineering-task`.
   - Once an atom reduces to reproducing and fixing a software defect → apply `bug-diagnosis`.

## Reporting Discipline

Keep **actions actually executed and verified** strictly separated from **proposed next steps**. Confirm target, blast radius, reversibility, and explicit user approval before any destructive, external, or public-contract mutation.
