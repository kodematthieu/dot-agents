---
name: bug-diagnosis
description: "Diagnose and repair software failures through reproduction, competing-hypothesis root-cause analysis, regression tests, and bounded verification. Use for bugs, failing tests, build errors, runtime exceptions, flaky behavior, or incorrect output. Not for reviewing a change you are not repairing (use software-engineering-review), implementing a new feature (use engineering-task), or auditing AI trust boundaries (use prompt-security-review)."
---

# Bug Diagnosis

## Purpose

Repair the causal mechanism of a failure rather than masking its symptom. Keep reproduction, root-cause falsification, minimal repair, and verification distinct so the evidence proving the fix stays explicit.

## Procedure

1. Capture observed behavior, expected behavior, reproduction trigger, exact error output, environment assumptions, and scope constraints.
2. Inspect repository status and applicable instructions without disturbing unrelated workspace changes. If test/build commands or entry points are unknown, apply `repository-orientation` discovery first rather than guessing commands.
3. Reproduce the failure directly, or write the smallest focused failing test/command when live reproduction is practical.
4. Trace the execution path, state transitions, boundary inputs, configuration, dependencies, and nearby tests.
5. Formulate the causal mechanism (`logic`, `state/concurrency`, `input/boundary`, `environment/config`, `dependency`, `build/tooling`, `integration`, or `faulty test`). For intermittent, concurrency, or ambiguous failures, list 2–3 competing hypotheses and run the cheapest **discriminating read or diagnostic check** before editing production code.
6. Establish a regression test or check that fails before the fix and passes only when the root cause is resolved.
7. Apply the smallest safe fix without weakening assertions, swallowing errors, adding arbitrary sleeps, or broadening scope.
8. Strip any temporary debug logging or diagnostic probes added during investigation, then run the regression check alongside nearest relevant tests, typechecks, and builds.
9. Inspect the final diff and report evidence, skipped checks, and residual risk.

## Decision Rules

- If expected behavior or the failure oracle is materially ambiguous, ask for the smallest missing fact rather than inventing requirements.
- **Revert failed hypotheses cleanly:** If a candidate fix fails the reproduction check, revert that edit before testing a new hypothesis—never accumulate stacked speculative workarounds.
- Retry a failed command only after classifying the error and confirming idempotency. A timeout after a write, migration, publication, or external call is **not** automatically safe to retry; check state first.
- When reproduction is impossible in the current environment, separate static root-cause analysis from verified confirmation—never imply an unrun regression check proved the fix.
- Leave unrelated defects untouched unless they directly block verification or the user expands scope.

## Output Contract

Report:

- observed vs. expected behavior;
- reproduction command/test (or exact reason reproduction was blocked);
- root-cause mechanism, classification, and discriminating evidence;
- files changed and why;
- regression check and verification commands with expected vs. actual results;
- checks skipped or blocked and why;
- unresolved uncertainty and residual risk.

## Safety

Diagnostic collection (`env`, stack traces, request payloads, crash dumps, test snapshots) routinely exposes credentials and tokens—filter and redact sensitive values before printing or reporting. Require explicit user approval before destructive cleanup, state resets, or external/production operations.
