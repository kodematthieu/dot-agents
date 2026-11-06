---
name: engineering-task
description: "Implement a scoped software-engineering change with repository-aware planning, minimal edits, incremental verification checkpoints, focused tests, and diff inspection. Use when the user requests code, configuration, dependency, or test changes in a repository. Not for diagnosing an existing failure (use bug-diagnosis), reviewing a finished diff (use software-engineering-review), or resolving contested cross-domain framing (use axiom)."
---

# Engineering Task

Turn a requested repository change into a minimal, verified implementation. Scale workflow to risk—avoid ceremony on small edits.

## Pre-Edit Checks

Establish internally from repository evidence (asking concisely only when ambiguous):

- goal, non-goals, and relevant entry points/callers/tests (apply `repository-orientation` discovery first if layout or check commands are unknown);
- **generated, codegen, migration, and lockfile boundaries** (edit upstream sources/schemas rather than generated files);
- public contract, compatibility, dependency, and approval boundaries.

Stop for explicit approval before changing public APIs/schemas, permissions, deployment state, external systems, or destructive paths.

## Procedure

1. Read applicable instructions and inspect target files, callers, types/schemas, config, and existing tests.
2. Plan multi-file dependency order internally (e.g., types → logic → callers → tests); surface a plan beforehand only if user confirmation is needed.
3. Follow existing repository idioms and make the smallest safe edit, running codegen when upstream schemas change.
4. Verify compile/typecheck boundaries incrementally across multi-step edits rather than batching many blind writes.
5. Add or update focused tests when observable behavior or edge cases change.
6. Inspect `git status` and diff to preserve unrelated dirty work and catch stray artifacts or unintended contract changes.
7. Run the narrowest relevant checks, then broader checks when practical.

## Reporting & Safety

- **Keep reporting compact:** State what changed (files and behavior) and the verification commands/results. Mention skipped checks, assumptions, or residual risks **only when present**—omit empty boilerplate sections and `"unrelated files untouched"` confirmations.
- Follow host permissions; never expose secrets or commit, push, publish, or mutate external systems unless explicitly requested.
