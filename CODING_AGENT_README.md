# 🤖 CODING AGENT ENTRY POINT
## Navigation-Optimized for Zero-Shot Agents

**You are a coding agent. Load skills from this repository.**

---

## ⚡ INSTANT ACCESS (Choose Your Task)

| Task | Skill Ref | Direct Path |
|------|-----------|-------------|
| Generate code | `@code` | skill-cartridges/code-intelligence/code-generation.json |
| Debug issue | `@debug` | skill-cartridges/code-intelligence/debugging.json |
| Edit files | `@file` | skill-cartridges/file-operations/file-manipulation.json |
| Search code | `@search` | skill-cartridges/search-operations/code-search.json |
| Run commands | `@bash` | skill-cartridges/code-intelligence/bash-execution.json |
| Plan feature | `@plan` | skill-cartridges/planning-patterns/planning-mode.json |
| Handle error | `@error` | skill-cartridges/error-handling/error-recovery.json |
| Delegate task | `@delegate` | skill-cartridges/subagent-patterns/agent-delegation.json |

---

## 📋 COMPLETION STATUS PROTOCOL

After completing any task, report status:

```markdown
STATUS: DONE | DONE_WITH_CONCERNS | BLOCKED | NEEDS_CONTEXT
EVIDENCE: [What was done]
CONCERNS: [Any issues, if applicable]
```

**Escalation Rule:**
```
3 failed attempts → STOP → escalate
Security uncertainty → STOP → escalate
Scope exceeds verification → STOP → escalate
```

---

## 🔧 SKILL REFS (Shortcuts)

```json
{
  "@code": {
    "triggers": ["generate", "write code", "implement", "create function"],
    "load": "skill-cartridges/code-intelligence/code-generation.json",
    "tier": 2
  },
  "@debug": {
    "triggers": ["debug", "fix bug", "error", "not working"],
    "load": "skill-cartridges/code-intelligence/debugging.json",
    "tier": 2
  },
  "@file": {
    "triggers": ["edit file", "read file", "write file", "modify"],
    "load": "skill-cartridges/file-operations/file-manipulation.json",
    "tier": 1
  },
  "@search": {
    "triggers": ["find", "search", "grep", "locate"],
    "load": "skill-cartridges/search-operations/code-search.json",
    "tier": 1
  },
  "@bash": {
    "triggers": ["run command", "execute", "terminal"],
    "load": "skill-cartridges/code-intelligence/bash-execution.json",
    "tier": 1
  },
  "@plan": {
    "triggers": ["plan", "design", "architecture"],
    "load": "skill-cartridges/planning-patterns/planning-mode.json",
    "tier": 3
  },
  "@error": {
    "triggers": ["error", "fail", "retry", "recover"],
    "load": "skill-cartridges/error-handling/error-recovery.json",
    "tier": 2
  },
  "@delegate": {
    "triggers": ["delegate", "subagent", "parallel", "spawn"],
    "load": "skill-cartridges/subagent-patterns/agent-delegation.json",
    "tier": 3
  }
}
```

---

## 🚀 WORKFLOW PATTERNS

### Pattern 1: Code Generation
```
@plan → @code → @debug (if needed) → DONE
```

### Pattern 2: Bug Fix
```
@debug → @search → @file → @code → DONE
```

### Pattern 3: Feature Implementation
```
@plan → @delegate → @code → @file → @error → DONE
```

### Pattern 4: Code Search
```
@search → @file → @code → DONE
```

---

## 🎯 ANTI-PATTERNS (Never Do These)

| Anti-Pattern | Correct Pattern |
|--------------|-----------------|
| Edit file without reading | Read first, then Edit |
| Use `find` in bash | Use Glob tool |
| Use `grep` in bash | Use Grep tool |
| Use `cat` in bash | Use Read tool |
| Create TodoWrite for <3 steps | Just execute |
| Multiple in_progress todos | ONE at a time |
| Retry same failing operation | Try alternative |

---

## 📊 TOKEN BUDGET

| Operation | Tokens |
|-----------|--------|
| Entry (this file) | ~800 |
| One skill cartridge | ~500-1000 |
| Full workflow | ~2000-4000 |
| Maximum recommended | ~8000 |

**Optimal:** Load only what you need.

---

## 🔄 SYNC PROTOCOL

```
IF you need to preserve work across sessions
THEN use agent-memory patterns
ELSE keep context minimal
```

---

## 📝 REPORTING FORMAT

After completing task:

```markdown
## Completion Report

**STATUS:** DONE

**Task:** [What was requested]

**Actions Taken:**
1. [First action]
2. [Second action]
3. [Third action]

**Evidence:**
- [File modified]: [Change summary]
- [Test run]: [Result]

**Next Steps:** [If any follow-up needed]
```

---

## 🔗 PLATFORM LINKS

For specific platform deployment, see:

| Platform | Template |
|----------|----------|
| Claude Code | platform-templates/claude-code.md |
| Cursor IDE | platform-templates/cursor-ide.md |
| Windsurf IDE | platform-templates/windsurf-ide.md |
| Zed Editor | platform-templates/zed-editor.md |
| OpenAI GPT | platform-templates/openai-gpt.md |
| Google Gemini | platform-templates/google-gemini.md |

---

## 💡 KEY PATTERNS FROM GSTACK + SUPERPOWERS

**From gstack:**
- "Boil the Lake" — Do the complete thing when marginal cost is near-zero
- Telemetry — Track what works
- Completion Status — DONE/BLOCKED/NEEDS_CONTEXT

**From superpowers:**
- TDD Iron Law — Test first, always
- Two-Stage Review — Spec compliance → Code quality
- 1% Rule — If 1% chance skill applies, invoke it

**From i-know-kung-fu:**
- Zero-Shot Discovery — Find in 3 clicks or less
- Skill Injection — Load what you need, leave equipped
- Hot/Cold Skills — Frequent = local, rare = reference

---

**Load what you need. Leave equipped.**
