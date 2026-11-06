# Evaluation guidance

Load this when a prompt change needs to be shown to work, not assumed to work.

## Sizing the set

Size the evaluation set by risk and use case, not by a fixed number. Cover:

- normal successful cases;
- ambiguous or underspecified requests;
- missing or contradictory evidence;
- adversarial or injection-shaped input;
- tool errors, denials, and timeouts;
- the specific failure the design is meant to prevent.

Add cases for failures you actually observe in production. A curated set that never changes measures the cases you thought of, not the failures that occur.

## Comparing variants

- Change one thing at a time, or state clearly that several changed together.
- Run both variants on the same cases with the same model and settings.
- Use deterministic checks wherever the output has a checkable property.
- Use judge models for subjective criteria, and calibrate the judge against human ratings on a sample before trusting its scores.
- Do not claim improvement from a single example. Report the number of cases and the size of any difference.

## Judge models

A judge model is an uncalibrated estimator, not ground truth.

- Sample judge ratings against human judgment; measure agreement.
- Watch for position bias, verbosity bias, and self-preference for the model's own output.
- Have the judge return a compact rationale and a confidence signal. Do not ask for private reasoning traces.
- Use several judges or repeated runs when the decision matters.
- Require human review for high-stakes or low-agreement cases.

## Metrics that generalize

Prefer metrics tied to the use case: task success, schema validity, refusal correctness on inputs that should be refused, latency and cost percentiles, and rate of unauthorized or unintended tool calls. Bias and safety rates have no universal values; measure them for your own system and report the measurement conditions.

## Reporting

State the evaluation set composition, the model and configuration used, the metrics, the observed difference with its uncertainty, and what the evaluation does not cover. An evaluation with no stated limits cannot support a reliability claim.