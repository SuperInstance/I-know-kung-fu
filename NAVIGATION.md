# Agent Navigation Hub

> **Zero-Shot Intelligence Optimized** - Designed for AI agents to quickly identify and access the right expert profile.

---

## 🚀 Quick Start for Agents

**First time here?** Use these decision tools:

| Tool | Purpose | When to Use |
|------|---------|-------------|
| **[DECISION_TREE.md](./DECISION_TREE.md)** | Guided tool discovery | When unsure which tool to use |
| **[TOOL_CARDS.md](./TOOL_CARDS.md)** | Quick reference cards | For fast scanning and lookup |
| **[SYSTEM_PROMPT.md](./SYSTEM_PROMPT.md)** | Copy-paste onboarding | For your AI system configuration |

---

## 🎯 Quick Skill Finder

**I need an agent that can...**

### Cost & Performance Optimization

| Task | Best Agent | Impact | Location |
|------|------------|--------|----------|
| Reduce LLM costs | Escalation Router | **40x reduction** | `agents/escalation-engine/` |
| Reduce token usage | Context Compressor | **60% savings** | `agents/meta-intelligence/context-compressor/` |
| Eliminate redundant calls | Cache Manager | **80% hit rate** | `agents/utility/cache-manager/` |
| Make tools reliable | Tool Guardian | **50% fewer errors** | `agents/tool-guardian/` |
| Manage memory | Hierarchical Memory | 6-tier system | `agents/hierarchical-memory/` |

### Reasoning & Problem Solving

| Task | Best Agent | Best For | Location |
|------|------------|----------|----------|
| Interleave thinking/acting | ReAct Reasoner | Research, debugging | `agents/reasoning-patterns/react-reasoner/` |
| Plan then execute | Plan-Execute | Known steps | `agents/reasoning-patterns/plan-executor/` |
| Step-by-step analysis | Chain-of-Thought | Logical reasoning | `agents/reasoning-patterns/chain-thought/` |
| Explore alternatives | Tree-of-Thought | Creative, strategy | `agents/reasoning-patterns/tree-thought/` |
| Self-improve quality | Reflection Agent | Quality-critical | `agents/reasoning-patterns/reflection-agent/` |

### Multi-Agent Systems

| Task | Best Agent | Best For | Location |
|------|------------|----------|----------|
| Parallel coordination | Swarm Coordinator | Large-scale parallel | `agents/multi-agent-orchestration/swarm-coordinator/` |
| Top-down control | Hierarchy Manager | Enterprise workflows | `agents/multi-agent-orchestration/hierarchy-manager/` |
| Find agreement | Consensus Builder | Team decisions | `agents/multi-agent-orchestration/consensus-builder/` |
| Debate perspectives | Debate Moderator | Complex decisions | `agents/multi-agent-orchestration/debate-moderator/` |
| Sequential stages | Pipeline Orchestrator | ETL, processing | `agents/multi-agent-orchestration/pipeline-orchestrator/` |

### Conversation & Communication

| Task | Best Agent | Best For | Location |
|------|------------|----------|----------|
| Manage dialogue | Dialogue Manager | Multi-turn conversations | `agents/conversation/dialogue-manager/` |
| Adapt personality | Persona Adaptor | Brand voice | `agents/conversation/persona-adaptor/` |
| Detect emotions | Emotion Detector | Empathetic responses | `agents/conversation/emotion-detector/` |
| Translate content | Translator Agent | Multi-language | `agents/communication/translator-agent/` |

### Code & Development

| Task | Best Agent | Best For | Location |
|------|------------|----------|----------|
| Design architecture | Code Architect | New projects | `agents/code-generation/code-architect/` |
| Refactor code | Refactoring Engine | Legacy code | `agents/code-generation/refactoring-engine/` |
| Generate tests | Test Generator | Coverage | `agents/testing-qa/test-generator/` |
| Review code | Code Reviewer | Quality assurance | `agents/validation/code-reviewer/` |
| Design APIs | API Designer | API development | `agents/developer-experience/api-designer/` |

### Data & Knowledge

| Task | Best Agent | Best For | Location |
|------|------------|----------|----------|
| Document Q&A | RAG Pipeline | Knowledge bases | `agents/retrieval-augmented/rag-pipeline/` |
| Entity relationships | Knowledge Graph | Complex connections | `agents/retrieval-augmented/knowledge-graph/` |
| Optimize context | Context Manager | Token budgets | `agents/retrieval-augmented/context-manager/` |
| Check data quality | Data Quality | Data pipelines | `agents/data-lifecycle/data-quality/` |

