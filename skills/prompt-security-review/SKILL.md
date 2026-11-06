---
name: prompt-security-review
description: "Audit prompts, skills, custom agents, MCP/tool servers, multi-agent workflows, repositories, and dependencies for prompt injection, secret exposure, excessive agency, confused-deputy escalation, unsafe commands/paths, output handling, and supply-chain threats. Use for dedicated AI/agent security reviews or before granting new capabilities. Not for general code/regression review (use software-engineering-review), designing prompt instructions (use prompt-engineering), or debating domain framing (use axiom)."
---

# Prompt Security Review

## Purpose

Audit the full trust and execution boundary around an AI system or agent workflow: untrusted data paths, capability amplification, secret exposure, persistent state mutation, and external side effects. Prompt text is an advisory layer—never a substitute for sandboxing, least-privilege permissions, schema validation, or human approval gates.

## On-demand reference

Read `references/threat-catalog.md` before conducting the audit so coverage includes direct/indirect injection, obfuscated payloads, MCP/tool-metadata poisoning, subagent confused-deputy escalation, secret exfiltration, unsafe execution, and supply-chain persistence.

## Procedure

1. Define protected assets, trust actors, runtime permission boundaries, sandbox posture, and audit scope.
2. Trace every data-to-instruction flow: system rules, user input, repository files/comments, web/retrieved docs, subagent reports, MCP tool schemas/descriptions, skill bundles, credentials, and persistent state (`AGENTS.md`, rules, memory, hooks).
3. Inspect all relevant prompts, `SKILL.md` / `agents/*.md` files, helper scripts, `opencode.jsonc` / MCP configs, symlink targets, and runtime enforcement hooks.
4. Check for direct/indirect injection, hidden/obfuscated Unicode or HTML-comment payloads, MCP tool-metadata poisoning or rug-pulls, cross-agent confused-deputy paths, secret exfiltration (including Markdown image/URL rendering), path/symlink escape, and shell interpolation.
5. Check non-idempotent/destructive tools, missing iteration/cost budgets, bypassable approval rules, unvalidated structured output feeding downstream executors, and persistent memory/rule poisoning.
6. Where safe and read-only, verify findings against concrete boundary inputs (permission denial, malformed schema, untrusted fixture).
7. Separate advisory **prompt-level mitigations** from **deterministic runtime controls** (sandbox, allowlist, permission policy, schema validator, CI).

## Severity Calibration

Calibrate severity by **exploit precondition $\times$ runtime enforcement $\times$ blast radius**:

- **Critical:** Reachable via untrusted input (repo/web/tool output) with live capability to execute arbitrary commands, exfiltrate secrets, or persist across sessions without human approval.
- **High:** Reachable trust-boundary bypass, confused-deputy escalation, secret exposure into model context, or bypassable approval gate requiring minimal user interaction.
- **Medium:** Overly broad tool/permission scope, unvalidated model output at an internal boundary, or missing budget/idempotency guard mitigated partially by host prompts.
- **Low:** Advisory prompt-hygiene weakness where hard runtime sandboxing and permissions already block exploitation (defense-in-depth gap).

## Finding Format

For each finding report:

- **Severity** (`Critical` | `High` | `Medium` | `Low`);
- **Boundary / Target** (exact file, tool, MCP server, subagent, or config);
- **Exploit Precondition** (who controls the input and what permissions are active);
- **Concrete Attack Path & Impact**;
- **Evidence**;
- **Remediation** (explicitly splitting *runtime control* vs. *prompt hardening*);
- **Verification Status**.

If no vulnerabilities are found, state the exact audited boundary and residual blind spots.

## Safety

Never echo real credentials, tokens, or live exfiltration URLs in findings—redact sensitive payloads. Never install packages, connect to untrusted remote MCP servers, or run destructive/networked exploits merely to prove a vulnerability without explicit user authorization and isolation.
