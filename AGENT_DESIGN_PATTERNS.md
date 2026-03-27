# 🎨 Agent Design Patterns - The Deep Dive

> **Architectural Patterns, Reasoning Templates, and Composition Strategies**
> 
> This document provides the deep design knowledge for building sophisticated agents that compose well and perform reliably.

---

## 📐 Pattern Categories

| Category | Purpose | Complexity |
|----------|---------|------------|
| Structural | Agent organization | Simple to Complex |
| Behavioral | How agents act | Simple to Moderate |
| Reasoning | How agents think | Moderate to Complex |
| Orchestration | Multi-agent coordination | Complex |
| Integration | Platform adaptation | Simple to Moderate |

---

## 🏗️ Structural Patterns

### Pattern: Stateless Worker

**When to use**: Simple transformations, no context needed between requests.

```
┌─────────────┐
│   Input     │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  Transform  │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│   Output    │
└─────────────┘
```

**Implementation**:
```json
{
  "pattern": "stateless_worker",
  "agent_type": "quick-task",
  "memory": "none",
  "examples": [
    "JSON Formatter",
    "Timestamp Converter",
    "Regex Helper"
  ]
}
```

**Pros**: Fast, scalable, easy to test
**Cons**: No learning, no context preservation

---

### Pattern: Session-Based Agent

**When to use**: Multi-turn interactions, context matters.

```
┌─────────────┐     ┌─────────────┐
│   Input     │────▶│   Session   │
└─────────────┘     │    Memory   │
                    └──────┬──────┘
                           │
                           ▼
                    ┌─────────────┐
                    │  Processing │
                    └──────┬──────┘
                           │
                           ▼
                    ┌─────────────┐
                    │   Output    │
                    └─────────────┘
```

**Implementation**:
```json
{
  "pattern": "session_based",
  "memory": {
    "type": "conversation",
    "window": 10,
    "persistence": "session"
  },
  "context_injection": "automatic",
  "examples": [
    "Customer Support Agent",
    "Research Assistant",
    "Code Reviewer"
  ]
}
```

---

### Pattern: Hierarchical Agent

**When to use**: Complex tasks with subtasks, delegation needed.

```
        ┌─────────────────┐
        │  Orchestrator   │
        └────────┬────────┘
                 │
        ┌────────┼────────┐
        │        │        │
        ▼        ▼        ▼
    ┌───────┐┌───────┐┌───────┐
    │Agent 1││Agent 2││Agent 3│
    └───────┘└───────┘└───────┘
```

**Implementation**:
```json
{
  "pattern": "hierarchical",
  "roles": {
    "orchestrator": {
      "responsibility": "task decomposition and routing",
      "delegates_to": ["researcher", "analyst", "writer"]
    },
    "specialists": [
      {
        "name": "researcher",
        "skills": ["web_search", "data_gathering"]
      },
      {
        "name": "analyst",
        "skills": ["data_analysis", "pattern_recognition"]
      },
      {
        "name": "writer",
        "skills": ["synthesis", "formatting"]
      }
    ]
  },
  "communication": "pass_results_down"
}
```

---

### Pattern: Pipeline Agent

**When to use**: Sequential processing stages, clear flow.

```
Input ──▶ [Stage 1] ──▶ [Stage 2] ──▶ [Stage 3] ──▶ Output
           │              │              │
           ▼              ▼              ▼
        Validate      Transform      Enrich
```

**Implementation**:
```json
{
  "pattern": "pipeline",
  "stages": [
    {
      "name": "validate",
      "action": "input_validation",
      "on_failure": "reject"
    },
    {
      "name": "transform",
      "action": "core_processing",
      "on_failure": "retry"
    },
    {
      "name": "enrich",
      "action": "add_metadata",
      "on_failure": "continue_without"
    }
  ],
  "error_handling": "stage_specific"
}
```

---

## 🧠 Reasoning Patterns

### Pattern: ReAct (Reasoning + Acting)

**When to use**: Need to think and act iteratively.

```
┌─────────────────────────────────────┐
│            ReAct Loop               │
│                                     │
│  Thought ──▶ Action ──▶ Observation │
│     │                           │   │
│     └───────────────────────────┘   │
│                 │                   │
│                 ▼                   │
│              Answer                 │
└─────────────────────────────────────┘
```

