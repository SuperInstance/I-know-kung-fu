# Agent Builder Guide

> **Comprehensive guide for creating new agent specifications. From idea to deployment.**

---

## 🚀 Overview

This guide teaches you how to create professional agent specifications that can be:
- Used by AI systems for zero-shot intelligence
- Deployed to multiple platforms (MiniMax, Claude MCP, MindStudio, etc.)
- Monetized through various channels

---

## 📋 Table of Contents

1. [Agent Anatomy](#agent-anatomy)
2. [Design Process](#design-process)
3. [Template System](#template-system)
4. [Skill Patterns](#skill-patterns)
5. [Configuration Standards](#configuration-standards)
6. [Platform Adaptation](#platform-adaptation)
7. [Testing & Validation](#testing--validation)
8. [Monetization Setup](#monetization-setup)

---

## 🧬 Agent Anatomy

Every agent specification has these core components:

### 1. README.md (Required)

```markdown
# [Agent Name]

## Overview
One-paragraph description of what the agent does and when to use it.

## Core Capabilities
| Capability | Description |
|------------|-------------|
| [Capability 1] | [What it does] |
| [Capability 2] | [What it does] |

## Skills
### Primary Skills
1. **[Skill Name]** - [Description]
2. **[Skill Name]** - [Description]

### Secondary Skills
- [Skill 1]
- [Skill 2]

## Use Cases
1. **[Use Case]** - [Description]
2. **[Use Case]** - [Description]

## Example Interactions
### [Scenario 1]
```
User: [Example input]
Agent: [Example output with reasoning]
```

## Configuration
```json
{
  "agent_type": "[type]",
  "[key]": "[value]"
}
```

## Performance Characteristics
| Metric | Value |
|--------|-------|
| [Metric] | [Value] |

## Monetization Strategy
### Pricing Tiers
- **Basic**: $[price]/[unit]
- **Pro**: $[price]/[unit]
- **Enterprise**: $[price]/[unit]

## Related Agents
- `related-agent-1/` - [How it relates]
- `related-agent-2/` - [How it relates]
```

### 2. schema.json (Required)

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "[Agent Name]",
  "description": "[Agent description]",
  "type": "object",
  "properties": {
    "agent_type": {
      "type": "string",
      "const": "[type]",
      "description": "Agent type identifier"
    },
    "inputs": {
      "type": "object",
      "properties": {
        "[input_name]": {
          "type": "[type]",
          "description": "[Description]",
          "required": true
        }
      },
      "required": ["[input_name]"]
    },
    "outputs": {
      "type": "object",
      "properties": {
        "[output_name]": {
          "type": "[type]",
          "description": "[Description]"
        }
      }
    },
    "configuration": {
      "type": "object",
      "properties": {
        "[config_key]": {
          "type": "[type]",
          "default": "[default_value]",
          "description": "[Description]"
        }
      }
    }
  }
}
```

### 3. config.json (Platform-Specific)

```json
{
  "agent": {
    "name": "[Agent Name]",
    "version": "1.0.0",
    "description": "[Description]",
    "author": "[Author]"
  },
  "model": {
    "type": "[model_type]",
    "temperature": 0.7,
    "max_tokens": 2000
  },
  "tools": [
    {
      "name": "[tool_name]",
      "description": "[Description]",
      "parameters": {}
    }
  ],
  "prompts": {
    "system": "[System prompt template]",
    "user": "[User prompt template]"
  }
}
```

---

## 🔄 Design Process

### Step 1: Define Purpose (5 minutes)

Answer these questions:

```
1. What specific problem does this agent solve?
   → [One sentence answer]

2. Who is the target user?
   → [Developer, Business User, Consumer, etc.]

3. What is the input format?
   → [Text, JSON, File, API call, etc.]

4. What is the output format?
   → [Text, JSON, File, Action, etc.]

5. What complexity level?
   → [Simple/Moderate/Complex/Enterprise]
```

### Step 2: Identify Skills (10 minutes)

Map out the required skills:

```
PRIMARY SKILLS (2-5):
1. ______________ - ______________________
2. ______________ - ______________________
3. ______________ - ______________________

SECONDARY SKILLS (2-5):
- ______________
- ______________
- ______________
```

### Step 3: Design Configuration (10 minutes)

```json
{
  "agent_type": "[unique_identifier]",
  "complexity": "[simple|moderate|complex|enterprise]",
  "execution_mode": "[synchronous|asynchronous|streaming]",
  "requires_tools": [true|false],
  "requires_memory": [true|false],
  "requires_knowledge": [true|false],
  
  "inputs": {
    "[input_1]": { "type": "[type]", "required": [true|false] }
  },
  
  "outputs": {
    "[output_1]": { "type": "[type]" }
  },
  
  "parameters": {
    "[param_1]": { "type": "[type]", "default": "[value]" }
  }
}
```

### Step 4: Create Examples (15 minutes)

Write 3-5 realistic examples:

```
EXAMPLE 1: [Simple case]
Input: "..."
Output: "..."
Reasoning: "..."

EXAMPLE 2: [Moderate case]
Input: "..."
Output: "..."
Reasoning: "..."

EXAMPLE 3: [Edge case]
Input: "..."
Output: "..."
Reasoning: "..."

EXAMPLE 4: [Error case]
Input: "..."
Output: "..."
Error handling: "..."
```

### Step 5: Set Pricing (5 minutes)

```markdown
PRICING TIERS:
- Basic: $___/___ (includes: ___)
- Pro: $___/___ (includes: ___)
- Enterprise: $___/___ (includes: ___)

TARGET MARKETS:
1. ______________
2. ______________
3. ______________
```

---

## 📝 Template System

### Quick Task Agent Template

```markdown
# [Tool Name]

## Overview
[One-line description of what this tool does]

## Input → Output
[Input format] → [Output format]

## Usage
```
[Example usage]
```

## Configuration
```json
{
  "agent_type": "quick-task",
  "tool_name": "[name]",
  "input_format": "[format]",
  "output_format": "[format]"
}
```

## Error Handling
- [Error case 1]: [How handled]
- [Error case 2]: [How handled]
```

### Reasoning Agent Template

```markdown
# [Reasoning Agent Name]

## Overview
[What reasoning pattern this agent uses]

## Reasoning Process
1. [Step 1]
2. [Step 2]
3. [Step 3]

## When To Use
- [Scenario 1]
- [Scenario 2]

## When NOT To Use
- [Scenario 1]
- [Scenario 2]

## Configuration
```json
{
  "agent_type": "reasoning",
  "pattern": "[pattern_name]",
  "max_iterations": [number],
  "verification": [true|false]
}
```

## Comparison with Similar Agents
| Aspect | This Agent | Alternative |
|--------|------------|-------------|
| [Aspect] | [Value] | [Value] |
```

### Multi-Agent Template

```markdown
# [Orchestration Agent Name]

## Overview
[How this agent coordinates multiple agents]

## Agent Roles
| Role | Purpose | Agent Type |
|------|---------|------------|
| [Role 1] | [Purpose] | [Type] |
| [Role 2] | [Purpose] | [Type] |

## Coordination Pattern
[Diagram or description of how agents interact]

## Configuration
```json
{
  "agent_type": "orchestration",
  "coordination_style": "[style]",
  "agent_pool": [number],
  "communication_protocol": "[protocol]"
}
```

## Scaling Considerations
- [Consideration 1]
- [Consideration 2]
```

---

## 🎯 Skill Patterns

### Pattern 1: Input Validation

```json
{
  "skill": "input_validation",
  "implementation": {
    "check_type": true,
    "check_format": true,
    "check_range": true,
    "sanitize": true,
    "on_failure": "reject_with_message"
  }
}
```

### Pattern 2: Progress Tracking

```json
{
  "skill": "progress_tracking",
  "implementation": {
    "checkpoints": ["start", "25%", "50%", "75%", "complete"],
    "callback_url": "optional",
    "timeout_per_checkpoint": 60
  }
}
```

### Pattern 3: Error Recovery

```json
{
  "skill": "error_recovery",
  "implementation": {
    "retry_count": 3,
    "backoff_strategy": "exponential",
    "fallback_behavior": "graceful_degradation",
    "error_categories": {
      "transient": "retry",
      "permanent": "fail_fast",
      "unknown": "log_and_retry"
    }
  }
}
```

### Pattern 4: Caching

```json
{
  "skill": "caching",
  "implementation": {
    "enabled": true,
    "ttl_seconds": 3600,
    "max_entries": 1000,
    "key_strategy": "content_hash",
    "eviction_policy": "lru"
  }
}
```

### Pattern 5: Rate Limiting

```json
{
  "skill": "rate_limiting",
  "implementation": {
    "enabled": true,
    "requests_per_minute": 60,
    "burst_allowance": 10,
    "strategy": "token_bucket",
    "on_limit_exceeded": "queue"
  }
}
```

### Pattern 6: Output Formatting

```json
{
  "skill": "output_formatting",
  "implementation": {
    "format": "json",
    "schema_validation": true,
    "pretty_print": false,
    "include_metadata": true,
    "null_handling": "omit"
  }
}
```

---

## ⚙️ Configuration Standards

### Required Fields

```json
{
  "agent_type": "string (required)",
  "version": "semver (required)",
  "description": "string (required)",
  "inputs": "object (required)",
  "outputs": "object (required)"
}
```

### Optional Fields

```json
{
  "author": "string",
  "license": "string",
  "repository": "url",
  "documentation": "url",
  "examples": "array",
  "dependencies": "object",
  "environment_variables": "array"
}
```

### Performance Configuration

```json
{
  "performance": {
    "timeout_seconds": 30,
    "max_retries": 3,
    "memory_limit_mb": 512,
    "cpu_limit": "1",
    "concurrency_limit": 10
  }
}
```

### Security Configuration

```json
{
  "security": {
    "input_sanitization": true,
    "output_filtering": true,
    "audit_logging": true,
    "pii_detection": true,
    "rate_limiting": {
      "enabled": true,
      "requests_per_minute": 60
    }
  }
}
```

---

## 🌐 Platform Adaptation

### MiniMax Experts

```json
{
  "platform": "minimax",
  "expert_config": {
    "name": "[Expert Name]",
    "description": "[2-3 sentences]",
    "category": "[Category]",
    "skills": ["[Skill 1]", "[Skill 2]"],
    "pricing": {
      "credits_per_use": 1
    },
    "example_interactions": [
      {
        "user": "[Input]",
        "expert": "[Output]"
      }
    ]
  }
}
```

### Claude MCP

```json
{
  "platform": "claude-mcp",
  "mcp_config": {
    "name": "[Server Name]",
    "version": "1.0.0",
    "tools": [
      {
        "name": "[tool_name]",
        "description": "[Description]",
        "inputSchema": {
          "type": "object",
          "properties": {}
        }
      }
    ],
    "resources": [],
    "prompts": []
  }
}
```

### MindStudio

```json
{
  "platform": "mindstudio",
  "workflow": {
    "name": "[Workflow Name]",
    "trigger": {
      "type": "[webhook|schedule|manual]"
    },
    "nodes": [
      {
        "type": "ai",
        "model": "[model_name]",
        "prompt": "[Prompt template]"
      }
    ],
    "output": {
      "type": "[response|webhook|file]"
    }
  }
}
```

### Skills.sh

```markdown
# [Skill Name]

> [One-line description]

## Purpose
[Detailed purpose]

## Instructions
1. [Step 1]
2. [Step 2]

## Examples
### Example 1
Input: [Input]
Output: [Output]

## Requirements
- [Requirement 1]
- [Requirement 2]
```

---

## 🧪 Testing & Validation

### Test Suite Structure

```
tests/
├── unit/
│   ├── test_inputs.json
│   ├── test_outputs.json
│   └── test_edge_cases.json
├── integration/
│   └── test_workflow.json
└── performance/
    └── benchmarks.json
```

### Test Case Format

```json
{
  "test_name": "[Test Name]",
  "description": "[What is being tested]",
  "input": {
    "[field]": "[value]"
  },
  "expected_output": {
    "[field]": "[value]"
  },
  "validation": {
    "type": "[exact|regex|schema|custom]",
    "criteria": "[Criteria]"
  },
  "timeout_seconds": 30
}
```

### Validation Checklist

```markdown
## Pre-Release Checklist

### Functionality
- [ ] All test cases pass
- [ ] Edge cases handled
- [ ] Error messages are clear
- [ ] Performance meets targets

### Documentation
- [ ] README is complete
- [ ] Examples are accurate
- [ ] Configuration is documented
- [ ] Related agents are linked

### Platform Compatibility
- [ ] MiniMax schema valid
- [ ] MCP config valid
- [ ] MindStudio workflow valid
- [ ] Skills.sh format correct

### Security
- [ ] Input sanitization in place
- [ ] No hardcoded secrets
- [ ] Rate limiting configured
- [ ] Audit logging enabled

### Monetization
- [ ] Pricing tiers defined
- [ ] Target markets identified
- [ ] Value proposition clear
```

---

## 💰 Monetization Setup

### Pricing Strategies

#### Usage-Based
```json
{
  "pricing_model": "usage",
  "tiers": {
    "basic": {
      "price_per_unit": 0.05,
      "unit": "request",
      "includes": ["basic features"]
    },
    "pro": {
      "price_per_unit": 0.15,
      "unit": "request",
      "includes": ["basic features", "advanced features", "priority support"]
    }
  }
}
```

#### Subscription
```json
{
  "pricing_model": "subscription",
  "plans": {
    "starter": {
      "monthly_price": 29,
      "requests_per_month": 1000
    },
    "professional": {
      "monthly_price": 99,
      "requests_per_month": 10000
    },
    "enterprise": {
      "monthly_price": "custom",
      "requests_per_month": "unlimited"
    }
  }
}
```

#### Revenue Share
```json
{
  "pricing_model": "revenue_share",
  "percentage": 20,
  "minimum_payout": 50,
  "payment_schedule": "monthly"
}
```

### Market Positioning

```markdown
## Target Markets
1. **[Market 1]**: [Why they need this]
2. **[Market 2]**: [Why they need this]
3. **[Market 3]**: [Why they need this]

## Competitive Advantage
- [Advantage 1]
- [Advantage 2]
- [Advantage 3]

## Revenue Potential
- Conservative: $[amount]/month
- Moderate: $[amount]/month
- Optimistic: $[amount]/month
```

---

## 📚 Examples

### Example: Building a Translation Agent

```markdown
# Translation Agent

## Overview
Multi-language translation agent with context awareness and tone preservation.

## Design Decisions
1. **Input**: Text + source language + target language + tone
2. **Output**: Translated text + confidence score + alternatives
3. **Complexity**: Moderate (requires context understanding)
4. **Skills**: Language detection, context preservation, tone matching

## Configuration
```json
{
  "agent_type": "translation",
  "supported_languages": ["en", "es", "fr", "de", "ja", "zh", "ko"],
  "tone_preservation": true,
  "context_window": 500,
  "alternatives_count": 3
}
```

## Platform Deployment
- MiniMax: Language expert
- MCP: Translation server
- MindStudio: Translation workflow
```

### Example: Building a Code Review Agent

```markdown
# Code Review Agent

## Overview
Automated code review focusing on quality, security, and best practices.

## Design Decisions
1. **Input**: Code + language + review depth
2. **Output**: Issues + suggestions + score
3. **Complexity**: Moderate-Complex
4. **Skills**: Pattern detection, security scanning, best practices

## Configuration
```json
{
  "agent_type": "code-review",
  "languages": ["python", "javascript", "typescript", "java", "go"],
  "check_categories": ["security", "performance", "maintainability", "style"],
  "severity_levels": ["critical", "major", "minor", "info"]
}
```

## Pricing
- Basic: $0.10/review (basic checks)
- Pro: $0.25/review (all checks + suggestions)
- Enterprise: $0.50/review (custom rules + CI/CD integration)
```

---

## 🎓 Best Practices

### Do's
- ✅ Write clear, one-sentence descriptions
- ✅ Include realistic examples
- ✅ Define clear input/output schemas
- ✅ Handle errors gracefully
- ✅ Document configuration options
- ✅ Link to related agents
- ✅ Set appropriate pricing

### Don'ts
- ❌ Over-engineer simple agents
- ❌ Skip error handling
- ❌ Use vague descriptions
- ❌ Forget edge cases
- ❌ Ignore platform requirements
- ❌ Skip testing
- ❌ Underprice your work

---

## 🔗 Related Resources

- [SKILL_PATTERNS.md](./SKILL_PATTERNS.md) - Reusable skill patterns
- [templates/](./templates/) - Agent templates
- [schemas/agent-schema.json](./schemas/agent-schema.json) - Schema definition

---

*Version: 1.0 | Last Updated: March 2026*