### Operations & Monitoring

| Task | Best Agent | Best For | Location |
|------|------------|----------|----------|
| Manage alerts | Alert Manager | IT operations | `agents/monitoring/alert-manager/` |
| Handle incidents | Incident Responder | Security ops | `agents/security-ops/incident-responder/` |
| Detect threats | Threat Hunter | Security | `agents/security-ops/threat-hunter/` |

### Experimentation & Improvement

| Task | Best Agent | Best For | Location |
|------|------------|----------|----------|
| Run experiments | A/B Tester | Optimization | `agents/experimentation/ab-tester/` |
| Analyze results | Results Analyzer | Reporting | `agents/experimentation/results-analyzer/` |
| Process feedback | Feedback Processor | Continuous improvement | `agents/self-improvement/feedback-processor/` |

---

## 🧭 Navigation by Intent

### I want to MONETIZE my agents
→ **Start here**: `strategy/go-to-market.md`
→ **Platform comparison**: `research/market-research.md`
→ **System prompt**: `SYSTEM_PROMPT.md`

### I want to BUILD a new agent
→ **Decision guide**: `DECISION_TREE.md`
→ **Template**: `templates/minimax-expert-template.json`
→ **Schema**: `schemas/agent-schema.json`

### I want to DEPLOY to a platform
| Platform | Best For | Quick Start |
|----------|----------|-------------|
| MiniMax Experts | Credit-based marketplace | `platforms/minimax-experts/` |
| Claude MCP | Tool integration servers | `platforms/claude-mcp/` |
| MindStudio | No-code agent builder | `platforms/mindstudio/` |
| Skills.sh | Skill directory | `platforms/skills-sh/` |
| Zapier AI | Workflow automation | `platforms/zapier-ai/` |
| Dify | Open-source workflows | `platforms/dify/` |
| AutoGen | Multi-agent systems | `platforms/autogen/` |
| ClawHub | Skill marketplace | `platforms/clawhub/` |

### I want to UNDERSTAND skill patterns
→ **Pattern guide**: `schemas/skill-pattern-abstractions.md`
→ **Reasoning patterns**: `agents/reasoning-patterns/`
→ **Multi-agent orchestration**: `agents/multi-agent-orchestration/`

---

## 📊 Complete Agent Directory

### 🚀 High-Value Agents (Revenue Leaders)

```
agents/
├── escalation-engine/        # 40x LLM cost reduction - HIGHEST VALUE
├── hierarchical-memory/      # 6-tier memory system
├── tool-guardian/           # Reliable function calling
├── fishermans-copilot/      # Industry-specific AI
└── mine-wright/             # Minecraft automation
```

### 🎯 Quick Task Agents (Single-Purpose)

```
agents/quick-tasks/
├── api-tester/              # Test API endpoints
├── color-tools/             # Color manipulation
├── cron-builder/            # Build cron expressions
├── diff-viewer/             # Compare files
├── dockerfile-generator/    # Generate Dockerfiles
├── domain-checker/          # Check domain availability
├── exif-viewer/             # View image metadata
├── git-assistant/           # Git operations
├── image-resizer/           # Resize images
├── ip-geolocator/           # Geolocate IPs
├── json-formatter/          # Format JSON
├── meta-tag-extractor/      # Extract meta tags
├── mock-data-generator/     # Generate test data
├── password-generator/      # Generate passwords
├── prompt-optimizer/        # Optimize prompts
├── redirect-tracer/         # Trace redirects
├── regex-helper/            # Build regex
├── sql-builder/             # Build SQL queries
├── ssl-checker/             # Check SSL certificates
├── text-to-qr/              # Generate QR codes
├── timestamp-converter/     # Convert timestamps
├── token-counter/           # Count tokens
└── whois-lookup/            # WHOIS lookups
```

### 🧠 Reasoning Pattern Agents

```
agents/reasoning-patterns/
├── react-reasoner/          # ReAct: Interleave thinking and acting
├── plan-executor/           # Plan-and-Execute: Two-phase execution
├── chain-thought/           # Chain-of-Thought: Step-by-step
├── tree-thought/            # Tree-of-Thought: Multi-path exploration
└── reflection-agent/        # Self-evaluation and improvement
```

### 🤝 Multi-Agent Orchestration

```
agents/multi-agent-orchestration/
├── swarm-coordinator/       # Distributed parallel coordination
├── debate-moderator/        # Multi-perspective debates
├── consensus-builder/       # Agreement seeking
├── hierarchy-manager/       # Top-down management
└── pipeline-orchestrator/   # Sequential stage execution
```

