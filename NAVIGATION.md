# Agent Navigation Hub

> **Zero-Shot Intelligence Optimized** - Designed for AI agents to quickly identify and access the right expert profile.

---

## 🎯 Quick Skill Finder

**I need an agent that can...**

| Task Category | Best Agent | Location |
|--------------|------------|----------|
| Reduce LLM costs | Escalation Router | `agents/escalation-engine/` |
| Remember context | Hierarchical Memory | `agents/hierarchical-memory/` |
| Make tools reliable | Tool Guardian | `agents/tool-guardian/` |
| Navigate codebases | Codebase Onboarder | `agents/developer-experience/codebase-onboarder/` |
| Process documents | Document Processor | `platforms/minimax-experts/document-processor/` |
| Handle spreadsheets | Spreadsheet Analyst | `platforms/minimax-experts/spreadsheet-analyst/` |
| Generate images | Image Generator | `platforms/minimax-experts/image-generator/` |
| Build presentations | Presentation Builder | `platforms/minimax-experts/presentation-builder/` |
| Analyze security | Security Analyst | `agents/role-based/security-analyst/` |
| Write code | Code Assistant | `platforms/minimax-experts/code-assistant/` |
| Create content | Content Writer | `platforms/minimax-experts/content-writer/` |
| Research web | Web Intelligence | `platforms/minimax-experts/web-intelligence/` |
| Process PDFs | PDF Toolkit | `platforms/minimax-experts/pdf-toolkit/` |
| Manage APIs | API Designer | `agents/developer-experience/api-designer/` |
| Optimize queries | Query Optimizer | `agents/performance/query-optimizer/` |
| Handle incidents | Incident Responder | `agents/security-ops/incident-responder/` |
| Analyze markets | Market Analyst | `agents/business-intelligence/market-analyst/` |
| Monitor threats | Threat Hunter | `agents/security-ops/threat-hunter/` |
| Manage projects | Project Management Suite | `agents/combined-suites/project-management-suite/` |
| Support customers | Customer Support Suite | `agents/combined-suites/customer-support-suite/` |

---

## 🧭 Navigation by Intent

### I want to MONETIZE my agents
→ **Start here**: `strategy/go-to-market.md`
→ **Platform comparison**: `research/market-research.md`
→ **Revenue projections**: `strategy/go-to-market.md#revenue-projections`

### I want to BUILD a new agent
→ **Template**: `templates/minimax-expert-template.json`
→ **Schema**: `schemas/agent-schema.json`
→ **Pattern abstractions**: `schemas/skill-pattern-abstractions.md`

### I want to DEPLOY to a platform
| Platform | Best For | Quick Start |
|----------|----------|-------------|
| MiniMax Experts | Credit-based marketplace | `platforms/minimax-experts/PLATFORM-README.md` |
| Claude MCP | Tool integration servers | `platforms/claude-mcp/PLATFORM-README.md` |
| MindStudio | No-code agent builder | `platforms/mindstudio/` |
| AgentNode | Skill marketplace | `platforms/agentnode/` |
| OpenAI GPT Store | Custom GPTs | `platforms/openai-gpt-store/PLATFORM-README.md` |
| Zapier AI | Workflow automation | `platforms/zapier-ai/` |
| Dify | Open-source workflows | `platforms/dify/` |
| AutoGen | Multi-agent systems | `platforms/autogen/` |
| ClawHub | Skill marketplace | `platforms/clawhub/` |
| Skills.sh | Agent skills directory | `platforms/skills-sh/` |

### I want to UNDERSTAND skill patterns
→ **Pattern guide**: `schemas/skill-pattern-abstractions.md`
→ **Reasoning patterns**: `agents/reasoning-patterns/`
→ **Multi-agent orchestration**: `agents/multi-agent-orchestration/`

---

