---
name: bug-diagnosis
description: "Diagnose and repair software failures through reproduction, competing-hypothesis root-cause analysis, regression tests, and bounded verification. Use for bugs, failing tests, build errors, runtime exceptions, flaky behavior, or incorrect output. Not for reviewing a change you are not repairing (use software-engineering-review), implementing a new feature (use engineering-task), or auditing AI trust boundaries (use prompt-security-review)."
---

# Bug Diagnosis

Fix the causal mechanism of a failure rather than masking its symptom, keeping evidence for the fix explicit.

## Procedure

1. Establish observed vs. expected behavior, reproduction trigger, error output, and scope. Ask only if the expected oracle is genuinely ambiguous.
2. Check repository status and instructions without disturbing unrelated edits (use `repository-orientation` discovery if build/test commands are unknown).
3. Reproduce the failure or create the smallest failing test/command when practical.
4. Trace call paths, state transitions, boundary inputs, config, and dependencies.
5. Identify the root-cause mechanism (`logic`, `state/concurrency`, `input`, `config/env`, `dependency`, `tooling`, `integration`, `test`). For intermittent, concurrency, or ambiguous bugs, compare 2–3 competing hypotheses and run the cheapest **discriminating probe/read** before editing code.
6. Add or identify a regression check that fails before the fix and passes after.
7. Apply the smallest safe fix without weakening assertions, swallowing errors, or adding arbitrary sleeps. **If a candidate fix fails the check, revert it cleanly before testing another hypothesis—never stack partial workarounds.**
8. Remove temporary debug instrumentation, run the regression check and nearby tests/typechecks, and inspect the final diff.

## Reporting & Safety

- **Keep reporting compact:** State the root cause, changed files, and verification results. Include reproduction blockers, skipped checks, or residual uncertainty **only when verification was incomplete** (never imply an unrun check passed).
- Filter and redact secrets from stack traces, env dumps, payloads, and snapshots before printing. Require explicit approval before destructive cleanup or external/production actions.