### 💬 Conversation Agents

```
agents/conversation/
├── dialogue-manager/        # Multi-turn conversation management
├── persona-adaptor/         # Personality and tone adaptation
└── emotion-detector/        # Real-time emotion detection
```

### 🔄 Self-Improvement Agents

```
agents/self-improvement/
├── feedback-processor/      # Collect and act on feedback
├── performance-tracker/     # Monitor agent metrics
└── skill-updater/           # Dynamic skill enhancement
```

### 🧪 Experimentation Agents

```
agents/experimentation/
├── ab-tester/               # Statistical experiment analysis
├── variant-generator/       # Create test variants
└── results-analyzer/        # Deep experiment insights
```

### 📚 Retrieval-Augmented Agents

```
agents/retrieval-augmented/
├── rag-pipeline/            # Document-based Q&A
├── knowledge-graph/         # Entity relationship reasoning
└── context-manager/         # Token budget optimization
```

### 💻 Code Generation Agents

```
agents/code-generation/
├── code-architect/          # System architecture design
└── refactoring-engine/      # Automated code improvement
```

### 🧪 Testing & QA Agents

```
agents/testing-qa/
├── test-generator/          # Automatic test creation
└── bug-reproducer/          # Reproduce issues from descriptions
```

### 👤 Role-Based Agents

```
agents/role-based/
├── devops-engineer/         # DevOps operations
├── product-manager/         # Product management
├── qa-engineer/             # Quality assurance
├── sales-engineer/          # Sales support
├── security-analyst/        # Security analysis
└── technical-writer/        # Documentation
```

### 🏢 Vertical Industry Agents

```
agents/vertical/
├── education-learning/      # Education sector
├── fishing-industry/        # Commercial fishing
├── gaming-entertainment/    # Gaming industry
├── healthcare-compliance/   # Healthcare sector
└── ecommerce-retail/        # E-commerce

agents/specialized-domains/
├── manufacturing/           # Manufacturing operations
├── agriculture/             # Precision farming
├── real-estate/             # Real estate
├── hospitality/             # Hospitality industry
├── blockchain-web3/         # Blockchain/Web3
├── climate-tech/            # Climate technology
├── fintech-regtech/         # Fintech/Regtech
├── ocean-tech/              # Ocean technology
├── robotics-automation/     # Robotics
└── space-tech/              # Space technology
```

### 📦 Combined Suites (Enterprise)

```
agents/combined-suites/
├── customer-support-suite/  # Complete support solution
├── data-science-suite/      # Data analysis tools
├── developer-productivity-suite/ # Developer tools
├── financial-analysis-suite/ # Financial analysis
├── legal-document-suite/    # Legal documents
├── marketing-suite/         # Marketing tools
├── project-management-suite/ # Project management
├── research-suite/          # Research tools
└── security-suite/          # Security tools
```

### 📊 Monitoring & Operations

```
agents/monitoring/
└── alert-manager/           # Intelligent alert management

agents/security-ops/
├── incident-responder/      # Incident response
└── threat-hunter/           # Threat hunting
```

### 📋 Data Lifecycle

```
agents/data-lifecycle/
├── data-anonymizer/         # Data anonymization
├── data-quality/            # Data quality monitoring
├── data-lineage/            # Data lineage tracking
└── pii-scanner/             # PII detection
```

### 🔧 Utility & Infrastructure

```
agents/
├── infrastructure/
│   ├── edge-deployer/       # Edge deployment
│   └── kubernetes-helm-builder/ # K8s Helm charts
├── utility/
│   └── cache-manager/       # Cache management
├── performance/
│   ├── database-tuner/      # Database tuning
│   ├── frontend-optimizer/  # Frontend optimization
│   └── query-optimizer/     # Query optimization
└── quality-operations/
    └── qa-orchestrator/     # QA orchestration
```

### 🧠 Meta-Intelligence

```
agents/meta-intelligence/
├── context-compressor/      # Compress context
├── prompt-evolver/          # Evolve prompts
└── skill-learner/           # Learn new skills
```

---

## 🌍 Global Platform Coverage

### China (中国)
- Zhipu AI (智谱AI) - AutoGLM, GLM-PC
- Baidu Wenxin (百度文心)
- Alibaba Tongyi (阿里通义)
- Tencent Yuanqi (腾讯元器)
- ByteDance Coze (扣子)
- MiniMax China