**Implementation**:
```json
{
  "pattern": "react",
  "max_iterations": 10,
  "thought_template": "I need to... Because... I will...",
  "action_space": ["search", "calculate", "query", "generate"],
  "observation_parser": "extract_relevant_info",
  "termination_conditions": {
    "found_answer": true,
    "max_iterations": true,
    "stuck": true
  }
}
```

**Example Trace**:
```
Question: What's the population of the capital of France?

Thought 1: I need to find the capital of France first.
Action 1: search("capital of France")
Observation 1: Paris is the capital of France.

Thought 2: Now I need to find the population of Paris.
Action 2: search("population of Paris")
Observation 2: Paris has a population of approximately 2.1 million.

Thought 3: I have the answer.
Answer: The capital of France is Paris, with a population of approximately 2.1 million.
```

---

### Pattern: Chain of Thought (CoT)

**When to use**: Complex reasoning, step-by-step breakdown needed.

```
Question
    │
    ▼
Step 1 ──▶ Intermediate 1
    │
    ▼
Step 2 ──▶ Intermediate 2
    │
    ▼
Step 3 ──▶ Final Answer
```

**Implementation**:
```json
{
  "pattern": "chain_of_thought",
  "prompting": "explicit_steps",
  "step_markers": ["First,", "Then,", "Next,", "Finally,"],
  "verification": {
    "enabled": true,
    "verify_each_step": false,
    "verify_final_answer": true
  },
  "examples": [
    "Mathematical reasoning",
    "Logical deduction",
    "Multi-step analysis"
  ]
}
```

---

### Pattern: Tree of Thought (ToT)

**When to use**: Multiple solution paths, need exploration.

```
                Question
                    │
        ┌───────────┼───────────┐
        │           │           │
     Thought 1   Thought 2   Thought 3
        │           │           │
     Evaluate    Evaluate    Evaluate
        │           │           │
     ┌──┴──┐    ┌──┴──┐    ┌──┴──┐
     │     │    │     │    │     │
   T1.1 T1.2  T2.1 T2.2  T3.1 T3.2
     │     │    │           │
   Best  Best  ...        Best
     │     │                │
     └──┬──┘                │
        │                   │
        └─────────┬─────────┘
                  │
              Final Answer
```

**Implementation**:
```json
{
  "pattern": "tree_of_thought",
  "branching_factor": 3,
  "max_depth": 3,
  "evaluation": {
    "method": "llm_evaluation",
    "criteria": ["feasibility", "completeness", "quality"]
  },
  "search_strategy": "best_first",
  "pruning": {
    "enabled": true,
    "threshold": 0.3
  }
}
```

---

### Pattern: Reflection

**When to use**: Self-improvement needed, quality assurance.

```
┌─────────────────────────────────────┐
│         Reflection Loop             │
│                                     │
│  Generate ──▶ Critique ──▶ Refine   │
│     │                          │    │
│     └──────────────────────────┘    │
│                 │                   │
│              Accept                 │
└─────────────────────────────────────┘
```

**Implementation**:
```json
{
  "pattern": "reflection",
  "critic": {
    "model": "same_or_different",
    "criteria": ["correctness", "completeness", "clarity"],
    "style": "constructive_feedback"
  },
  "refinement": {
    "max_iterations": 3,
    "focus_areas": ["identified_issues"]
  },
  "acceptance": {
    "threshold": 0.8,
    "or_max_iterations": true
  }
}
```

---

### Pattern: Plan-and-Execute

**When to use**: Long-horizon tasks, clear planning needed.

```
┌──────────────┐     ┌──────────────┐
│    Plan      │────▶│   Execute    │
└──────────────┘     └──────┬───────┘
                            │
                     ┌──────┴───────┐
                     │              │
                  Step 1        Step 2 ...
                     │              │
                     └──────┬───────┘
                            │
                     ┌──────▼───────┐
                     │   Replan?    │
                     └──────┬───────┘
                            │
                     Yes ───┼─── No
                      │           │
                   Replan    Complete
```

