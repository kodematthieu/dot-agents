---
name: prompt-security-review
description: "Audit prompts, skills, custom agents, MCP/tool servers, multi-agent workflows, repositories, and dependencies for prompt injection, secret exposure, excessive agency, confused-deputy escalation, unsafe commands/paths, output handling, and supply-chain threats. Use for dedicated AI/agent security reviews or before granting new capabilities. Not for general code/regression review (use software-engineering-review), designing prompt instructions (use prompt-engineering), or debating domain framing (use axiom)."
---

# Prompt Security Review

Audit the complete trust and execution boundary around an AI system: untrusted data flows, capability amplification, secret exfiltration, persistent state mutation, and side effects. Prompt prose is advisory—never a substitute for runtime sandboxing, permissions, validation, or human approval.

Read `references/threat-catalog.md` before auditing to ensure full sweep coverage.

## Procedure

1. Establish protected assets, trust actors, active host permissions/sandbox posture, and audit scope.
2. Trace untrusted inputs across repository files/comments, web/RAG data, subagent summaries, MCP tool descriptions/schemas/errors, skill bundles, credentials, and persistent state (`AGENTS.md`, rules, memory, hooks).
3. Check for direct/indirect injection, obfuscated Unicode/bidi/HTML-comment payloads, MCP metadata poisoning or rug-pulls, subagent confused-deputy escalation, Markdown image/link secret exfiltration, path/symlink escape, and shell interpolation.
4. Check non-idempotent/destructive tools, missing loop/cost budgets, bypassable approval rules, unvalidated structured output feeding executors, and cross-session persistence/supply-chain risks.
5. Verify concrete boundary cases safely (read-only) where practical.

## Severity Rubric (`Precondition × Runtime Boundary × Impact`)

- **Critical:** Untrusted input can trigger arbitrary execution, secret exfiltration, or cross-session persistence without human approval.
- **High:** Reachable trust-boundary bypass, confused-deputy escalation, secret exposure into context, or weak approval gate.
- **Medium:** Overly broad tool/permission grant, unvalidated internal output handoff, or missing budget/idempotency guard.
- **Low:** Advisory prompt gap already blocked from exploitation by hard runtime sandboxing/permissions.

## Reporting & Safety

- **Compact findings:** Order by severity using `[Severity] boundary/file — precondition, concrete attack path/impact, and fix (runtime control vs. prompt hardening)`. If clean, state the audited boundary and blind spots concisely.
- Redact credentials and live exfiltration URLs. Never install third-party packages, connect to untrusted remote MCP servers, or run destructive/networked exploits during review without explicit authorization and isolation.