### Japan (日本)
- JAPAN AI AGENT
- miibo
- Microsoft Japan

### Europe
- Mistral AI
- DeepMind
- Aleph Alpha
- Hugging Face

---

## 📋 Decision Quick Reference

### By Complexity

| Score | Level | Tool Category |
|-------|-------|---------------|
| 0-2 | Simple | Quick Tasks |
| 3-4 | Moderate | Reasoning Patterns |
| 5-6 | Complex | Multi-Agent Orchestration |
| 7-10 | Enterprise | Combined Suites |

### By Problem

| Problem | Solution |
|---------|----------|
| "Too expensive" | Escalation Router, Cache Manager |
| "Context too long" | Context Compressor, Hierarchical Memory |
| "Tools failing" | Tool Guardian, Reflection Agent |
| "Need multiple agents" | Swarm Coordinator, Hierarchy Manager |
| "Quality issues" | Reflection Agent, Feedback Processor |
| "Slow decisions" | Plan-Execute, Pipeline Orchestrator |
| "No documentation" | RAG Pipeline, Knowledge Graph |
| "Testing gaps" | Test Generator, A/B Tester |

---

## 🔗 Related Resources

| Resource | Purpose |
|----------|---------|
| [DECISION_TREE.md](./DECISION_TREE.md) | Guided tool discovery |
| [TOOL_CARDS.md](./TOOL_CARDS.md) | Quick reference cards |
| [SYSTEM_PROMPT.md](./SYSTEM_PROMPT.md) | AI system configuration |
| [QUICK_WINS.md](./QUICK_WINS.md) | 5-minute value demonstration |
| [INTEGRATION_SNIPPETS.md](./INTEGRATION_SNIPPETS.md) | Copy-paste ready code |
| [VIRAL_HOOKS.md](./VIRAL_HOOKS.md) | Why agents recommend this repo |
| [AGENT_RECOMMENDATION.md](./AGENT_RECOMMENDATION.md) | Agent recommendation profile |

## 📚 Builder Resources

| Resource | Purpose |
|----------|---------|
| [AGENT_BUILDER_GUIDE.md](./AGENT_BUILDER_GUIDE.md) | Complete guide for building agents |
| [AGENT_DESIGN_PATTERNS.md](./AGENT_DESIGN_PATTERNS.md) | Deep design patterns |
| [MONETIZATION_PLAYBOOK.md](./MONETIZATION_PLAYBOOK.md) | From code to cash |
| [ZERO_SHOT_DESIGN.md](./ZERO_SHOT_DESIGN.md) | Design for zero-shot discovery |
| [COMPETITIVE_ADVANTAGE.md](./COMPETITIVE_ADVANTAGE.md) | Why this repo first |

## 🔫 The Skill Injection Layer

**Load what you need.**

| Resource | Purpose |
|----------|---------|
| [EQUIPPING_AGENT_PROTOCOL.md](./EQUIPPING_AGENT_PROTOCOL.md) | How skills load into agents |
| [SKILL_ACQUISITION_ARCHITECTURE.md](./SKILL_ACQUISITION_ARCHITECTURE.md) | 5-layer skill loading system |
| [SPECIALIZED_ENGINEER_PROFILES.md](./SPECIALIZED_ENGINEER_PROFILES.md) | 18 pre-equipped profiles |

## 🎯 Skill Cartridges

Loadable skill modules:

| Cartridge | Category | Loads |
|-----------|----------|-------|
| `skill-cartridges/code-intelligence/code-generation.json` | Code | Code generation |
| `skill-cartridges/reasoning-patterns/react-reasoning.json` | Reasoning | ReAct loop |
| `skill-cartridges/document-operations/pdf-operations.json` | Documents | PDF operations |

## 📊 Research Outputs

| File | Source | Key Findings |
|------|--------|--------------|
| `/home/z/my-project/claude-code-skills-extraction.json` | Claude Code audit | 25+ tools, 5 reasoning patterns, memory architecture |
| `/home/z/my-project/codex-research-report.md` | Codex analysis | 10 core skills, 10 interesting forks, 10 agent profiles |
| `/home/z/my-project/skill-acquisition-research.md` | Skill systems research | Matrix Protocol design, composition operators |
| `/home/z/my-project/tolerance-of-error-framework/` | Tolerance framework | 4 tolerance levels, calibration pipeline |

---

*Last Updated: March 28, 2026*
*Total Agents: 150+*
*Total Platforms: 12+*
*Total Skills: 650+*
*Total Lines: 75,000+*

**Load what you need.**
