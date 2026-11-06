# `~/.agents` — Portable Agent Instructions, Skills, and Custom Agents

A model-, environment-, and harness-agnostic repository of global behavioral policy (`AGENTS.md`), progressive-disclosure [Agent Skills](https://agentskills.io) (`skills/`), and read-only custom agents (`agents/`).

## Layout

```text
~/.agents/
├── AGENTS.md                  # Global Axiom^2 behavioral & epistemic contract
├── agents/
│   ├── brainstorm.md          # Primary read-only option-generation & tradeoff agent
│   └── review.md              # Read-only code/security review & test subagent
├── skills/
│   ├── axiom/                 # First-principles, systems, ontology & formal lenses
│   ├── bug-diagnosis/         # Reproduction, competing-hypothesis root cause & fix
│   ├── engineering-task/      # Scoped implementation, checkpoints & diff verification
│   ├── prompt-engineering/    # Prompt/skill/agent architecture & eval calibration
│   ├── prompt-security-review/# Injection, MCP/tool boundary & supply-chain audit
│   ├── psychoanalytic-reflection/ # Hermeneutic & socio-technical UX/system lenses
│   ├── repository-orientation/# Token-efficient codebase & CI command mapping
│   └── software-engineering-review/ # Calibrated diff, regression & sibling-site review
├── LICENSE
└── README.md
```

## Per-Harness Global Wiring

Only `~/.agents/skills/*/SKILL.md` is auto-discovered globally out of the box by Open Agent Skills hosts (such as OpenCode v2). Global instructions (`AGENTS.md`) and custom agents (`agents/*.md`) require one-time host wiring.

Using config includes and **per-file** agent symlinks keeps each harness's own config directory free for harness-specific instructions and agents:

### 1. OpenCode v2

1. Link shared custom agents (per-file, leaving `~/.config/opencode/agents/` open for OpenCode-only agents):
   ```sh
   mkdir -p ~/.config/opencode/agents
   ln -sfn ~/.agents/agents/*.md ~/.config/opencode/agents/
   ```
2. Reference `~/.agents/AGENTS.md` and enforce runtime shell approval gates in `~/.config/opencode/opencode.jsonc` (preserving `~/.config/opencode/AGENTS.md` for OpenCode-specific rules):
   ```jsonc
   {
     "instructions": ["~/.agents/AGENTS.md"],
     "permissions": [
       { "action": "skill", "resource": "*", "effect": "allow" },
       { "action": "shell", "resource": "git push*", "effect": "ask" },
       { "action": "shell", "resource": "git reset --hard*", "effect": "ask" },
       { "action": "shell", "resource": "git clean -fd*", "effect": "ask" },
       { "action": "shell", "resource": "rm -rf*", "effect": "ask" },
       { "action": "shell", "resource": "sudo*", "effect": "deny" },
       { "action": "shell", "resource": "curl*", "effect": "ask" },
       { "action": "shell", "resource": "wget*", "effect": "ask" },
       { "action": "shell", "resource": "gh *", "effect": "ask" },
       { "action": "shell", "resource": "npm publish*", "effect": "ask" }
     ]
   }
   ```

### 2. Antigravity (`agy` CLI & IDE)

1. Link shared custom agents and register `~/.agents/skills` in `~/.gemini/config/skills.json`:
   ```sh
   mkdir -p ~/.gemini/config/agents
   ln -sfn ~/.agents/agents/*.md ~/.gemini/config/agents/
   printf '{\n  "entries": [\n    { "path": "~/.agents/skills" }\n  ]\n}\n' > ~/.gemini/config/skills.json
   ```
2. Include `~/.agents/AGENTS.md` at the top of `~/.gemini/GEMINI.md` above any Antigravity-specific rules:
   ```markdown
   @[AGENTS.md](/absolute/path/to/.agents/AGENTS.md)
   ```

### 3. Workspace / Other Hosts (Claude Code, Cursor, Codex)

- **Workspace-scoped:** Clone or submodule into `<repo>/.agents/` and symlink or `@include` `.agents/AGENTS.md` from `<repo>/AGENTS.md` or `<repo>/CLAUDE.md`.
- **Claude Code global:** Symlink skills if needed (`ln -sfn ~/.agents/skills/* ~/.claude/skills/`) and `@~/.agents/AGENTS.md` from `~/.claude/CLAUDE.md`.

## License

[MIT](./LICENSE)