**Implementation**:
```json
{
  "pattern": "plan_and_execute",
  "planner": {
    "output": "ordered_steps",
    "step_format": {
      "description": "what_to_do",
      "tool": "which_tool",
      "expected_output": "what_to_expect"
    }
  },
  "executor": {
    "mode": "sequential",
    "error_handling": "replan_on_failure"
  },
  "replanning": {
    "trigger": "step_failure_or_new_info",
    "preserve_completed": true
  }
}
```

---

## 🎭 Behavioral Patterns

### Pattern: Guard Rails

**When to use**: Safety-critical, need boundaries.

```json
{
  "pattern": "guard_rails",
  "input_guards": [
    {
      "type": "content_filter",
      "rules": ["no_pii", "no_harmful_content"]
    },
    {
      "type": "format_check",
      "schema": "input_schema.json"
    }
  ],
  "output_guards": [
    {
      "type": "content_filter",
      "rules": ["no_pii_leak", "factual_check"]
    },
    {
      "type": "format_check",
      "schema": "output_schema.json"
    }
  ],
  "on_violation": "reject_with_explanation"
}
```

---

### Pattern: Graceful Degradation

**When to use**: Reliability critical, partial results valuable.

```json
{
  "pattern": "graceful_degradation",
  "fallback_chain": [
    {
      "condition": "primary_tool_failed",
      "fallback": "cached_response"
    },
    {
      "condition": "cache_miss",
      "fallback": "simplified_response"
    },
    {
      "condition": "all_failed",
      "fallback": "error_message_with_alternatives"
    }
  ],
  "quality_levels": {
    "full": ["all_features", "full_accuracy"],
    "partial": ["core_features", "reduced_accuracy"],
    "minimal": ["basic_features", "best_effort"]
  }
}
```

---

### Pattern: Progressive Enhancement

**When to use**: Quick first response, add detail over time.

```json
{
  "pattern": "progressive_enhancement",
  "stages": [
    {
      "name": "quick_response",
      "time_budget_ms": 100,
      "output": "high_level_answer"
    },
    {
      "name": "detailed_response",
      "time_budget_ms": 1000,
      "output": "full_explanation"
    },
    {
      "name": "comprehensive_response",
      "time_budget_ms": 5000,
      "output": "examples_and_context"
    }
  ],
  "delivery": "streaming"
}
```

---

## 🎼 Orchestration Patterns

### Pattern: Swarm

**When to use**: Parallel work, no dependencies.

```
            ┌─────────────┐
            │ Coordinator │
            └──────┬──────┘
                   │
         ┌─────────┼─────────┐
         │         │         │
         ▼         ▼         ▼
     ┌───────┐ ┌───────┐ ┌───────┐
     │Agent 1│ │Agent 2│ │Agent 3│
     └───┬───┘ └───┬───┘ └───┬───┘
         │         │         │
         └─────────┼─────────┘
                   │
                   ▼
            ┌─────────────┐
            │  Aggregate  │
            └─────────────┘
```

**Implementation**:
```json
{
  "pattern": "swarm",
  "coordinator": {
    "task_distribution": "broadcast_or_partition",
    "agent_pool_size": 5
  },
  "agents": {
    "type": "homogeneous_or_heterogeneous",
    "specializations": ["research", "analysis", "writing"]
  },
  "aggregation": {
    "method": "merge_or_vote_or_rank",
    "conflict_resolution": "best_score"
  }
}
```

---

### Pattern: Debate

**When to use**: Need multiple perspectives, consensus building.

```
Position A ◀──────────────▶ Position B
    │                           │
    │        Moderator          │
    │           │               │
    │     ┌─────┴─────┐         │
    └────▶│ Synthesis │◀────────┘
          └─────┬─────┘
                │
                ▼
           Consensus
```

**Implementation**:
```json
{
  "pattern": "debate",
  "participants": [
    {
      "role": "proponent",
      "stance": "support_position_a"
    },
    {
      "role": "opponent",
      "stance": "support_position_b"
    }
  ],
  "moderator": {
    "turns": 3,
    "focus": "identify_common_ground"
  },
  "synthesis": {
    "method": "weighted_combination",
    "weights": "argument_strength"
  }
}
```

