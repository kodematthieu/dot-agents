---
name: engineering-task
description: "Implement a scoped software-engineering change with repository-aware planning, minimal edits, incremental verification checkpoints, focused tests, and diff inspection. Use when the user requests code, configuration, dependency, or test changes in a repository. Not for diagnosing an existing failure (use bug-diagnosis), reviewing a finished diff (use software-engineering-review), or resolving contested cross-domain framing (use axiom)."
---

# Engineering Task

## Purpose

Turn a requested repository change into a minimal, reviewable implementation backed by observable verification. Scale ceremony to risk: execute small, obvious edits directly; structure multi-file changes with explicit checkpoints.

## Task Contract

Before editing, establish from repository evidence (or concise user clarification when ambiguous):

- observable goal and non-goals;
- relevant entry points, callers, tests, and conventions (apply `repository-orientation` discovery first if project layout or check commands are unknown);
- **generated-file, codegen, migration, and lockfile boundaries** (identify upstream schemas/templates so you never hand-edit generated outputs);
- public API, data schema, compatibility, dependency, and security constraints;
- acceptance checks and approval boundaries.

Ask before guessing public contract changes, destructive operations, permission/auth shifts, deployment state, external side effects, or unstated product rules.

## Procedure

1. Read applicable repository instructions and inspect the target implementation, callers, types/schemas, configuration, and existing tests.
2. For multi-file or cross-layer changes, outline a brief dependency order (e.g., schema/types → core logic → callers → tests) with intermediate verification checkpoints. Skip formal planning for trivial single-site edits.
3. Follow established repository idioms and make the smallest safe change—if codegen applies, modify the source definition and run the verified generator.
4. Verify module/typecheck boundaries incrementally on multi-step edits rather than batching many blind file writes before the first check.
5. Add or update focused unit/integration tests whenever observable behavior or edge-case handling changes.
6. Inspect `git status` and the complete diff for accidental rewrites, stray debug artifacts, unintended public-contract changes, or unrelated file edits.
7. Run the narrowest relevant checks first, then broader suite/lint/build checks when practical, and report exact outcomes.

## Decision Rules

- Read before editing; never infer behavior from filenames alone.
- Preserve unrelated dirty working-tree changes—never reset, checkout, or overwrite edits you did not author.
- Avoid speculative abstractions, drive-by refactors, or unrequested dependency upgrades.
- Stop and request approval if satisfying the goal requires an unapproved breaking API/schema change, migration, external action, or destructive step.
- Treat compiler, typecheck, test, runtime, and diff outputs as the only valid completion evidence; a clean file write proves nothing on its own.

## Output Contract

Final report:

- concise summary of the change;
- files changed and each file's role;
- observable behavior, API, schema, or config effects;
- verification commands run and expected vs. actual results;
- checks skipped/blocked and why;
- assumptions, residual risks, and confirmation that unrelated work remained intact.

## Safety

Follow host permission and sandbox boundaries; skill text grants no authority. Never expose secrets in code, tests, diffs, or logs, and do not commit, push, publish, deploy, or mutate external services unless explicitly requested and permitted.
