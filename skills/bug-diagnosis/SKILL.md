---
name: bug-diagnosis
description: "Diagnose and repair software failures through reproduction, root-cause analysis, regression tests, and bounded verification. Use for bugs, failing tests, build errors, runtime errors, incorrect generated output, or unexpected behavior. Not for reviewing a change you are not repairing, or auditing a system boundary."
---

# Bug Diagnosis

## Purpose

Fix the cause of a failure rather than suppressing its symptom. Keep diagnosis, repair, and verification distinct enough that the evidence for the fix remains visible.

This skill assumes the goal is a repair with a regression check, not only an explanation.

## Procedure

1. Capture observed behavior, expected behavior, reproduction steps, error output, environment, and constraints.
2. Inspect current status and applicable repository instructions without disturbing unrelated work.
3. Reproduce the failure, or create the smallest focused failing test or command when reproduction is feasible.
4. Trace the relevant call path, state transitions, inputs, configuration, dependencies, and existing tests.
5. Classify the likely root cause as logic, state, input, environment, dependency, tooling, integration, or test.
6. Add or identify a regression check that distinguishes the failure from the corrected behavior.
7. Apply the smallest safe fix without weakening assertions, suppressing errors, or broadening scope without evidence.
8. Run the regression check and nearest relevant tests, builds, typechecks, or runtime checks.
9. Inspect the diff and report evidence, remaining uncertainty, and skipped checks.

## Decision Rules

- If expected behavior or reproduction is materially unclear, ask for the smallest missing information rather than inventing an oracle.
- Retry a failed operation only after classifying the failure and only when the retry is safely idempotent.
- A timeout after a write, migration, publication, or external request is not automatically retryable; determine whether it completed first.
- If the failure cannot be reproduced, distinguish diagnosis from confirmation and use static evidence or a focused test without claiming reproduction.
- Do not fix unrelated failures unless they block verification or the user expands scope.

## Output Contract

Report:

- observed versus expected behavior;
- reproduction command or reason reproduction was unavailable;
- root-cause classification and evidence;
- changed files and why;
- regression test or verification path;
- commands and results;
- unresolved uncertainty and residual risk.

For each check, state expected versus actual. List checks you ran, checks you skipped and why, and any area left unverified. A regression check that could not run is not evidence of a fix; say so explicitly rather than implying the failure is resolved.

## Safety

Do not print secrets while collecting diagnostics. Redact sensitive values from logs and reports. Stop before destructive cleanup, production changes, or external side effects unless the user has explicitly authorized them and the host permits them.