---

### Pattern: Consensus

**When to use**: Multiple agents voting on outcomes.

```json
{
  "pattern": "consensus",
  "voting": {
    "method": "majority_or_unanimous_or_weighted",
    "agents": 5,
    "tie_breaker": "highest_confidence"
  },
  "confidence_threshold": 0.7,
  "on_no_consensus": "escalate_or_retry"
}
```

---

## 🔌 Integration Patterns

### Pattern: Adapter

**When to use**: Platform-specific requirements.

```json
{
  "pattern": "adapter",
  "core_agent": "universal_specification.json",
  "adapters": {
    "minimax": {
      "input_transform": "minimax_input_mapper",
      "output_transform": "minimax_output_mapper"
    },
    "claude_mcp": {
      "input_transform": "mcp_input_mapper",
      "output_transform": "mcp_output_mapper"
    },
    "openai": {
      "input_transform": "openai_input_mapper",
      "output_transform": "openai_output_mapper"
    }
  }
}
```

---

### Pattern: Facade

**When to use**: Simplify complex agent for platform.

```json
{
  "pattern": "facade",
  "internal": {
    "complexity": "high",
    "sub_agents": 5,
    "orchestration": "hierarchical"
  },
  "external": {
    "complexity": "simple",
    "interface": "single_endpoint",
    "documentation": "simplified"
  }
}
```

---

## 📊 Pattern Selection Guide

| Task Type | Recommended Pattern | Reason |
|-----------|---------------------|--------|
| Simple transformation | Stateless Worker | No context needed |
| Multi-turn chat | Session-Based | Context matters |
| Complex analysis | ReAct | Iterative discovery |
| Math/logic problems | Chain of Thought | Step-by-step reasoning |
| Creative exploration | Tree of Thought | Multiple paths |
| Quality-critical | Reflection | Self-improvement |
| Long tasks | Plan-and-Execute | Clear planning |
| Parallel work | Swarm | Speed through concurrency |
| Decision making | Debate/Consensus | Multiple perspectives |

---

## 🔄 Pattern Composition

Patterns can be combined:

```
Plan-and-Execute + ReAct + Reflection
     │
     ├── Plan: Generate steps
     │
     ├── Execute each step with ReAct
     │         │
     │         ├── Think → Act → Observe
     │         └── Repeat until step done
     │
     └── Reflect on final result
               │
               └── Improve if needed
```

**Composition Template**:
```json
{
  "composition": {
    "outer": "plan_and_execute",
    "middle": "react",
    "inner": "reflection",
    "integration_points": {
      "reflection_after": "each_plan_step",
      "replan_trigger": "reflection_suggests"
    }
  }
}
```

---

## 🎓 Anti-Patterns to Avoid

### Anti-Pattern: God Agent

❌ One agent does everything

```
┌────────────────────────────┐
│        GOD AGENT           │
│                            │
│  - Handles all inputs      │
│  - Does all processing     │
│  - Manages all state       │
│  - Knows everything        │
└────────────────────────────┘
```

**Why it fails**: Unmaintainable, poor performance, hard to debug

**Solution**: Decompose into specialized agents

---

### Anti-Pattern: Infinite Loop

❌ Agent keeps thinking without progress

**Symptoms**:
- Same thought repeated
- No termination condition
- Token exhaustion

**Solution**:
```json
{
  "safeguards": {
    "max_iterations": 10,
    "progress_check": {
      "interval": 3,
      "criteria": "new_information_generated"
    },
    "forced_termination": {
      "condition": "no_progress_after_n_steps",
      "action": "best_effort_answer"
    }
  }
}
```

---

### Anti-Pattern: Context Explosion

❌ Accumulating too much context

**Symptoms**:
- Slow responses
- Token limit errors
- Decreased quality

**Solution**:
```json
{
  "context_management": {
    "strategy": "sliding_window",
    "max_tokens": 4000,
    "summarization": {
      "trigger": "token_threshold",
      "method": "extract_key_points"
    }
  }
}
```

---

*Last Updated: March 28, 2026 - Design patterns for sophisticated agent architectures*
