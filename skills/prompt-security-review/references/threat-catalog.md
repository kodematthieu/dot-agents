# Threat catalog

Load this when auditing prompts, skills, tools, agent workflows, repositories, or dependencies. This is a checklist of what to inspect, not evidence that any of it is present.

## Direct prompt injection

The user issues instructions that contradict trusted policy: ignoring prior rules, claiming a new role, asserting authorization the user does not have, or requesting secrets. Test with representative phrasings, including polite and technical framings.

## Indirect injection

Instructions arrive through content the agent reads: retrieved documents, web pages, issue text, code comments, file contents, tool output, or dependency documentation. Any text that reaches the model can carry an adversarial payload. Delimiters and role separation communicate intent to the model but do not make content non-executable.

## Instruction / data confusion

- Content the model should treat as data being read as policy.
- Policy text embedded inside untrusted content.
- Tool results containing instructions that redirect agent behavior.
- Retrieved documents used to justify expanded scope or permissions.

## Secret exposure

- Credentials, tokens, private keys, or personal data in prompts, examples, logs, or skill references.
- Instructions that ask the model to render environment variables, system prompt contents, or confidential records.
- Exfiltration through rendered markdown images, outbound URLs, or tool arguments.
- Error output that echoes secrets.

Prefer a scoped runtime operation over exposing a secret to the model.

## Excessive agency

- Tools that are broader than the task requires, especially write, delete, network, or credential access.
- Loops without stop conditions, budgets, or iteration limits.
- Autonomous action where the smallest sufficient architecture is a direct call or a fixed workflow.
- Approval gates that are configured but bypassable, or absent where authorization is required.

## Unsafe commands and paths

- Shell interpolation of untrusted or model-produced values.
- Path traversal, absolute paths outside the workspace, and symlink escape.
- Destructive or non-idempotent operations: recursive deletion, force pushes, migrations, bulk updates, publication.
- Unbounded timeouts, retries after writes, and operations repeated without idempotency.

## Output handling

- Model output consumed by a downstream system without schema validation.
- Output trusted as an authorization decision rather than a proposal.
- Rendering model output as executable content: HTML, markdown with embedded links or images, code.
- Unvalidated structured output treated as correct because it parsed.

## Supply chain

- Skills, plugins, or MCP servers added without review.
- Unpinned dependencies, packages installed or scripts executed during review or at runtime.
- Third-party code connected to network or filesystem access it does not need.
- HTTP skill catalogs: verify `index.json`, same-origin safe relative paths, and a changed `version` before trusting refreshed contents.

## Classification

For each finding, separate:

- the prompt-level mitigation, which is advisory;
- the runtime control that actually enforces the boundary: authorization, sandboxing, allowlists, schema validation, approval, or CI.

A hidden prompt or a prose instruction such as "do not" is not sufficient security evidence.