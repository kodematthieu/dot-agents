---
name: prompt-engineering
description: "Design, review, or improve system prompts, developer instructions, agent specs, skills, tool contracts, routing descriptions, output schemas, and prompt evaluations. Use when instruction behavior, context structure, cross-model adaptation, progressive disclosure, or evaluation methodology needs work. Not for security/injection boundary audits (use prompt-security-review) or PR diff-hygiene checks on surrounding code (use software-engineering-review)."
---

# Prompt Engineering

Treat prompts, skills, and agent specs as versioned behavioral interfaces. Design for observable outcomes, bounded authority, low token overhead, cross-model reliability, and measurable evaluation.

## On-demand references

- `references/provider-claims.md` — verify context limits, caching, reasoning toggles, structured outputs, and tool-call shapes against current docs before encoding them.
- `references/evaluation.md` — dataset sizing, variant comparison, anchored judge rubrics, and reporting.
- `references/skill-and-agent-authoring.md` — progressive-disclosure sizing, trigger `description` precision, model-agnostic phrasing, and cross-harness `SKILL.md` / `agents/*.md` schema portability.

## Procedure

1. Define objective, trusted vs. untrusted inputs, allowed tools/actions, acceptance criteria, and failure behavior.
2. Separate global policy, repo facts, on-demand skills, task context, provider adapters, and deterministic runtime controls (preferring Direct Call → Workflow → Single Agent → Subagents).
3. Use calm, observable rules and positive framing; avoid shouting (`CRITICAL`, `MUST`, `MANDATORY`) that causes frontier thinking models to over-trigger.
4. Place long reference context before active instructions; keep specialized procedures progressive (`SKILL.md` + `references/`) rather than growing always-on mega-prompts.
5. Eliminate output bloat: avoid forcing multi-heading ceremonial printouts, chain-of-thought dumps, or artificial confidence floats when concise answers suffice.
6. Specify clarification gates, narrow tool selection, approval gates, idempotent retry caps, and stop conditions.
7. Put hard guarantees in runtime permissions, sandboxes, schemas, hooks, or CI rather than `"do not"` prose.
8. Audit for internal contradictions, sibling-skill routing collisions, unverified provider claims, and context waste; define deterministic checks + anchored eval cases (`references/evaluation.md`) before claiming gains.

## Reporting & Safety

- **Keep output proportional:** Deliver the drafted/revised prompt or prioritized critique directly. Include trust-boundary notes, runtime controls, or evaluation designs **only where missing, changed, or requested**.
- Never place real secrets in prompts or examples, and never claim prompt prose enforces sandboxing or permissions.
