# Evaluation guidance

Load this when a prompt, skill, or agent change needs to be shown to work, not assumed to work.

## Sizing the set

Size the evaluation set by risk and failure surface, not an arbitrary round number. Cover:

- representative normal cases;
- ambiguous or underspecified requests (testing clarification gates);
- missing, stale, or contradictory evidence;
- adversarial or indirect-injection-shaped inputs;
- tool failures, permission denials, and non-idempotent timeouts;
- the exact regression or failure mode the change targets.

Continuously promote real failures observed in use into the evaluation set. A static benchmark measures only failures you anticipated at design time.

## Comparing variants

- Change one variable at a time when isolating cause, or explicitly label multi-factor bundle tests.
- Evaluate variants on identical inputs, model versions, reasoning settings, and tool mocks.
- Use deterministic programmatic assertions wherever an output property is checkable (schema validity, tool argument bounds, forbidden token/secret absence, file-path containment).
- Reserve LLM judges strictly for semantic or qualitative properties that deterministic code cannot check.
- Never claim improvement from one example. Report sample size, pass-rate delta, variance across repeated runs, and regressions introduced.

## Calibrating LLM judges

An LLM judge is an uncalibrated estimator, not ground truth:

- **Use anchored discrete rubrics, not raw floats:** Score specific criteria as binary (`pass` / `fail`) or anchored `0 / 1 / 2` levels with explicit behavioral definitions, requiring the judge to quote the exact span supporting its score. Avoid uncalibrated `1–10` Likert scales or raw `0.0–1.0` judge confidence floats.
- **Control judge biases:** Randomize A/B candidate order to detect position bias, penalize filler to counter verbosity bias, and check for self-preference when the judge shares a model family with a candidate.
- **Measure human agreement:** Validate the judge rubric against human labels on a stratified sample before trusting automated runs.
- **Keep reasoning private:** Ask the judge for quoted evidence and criterion verdicts, not raw chain-of-thought dumps.

## Metrics that generalize

Prefer operational metrics tied to system risk: task completion rate, schema/contract compliance, false-trigger and missed-trigger routing rates (for skills/agents), refusal accuracy on unauthorized actions, unintended or overly broad tool calls, latency percentiles, and token/cost budgets.

## Reporting

State the evaluation set composition, model and harness configuration, deterministic vs. judge-scored metrics, observed deltas with run-to-run variance, and explicit blind spots not covered by the suite.
