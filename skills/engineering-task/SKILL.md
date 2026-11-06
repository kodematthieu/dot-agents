---
name: engineering-task
description: "Implement a scoped software-engineering change with repository-aware planning, minimal edits, focused tests, diff inspection, and evidence-based verification. Use when the user requests code, configuration, dependency, or test changes in an existing repository. Not for diagnosing an existing failure, reviewing a finished change, or deciding whether the approach itself is sound."
---

# Engineering Task

## Purpose

Turn a requested repository change into a bounded implementation with a reviewable diff and verified result. Prefer the smallest reliable workflow; do not add ceremony to a small, clear change.

## Task Contract

Before editing, establish:

- observable goal;
- relevant context and files;
- allowed scope and non-goals;
- API, schema, dependency, compatibility, and security constraints;
- acceptance checks;
- approval boundaries.

Resolve these from repository evidence when possible. Ask before guessing authorization, destructive behavior, public API or schema changes, deployment state, external communication, or materially different product behavior.

## Procedure

1. Read applicable instructions and inspect the relevant implementation, callers, configuration, and tests.
2. For uncertain or multi-file work, state a short plan covering scope, dependencies, risks, and checks. Skip a formal plan for a small, obvious change.
3. Follow existing repository patterns and make the smallest safe edit.
4. Add or update focused tests when behavior changes or a regression is involved.
5. Inspect the final diff for accidental rewrites, unrelated files, generated-file mistakes, and public behavior changes.
6. Run the narrowest relevant checks, then broader checks when practical.
7. Report evidence, skipped checks, assumptions, and residual risks.

## Decision Rules

- Read before editing; do not infer code behavior from filenames or prior assumptions.
- Preserve unrelated user changes. Never reset or overwrite work you did not create.
- Do not broaden a fix, update unrelated dependencies, or create abstractions without evidence of need.
- If the approved goal requires a public API, schema, permission, deployment, external-system, or destructive change, stop at the boundary and ask for approval.
- Treat test, compiler, build, diff, and runtime results as evidence. A successful edit is not proof of completion.

## Output Contract

Final report:

- summary of the change;
- files changed and purpose;
- observable behavior or API/data effects;
- verification commands and results;
- skipped checks and why;
- assumptions, residual risks, and follow-up;
- confirmation that unrelated files were not changed, when verified.

## Safety

Skill instructions do not grant permissions. Follow the host's permission and approval decisions. Do not expose secrets, publish changes, commit, push, deploy, or modify external systems unless explicitly requested and permitted.