## 📊 Agent Categories (Click to Explore)

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
```

### 🧠 Reasoning Pattern Agents (NEW)

```
agents/reasoning-patterns/
├── react-reasoner/          # ReAct pattern
├── plan-executor/           # Plan-and-Execute
├── chain-thought/           # Chain-of-Thought
├── tree-thought/            # Tree-of-Thought
└── reflection-agent/        # Self-reflection
```

### 🤝 Multi-Agent Orchestration (NEW)

```
agents/multi-agent-orchestration/
├── swarm-coordinator/       # Swarm intelligence
├── debate-moderator/        # Multi-perspective debate
├── consensus-builder/       # Agreement seeking
├── hierarchy-manager/       # Hierarchical teams
└── pipeline-orchestrator/   # Sequential pipelines
```

### 🔄 Transformation Agents

```
agents/transformation/
├── api-migrator/            # API version migration
└── data-transformer/        # Data format conversion
```

### ✅ Validation Agents

```
agents/validation/
├── code-reviewer/           # Code review
├── compliance-checker/      # Compliance checking
├── contract-validator/      # Contract validation
└── structured-data-validator/ # Data validation
```

### 🎨 Creative Agents

```
agents/creative/
├── audio-producer/          # Audio production
├── fiction-writer/          # Fiction writing
├── presentation-designer/   # Presentation design
└── world-builder/           # World building
```

### 📦 Combined Suites (Enterprise)

```
agents/combined-suites/
├── customer-support-suite/  # Complete support
├── data-science-suite/      # Data analysis
├── developer-productivity-suite/ # Developer tools
├── financial-analysis-suite/ # Financial analysis
├── legal-document-suite/    # Legal documents
├── marketing-suite/         # Marketing tools
├── project-management-suite/ # Project management
├── research-suite/          # Research tools
└── security-suite/          # Security tools
```

---

## 🌍 Global Platform Coverage

### China (中国)
- Zhipu AI (智谱AI) - `global-platforms/china/`
- Baidu Wenxin (百度文心)
- Alibaba Tongyi (阿里通义)
- Tencent Yuanqi (腾讯元器)
- ByteDance

### Japan (日本)
- JAPAN AI AGENT - `global-platforms/japan/`
- miibo - Multi-agent platform
- Microsoft Japan

### Europe
- Mistral AI
- DeepMind
- Various EU platforms

---

## 🔧 Utility & Infrastructure

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

---

## 🔐 Security & Compliance

```
agents/
├── security-ops/
│   ├── incident-responder/  # Incident response
│   └── threat-hunter/       # Threat hunting
├── data-lifecycle/
│   ├── data-anonymizer/     # Data anonymization
│   └── pii-scanner/         # PII detection
└── accessibility/
    ├── screen-reader-optimizer/ # Accessibility
    ├── wcag-auditor/        # WCAG compliance
    └── accessibility-statement-generator/
```

---

## 📈 Business Intelligence

```
agents/
├── business-intelligence/
│   ├── competitive-intel/   # Competitive analysis
│   └── market-analyst/      # Market analysis
└── collaboration/
    ├── knowledge-base-builder/ # Knowledge management
    └── meeting-facilitator/ # Meeting facilitation
```

---

## 🚀 Emerging Tech

```
agents/
├── emerging-tech/
│   ├── ar-vr-content/       # AR/VR content
│   └── voice-interface-designer/ # Voice UI
├── specialized-domains/
│   ├── blockchain-web3/     # Blockchain/Web3
│   ├── climate-tech/        # Climate technology
│   ├── fintech-regtech/     # Fintech/Regtech
│   ├── ocean-tech/          # Ocean technology
│   ├── robotics-automation/ # Robotics
│   └── space-tech/          # Space technology
└── sustainability/
    ├── carbon-footprint-calculator/
    └── green-cloud-advisor/
```

---

## 🧠 Meta-Intelligence

```
agents/
├── meta-intelligence/
│   ├── context-compressor/  # Compress context
│   ├── prompt-evolver/      # Evolve prompts
│   └── skill-learner/       # Learn new skills
└── automation-novice/
    └── workflow-automator/  # Workflow automation
```

---

## 📋 Quick Reference Cards

### Skill Creation Checklist
- [ ] Define purpose (one sentence)
- [ ] List required inputs
- [ ] List expected outputs
- [ ] Define error handling
- [ ] Add examples (3-5)
- [ ] Set pricing tier
- [ ] Create README.md
- [ ] Create schema.json
- [ ] Create config files

### Platform Compatibility Matrix

| Agent Type | MiniMax | Claude MCP | MindStudio | GPT Store | n8n |
|-----------|---------|------------|------------|-----------|-----|
| Quick Task | ✅ | ✅ | ✅ | ✅ | ✅ |
| Role-Based | ✅ | ✅ | ✅ | ✅ | ⚠️ |
| Vertical | ✅ | ⚠️ | ✅ | ✅ | ⚠️ |
| Suite | ✅ | ✅ | ✅ | ⚠️ | ✅ |
| MCP Server | ❌ | ✅ | ❌ | ❌ | ⚠️ |

✅ = Native support | ⚠️ = Possible with adaptation | ❌ = Not applicable

---

## 🎓 Learning Paths

### Beginner: Build Your First Agent
1. Start with `agents/quick-tasks/password-generator/`
2. Study `templates/minimax-expert-template.json`
3. Read `schemas/skill-pattern-abstractions.md`

### Intermediate: Create a Suite
1. Study `agents/combined-suites/customer-support-suite/`
2. Combine 3-5 complementary agents
3. Add orchestration logic

### Advanced: Platform Integration
1. Study `platforms/claude-mcp/escalation-router/`
2. Create MCP server implementation
3. Add monetization strategy

---

*Last Updated: March 2026*
*Total Agents: 200+*
*Total Platforms: 12+*
*Total Skills: 400+*
