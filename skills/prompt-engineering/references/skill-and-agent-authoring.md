# Skill, Rule, and Custom Agent Authoring

Load this when designing or reviewing `SKILL.md` bundles, global/workspace `AGENTS.md` / `GEMINI.md` rules, or custom `agents/*.md` definitions—especially across OpenCode v2 and Antigravity (`agy`).

## 1. Progressive Disclosure & Context Budgets

- **Thin always-on rules, rich on-demand skills:** Keep global/workspace `AGENTS.md` / `GEMINI.md` compact (behavioral contract, trust boundaries, routing, completion standards) well below host truncation caps (e.g., Antigravity truncates single rule files above `24,000` bytes and shares a `20,000`-token aggregate rules budget).
- **`SKILL.md` sizing & output economy:** Aim for `30–60` lines in `SKILL.md`. Avoid multi-bullet `Output Contract` checklists that force models to print empty `"None"` sections or ceremonial footers on small tasks; require surfacing assumptions, skipped checks, or tables **only when load-bearing**.
- **`references/` threshold:** Split material into `references/*.md` only when a conditional reference is substantive (`~20+` lines) so on-demand loading saves tokens rather than burning a file-read tool call for a 7-line stub.
- **Executable helpers (`scripts/`):** When a skill relies on deterministic validation, parsing, or multi-step CLI checks, encapsulate them in `scripts/` and link relatively rather than describing fragile shell pipelines in prose.

## 2. Routing `description` Precision

Skill and subagent `description` fields are injected into the catalog on every turn:

- Keep `description` concise (`~40–90` words) and third-person/imperative.
- Pair **positive triggers** (*what observable user intent or artifact activates this skill*) with **negative boundaries** (`Not for ...`) naming the sibling skill that owns adjacent tasks, preventing false-positive auto-invocation and overlap.

## 3. Cross-Model Instruction Calibration

- **Avoid aggressive directives:** Frontier reasoning models (e.g., Claude Opus 4.x, Gemini 3.x/4.x) over-trigger on `CRITICAL`, `MANDATORY`, `YOU MUST ALWAYS`. Use calm, direct behavioral specifications (`Read relevant files before editing`, `Use X when...`).
- **Positive contracts over negation walls:** Pair boundaries with the affirmative action to take instead (e.g., *State decision-reversal conditions rather than numeric confidence floats*).
- **Context ordering:** Place reference schemas, diffs, or retrieved documents *before* the active evaluation criteria or task prompt to improve long-context recall.

## 4. Polyglot Compatibility (`~/.agents/` across OpenCode v2 & `agy`)

- **Skill directory depth:** Keep skills strictly 1 level deep (`skills/<skill-name>/SKILL.md`) with lowercase-hyphenated names matching the folder; OpenCode v2 recurses deeper, whereas `agy` scans strictly 1 level deep.
- **Custom agent file layout:** Use flat `agents/<name>.md` files (OpenCode v2 ignores `agents/<name>/agent.md`).
- **Orthogonal role keys in `agents/<name>.md`:** Include both OpenCode's `mode: primary | subagent | all` and Antigravity's `mainAgent: true | false` + `subagent: true | false` (`primary` $\iff$ `mainAgent: true, subagent: false`; `subagent` $\iff$ `mainAgent: false, subagent: true`).
- **Avoid breaking schema collisions in shared `agents/<name>.md`:**
  - **Omit `model:`** in shared Markdown frontmatter (`agy` accepts only `inherit | flash | pro`, whereas OpenCode v2 expects `provider/model#variant`; omitting lets both inherit the session model, with OpenCode overrides placed in `opencode.jsonc`).
  - **Never mix OpenCode tool names into `tools:`:** `agy` hangs on unmapped tool names like `bash`, `edit`, or `read` inside `tools:`. Keep `tools:` restricted to valid `agy` tool IDs (or omit) and define OpenCode v2 `permissions` in `opencode.jsonc` (working around OpenCode v2 Markdown frontmatter enforcement gaps).
