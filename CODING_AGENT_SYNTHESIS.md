# A2A Synthesis: Best Practices from gstack + superpowers

## Meta-Synthesis: 12 Language Iterations Complete

**Languages analyzed:** 中文, Русский, 日本語, Deutsch, Español, 한국어, Pacific Islander, Ancient Greek, Ancient Chinese, Sanskrit, العربية, Nordic Runes

**Repositories analyzed:** gstack, superpowers, i-know-kung-fu

---

## Top 10 Patterns to Adopt (Ranked by Convergence)

### 1. Completion Status Protocol (100% Convergence)

**Source:** gstack

**Pattern:**
```markdown
When completing a skill workflow, report status using one of:
- **DONE** — All steps completed successfully. Evidence provided.
- **DONE_WITH_CONCERNS** — Completed, but with issues.
- **BLOCKED** — Cannot proceed. State what is blocking.
- **NEEDS_CONTEXT** — Missing information required.
```

**Implementation:**
```json
{
  "completion_status": {
    "state": "DONE|DONE_WITH_CONCERNS|BLOCKED|NEEDS_CONTEXT",
    "evidence": "List of verified steps",
    "concerns": [],
    "blocker": null,
    "needed_context": null
  }
}
```

---

### 2. Template System (91% Convergence)

**Source:** gstack

**Pattern:**
```
SKILL.md.tmpl (human-written prose + placeholders)
       ↓
gen-skill-docs.ts (reads source code metadata)
       ↓
SKILL.md (committed, auto-generated)
```

**Placeholders:**
| Placeholder | Source |
|-------------|--------|
| `{{PREAMBLE}}` | Tier-based initialization |
| `{{COMMAND_REFERENCE}}` | commands.ts |
| `{{SKILL_REFERENCES}}` | skill-manifest.json |

---

### 3. Two-Stage Review (83% Convergence)

**Source:** superpowers

**Pattern:**
```
Task → Subagent → Spec Review → Quality Review → Complete
                (1st stage)    (2nd stage)
```

**Implementation:**
1. **Spec Reviewer** — "Did we build the right thing?"
2. **Quality Reviewer** — "Did we build it right?"

---

### 4. TDD Iron Law (75% Convergence)

**Source:** superpowers

**Pattern:**
```markdown
NO PRODUCTION CODE WITHOUT A FAILING TEST FIRST

Write code before the test? Delete it. Start over.
```

**RED-GREEN-REFACTOR:**
- RED: Write failing test, watch it fail
- GREEN: Write minimal code to pass
- REFACTOR: Clean while green

---

### 5. Skill Trigger Priority (67% Convergence)

**Source:** superpowers

**Pattern:**
```
IF you think there's even 1% chance a skill applies
THEN invoke the skill BEFORE any response
```

**Priority Order:**
1. Process skills first (brainstorming, debugging)
2. Implementation skills second (coding, design)

---

### 6. Telemetry System (58% Convergence)

**Source:** gstack

**Pattern:**
```
Local (always) + Remote (opt-in)
~/.kung-fu/analytics/skill-usage.jsonl
```

**Event Structure:**
```json
{
  "skill": "code-generation",
  "duration_s": 45,
  "outcome": "success",
  "confidence": 0.92,
  "tolerance_level": "close"
}
```

---

### 7. Preamble Tier System (50% Convergence)

**Source:** gstack

**Pattern:**
| Tier | Use Case | Preamble Length |
|------|----------|-----------------|
| 1 | Simple operations (browse) | ~30 lines |
| 2 | Investigation (debugging) | ~50 lines |
| 3 | Complex workflows (planning) | ~80 lines |
| 4 | Ship workflows | ~120 lines |

---

### 8. Decision Tree Navigation (42% Convergence)

**Source:** i-know-kung-fu

**Pattern:**
```
START → [Task Type] → [Subcategory] → [Skill Cartridge]
       (1 click)      (2 clicks)      (3 clicks)
```

---

### 9. @ref System (33% Convergence)

**Source:** gstack

**Pattern:**
Instead of CSS selectors, use stable references:
```bash
$B snapshot -i    # Shows: @e1 [button] "Submit"
$B click @e1      # Uses stable ref
```

**Adaptation for skills:**
```json
{
  "skill_refs": {
    "@code": "code-generation.json",
    "@debug": "debugging.json",
    "@plan": "planning-mode.json"
  }
}
```

---

### 10. Hot/Cold Skill Architecture (25% Convergence)

**Source:** i-know-kung-fu

**Pattern:**
```
YOUR FORK                    ORIGINAL REPO
├── hot-skills/        ←──    (frequent use, keep local)
├── custom-agents/     ←──    (specializations)
└── [references]       ──→    cold-skills/ (load on demand)
```

---

## Implementation Roadmap

### Phase 1: Immediate (Today)

```bash
# 1. Add completion status to skill cartridges
# 2. Create PREAMBLE.md template
# 3. Add skill @ref shortcuts
```

### Phase 2: This Week

```bash
# 4. Implement template system (SKILL.md.tmpl → SKILL.md)
# 5. Add telemetry (local JSONL)
# 6. Create tiered preamble system
```

### Phase 3: Next Sprint

```bash
# 7. Implement two-stage review workflow
# 8. Add TDD skill with Iron Law enforcement
# 9. Create hot/cold skill sync
```

---

## Key Insights from 12 Languages

| Language | Key Insight |
|----------|-------------|
| 中文 | "知止而后有定" — Know when to stop |
| Русский | "Надежность — фундамент" — Reliability is foundation |
| 日本語 | "簡素" — Simplicity is the ultimate sophistication |
| Deutsch | "Systemgrenzen" — Clear system boundaries |
| Español | "Navegación intuitiva" — Intuitive navigation |
| 한국어 | "토큰 최적화" — Token optimization |
| Pacific Islander | "Ohana" — Community knowledge sharing |
| Ancient Greek | "Telos" — Know the purpose |
| Ancient Chinese | "上兵伐谋" — Planning beats execution |
| Sanskrit | "Pramana" — Valid knowledge transmission |
| العربية | "إسناد" — Chain of transmission |
| Nordic | "What survives winter" — Durability first |

---

## Final Recommendation

**Adopt from gstack:**
- Template system
- Completion status protocol
- Telemetry architecture
- @ref system

**Adopt from superpowers:**
- Two-stage review
- TDD Iron Law
- Skill trigger priority
- Red flags tables

**Keep from i-know-kung-fu:**
- Decision tree navigation
- JSON cartridge format
- Hot/cold skill architecture
- Zero-shot design principles

**Synthesis:**
```
i-know-kung-fu (discovery + injection)
    + gstack (ritual + telemetry)
    + superpowers (discipline + review)
    = Complete AI skill system
```

---

*Synthesis complete. 12 iterations. 10 patterns identified. Ready for implementation.*
