# Claude Code Bridge Rules

Purpose
- Standard integration pattern when this framework runs alongside Claude Code (with or without ClaudeKit).
- Clean IP separation: this framework stays independent; `.claude/` stays independent.
- Neither system contains content from the other; a thin bridge layer connects them at project level.

When to apply
- If the project uses Claude Code as its AI CLI tool.
- If `.claude/` directory exists in the project root.

---

## 1) Architecture: Bridge Pattern

```
THIS FRAMEWORK (portable, tool-agnostic)     BRIDGE (project glue)           CLAUDE CODE RUNTIME (.claude/)
agent-framework/                         ←── CLAUDE.md + thin redirects ──→  .claude/hooks, agents, skills
```

- Framework files: ZERO references to `.claude/` internals.
- `.claude/` files: ZERO copies of framework content.
- Bridge: 3-5 small files that point from one to the other.

---

## 2) Bridge files to create

### A) CLAUDE.md (project root)

Rewrite to route primary workflow to the framework:

```markdown
# CLAUDE.md

## Workflows
- **Primary workflow:** `./agent-framework/_meta/Rules/Agent_Rules.md`
- Development rules: `./.claude/rules/development-rules.md`
- And other CK workflows: `./.claude/rules/*`

## Key Rule
When Agent_Rules.md and .claude/rules/ conflict, Agent_Rules.md takes precedence
for process/methodology decisions. .claude/rules/ takes precedence for
runtime/tooling decisions (hooks, agents, skills, commits).
```

### B) .claude/rules/development-rules.md (thin redirect)

Keep core principles inline (hooks read this file at runtime and inject into every prompt). Add pointer to authoritative source.

```markdown
# Development Rules (Bridge)

> **Authoritative process rules:** `agent-framework/_meta/Rules/Agent_Rules.md`
> **Coding conventions:** `agent-framework/_meta/Rules/extensions/ext_coding_conventions.md`

## Core Principles (kept inline for hook injection)
- **YAGNI** - You Aren't Gonna Need It
- **KISS** - Keep It Simple, Stupid
- **DRY** - Don't Repeat Yourself

For all process rules (task routing, grounding, quality gates, change review),
read the authoritative sources above.
```

### C) .claude/rules/primary-workflow.md (thin redirect)

```markdown
# Primary Workflow (Bridge)

> **Authoritative source:** `agent-framework/_meta/Rules/Agent_Rules.md`

This framework uses a gated pipeline (Scope → Problem → Requirements → Architecture → Detailed Design)
with 10 task-type routing modules. See Agent_Rules.md for the full routing table.
```

### D) .claude/rules/documentation-management.md (thin redirect)

```markdown
# Documentation Management (Bridge)

> **How to update docs:** `agent-framework/_meta/Rules/rules/G_docs_histories_update.md`
> **Doc structure guide:** `agent-framework/_meta/README/How_to_use.md`

All project documentation lives in `agent-framework/`.
```

### E) AGENTS.md (if OpenCode is also used)

Update workflows section to point to `agent-framework/`.

### F) .mcp.json (project root)

Create `.mcp.json` at project root with MCP servers required by A_global.md MCP Tool Activation Rules.
API keys are left empty — user fills them in after setup.

```json
{
  "mcpServers": {
    "microsoft-learn": {
      "type": "http",
      "url": "https://learn.microsoft.com/api/mcp"
    },
    "context7": {
      "type": "http",
      "url": "https://mcp.context7.com/mcp",
      "headers": {
        "CONTEXT7_API_KEY": ""
      }
    },
    "sequential-thinking": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-sequential-thinking"]
    },
    "playwright": {
      "command": "npx",
      "args": ["-y", "@anthropic-ai/mcp-server-playwright"]
    },
    "firecrawl": {
      "command": "npx",
      "args": ["-y", "firecrawl-mcp"],
      "env": {
        "FIRECRAWL_API_KEY": ""
      }
    }
  }
}
```

**Notes:**
- `context7` and `firecrawl` require API keys — user must fill `CONTEXT7_API_KEY` and `FIRECRAWL_API_KEY` after setup.
- `sequential-thinking`, `playwright`, `microsoft-learn` work without keys.
- If `.mcp.json` already exists, merge new servers into it (do not overwrite existing entries).

---

## 3) What NOT to bridge (keep separate)

These `.claude/rules/` files are runtime/tooling specific and should NOT be redirected:

| File | Reason |
|------|--------|
| `orchestration-protocol.md` | Subagent delegation patterns — no equivalent in this framework |
| `team-coordination-rules.md` | Team mode coordination — no equivalent in this framework |

---

## 4) Precedence rules

| Decision type | Who wins | Example |
|---------------|----------|---------|
| Process & methodology | Agent_Rules.md | Task routing, quality gates, change review, grounding |
| Runtime & tooling | .claude/rules/ | Hook behavior, agent delegation, commit format, file naming |
| Conflict | Agent_Rules.md | If both define different behavior for the same decision |

---

## 5) Confirmation Gate Hook (optional, recommended)

Enforces Agent_Rules.md Section 14 (Understanding Confirmation Gate) at system level.
The agent cannot Edit/Write files unless a confirmation state exists.

### How it works

```
User request → Agent runs Section 14 gate → User confirms → Agent writes state file
             → Agent calls Edit/Write → PreToolUse hook checks state file
             → Missing/expired → BLOCK + feedback to agent
             → Valid → ALLOW
```

### F) .claude/hooks/confirmation-gate.sh

```bash
#!/bin/bash
# PreToolUse hook: enforce Section 14 Confirmation Gate
# Blocks Edit/Write if confirmation state is missing or expired.
# State file is written by the agent after user confirms an approach.

STATE_FILE="$CLAUDE_PROJECT_DIR/.claude/.confirmation_state"
MAX_AGE=1800  # 30 minutes

# No state file → block
if [ ! -f "$STATE_FILE" ]; then
  echo "Section 14 Confirmation Gate: no confirmation found. Restate understanding, propose recommendations with success estimates, and wait for user to select an approach before editing." >&2
  exit 2
fi

# Check expiry (cross-platform: try GNU date, then BSD stat)
STATE_TIME=$(date -r "$STATE_FILE" +%s 2>/dev/null || stat -c %Y "$STATE_FILE" 2>/dev/null)
NOW=$(date +%s)
AGE=$((NOW - STATE_TIME))

if [ "$AGE" -gt "$MAX_AGE" ]; then
  echo "Section 14 Confirmation Gate: confirmation expired (${AGE}s ago, max ${MAX_AGE}s). Re-confirm with user before proceeding." >&2
  exit 2
fi

exit 0
```

### G) .claude/settings.json entry (merge into existing)

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Edit|Write|MultiEdit|NotebookEdit",
        "hooks": [
          {
            "type": "command",
            "command": "\"$CLAUDE_PROJECT_DIR\"/.claude/hooks/confirmation-gate.sh",
            "timeout": 5,
            "statusMessage": "Checking confirmation gate..."
          }
        ]
      }
    ]
  }
}
```

### H) Agent instructions for state file

When the agent completes Section 14 gate (user selects approach + says "proceed"), the agent MUST:

1. Create/overwrite `.claude/.confirmation_state` with:
```
timestamp: <ISO 8601>
task: <1-line summary of confirmed task>
approach: <selected approach>
```

2. The file's modification time is what the hook checks — content is for audit/debugging only.

3. After task completion, the agent SHOULD delete the state file so the next task requires fresh confirmation.

### Notes

- This hook is OPTIONAL. The framework works without it (soft enforcement via markdown rules).
- With the hook, enforcement is hard: the agent physically cannot edit files without confirmation.
- The 30-minute expiry prevents stale confirmations from auto-approving unrelated tasks.
- `.confirmation_state` should be added to `.gitignore` (runtime artifact, not source).

---

## 6) Deprecated folder cleanup

If ClaudeKit initialized a `./docs/` folder at project root with files like:
- `project-overview-pdr.md`, `code-standards.md`, `codebase-summary.md`, etc.

These are superseded by `agent-framework/` and should be deleted to avoid confusion.

---

## 6) Verification checklist

After setting up the bridge, verify:
- [ ] `CLAUDE.md` points to `agent-framework/_meta/Rules/Agent_Rules.md`
- [ ] `.claude/rules/development-rules.md` contains redirect + keeps YAGNI/KISS/DRY inline
- [ ] `.claude/rules/primary-workflow.md` contains redirect
- [ ] `.claude/rules/documentation-management.md` contains redirect
- [ ] Old `./docs/` folder is deleted or .gitignored
- [ ] CK hooks still work (start new session, check rules injection)
- [ ] (If Section 5 enabled) `.claude/hooks/confirmation-gate.sh` exists and is executable
- [ ] (If Section 5 enabled) `.claude/settings.json` contains PreToolUse hook for Edit|Write
- [ ] (If Section 5 enabled) `.claude/.confirmation_state` is in `.gitignore`
