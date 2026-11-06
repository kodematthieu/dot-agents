# Skill, Rule, and Custom Agent Authoring

Load this when designing or reviewing `SKILL.md` bundles, global/workspace instruction files, or custom `agents/*.md` definitions for portability across models, environments, and agent harnesses.

## 1. Progressive Disclosure & Context Budgets

- **Thin always-on rules, rich on-demand skills:** Keep global/workspace instruction files compact (behavioral contract, trust boundaries, routing) well below host per-file and aggregate token caps so rules are never silently truncated.
- **`SKILL.md` sizing & output economy:** Aim for `25–50` lines in `SKILL.md`. Avoid multi-bullet `Output Contract` templates that force models to print empty `"None"` sections or ceremonial footers on small tasks; surface assumptions, skipped checks, or tables **only when load-bearing**.
- **`references/` threshold:** Split material into `references/*.md` only when a conditional reference is substantive (`~20+` lines) so on-demand loading saves tokens rather than burning a file-read round-trip for a stub.
- **Executable helpers (`scripts/`):** Encapsulate deterministic validation or multi-step checks in portable scripts when available, without assuming a specific OS or shell in prose instructions.

## 2. Routing `description` Precision

Skill and subagent `description` fields are loaded into the catalog on every turn:

- Keep `description` concise (`~40–85` words) and third-person/imperative.
- Pair **positive triggers** (*what intent or artifact activates this skill*) with **negative boundaries** (`Not for ...`) naming the sibling skill that owns adjacent tasks to prevent false-positive auto-invocation.

## 3. Model- & Environment-Agnostic Instruction Design

- **Calm, observable directives:** Prefer direct behavioral rules over habitual all-caps imperatives (`CRITICAL`, `MANDATORY`, `YOU MUST ALWAYS`); vendor prompting guides report that some reasoning-tuned models can over-trigger on aggressive phrasing, and calm specifications generalize more cleanly across model families.
- **Positive contracts over negation walls:** Pair boundaries with the affirmative behavior to use instead (e.g., *State decision-reversal conditions rather than numeric confidence floats*).
- **Context ordering:** Place reference schemas, diffs, or retrieved documents *before* active task criteria to improve long-context attention across model families.
- **Environment neutrality:** Never hardcode OS names, shell dialects, VCS tools, or host-specific tool IDs inside shared skill or agent prose; refer to capabilities generically (*read-only search tools*, *VCS diff/status*, *active host session*).

## 4. Cross-Harness Portability (`~/.agents/`)

- **Skill directory depth:** Keep skills strictly 1 level deep (`skills/<skill-name>/SKILL.md`) with lowercase-hyphenated names matching the directory so both shallow-scanning and deep-scanning Agent Skills hosts discover them identically.
- **Custom agent file layout:** Use flat `agents/<name>.md` files rather than nested subdirectories for maximum host discovery compatibility.
- **Orthogonal vs. colliding frontmatter keys:**
  - Safe orthogonal role keys (such as `mode: primary | subagent | all` alongside `mainAgent` / `subagent` booleans) can coexist when each host ignores unknown keys.
  - **Isolate colliding keys into host-native configs:** Omit `model:` from shared Markdown frontmatter when hosts disagree on schema (e.g., tier enums vs. `provider/model` IDs) so agents inherit the session model cleanly. Likewise, avoid placing host-specific tool names (`bash`, `read`, `view_file`) in shared `tools:` lists where unmapped names can stall or break another harness; enforce tool/permission restrictions in each harness's native config file instead.
