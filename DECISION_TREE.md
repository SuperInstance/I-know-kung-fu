# Decision Tree for Tool Discovery

> **Guided tool discovery through systematic questioning. Follow the branches to find the optimal tool.**

---

## 🌳 Master Decision Tree

```
START: What are you trying to accomplish?
│
├─► ANSWER A SINGLE QUESTION / PERFORM ONE TASK
│   │
│   ├─► Is it a simple utility operation?
│   │   └─► YES → See [Quick Tasks Tree](#quick-tasks-tree)
│   │   └─► NO → Continue...
│   │
│   ├─► Does it require deep reasoning?
│   │   └─► YES → See [Reasoning Tree](#reasoning-tree)
│   │   └─► NO → Continue...
│   │
│   └─► Is it about retrieving information?
│       └─► YES → See [Retrieval Tree](#retrieval-tree)
│       └─► NO → See [Specialized Tree](#specialized-tree)
│
├─► SOLVE A COMPLEX MULTI-STEP PROBLEM
│   │
│   ├─► Do you know all the steps upfront?
│   │   └─► YES → Plan-Execute Agent
│   │   └─► NO → Continue...
│   │
│   ├─► Need to explore multiple approaches?
│   │   └─► YES → Tree-of-Thought Agent
│   │   └─► NO → Continue...
│   │
│   ├─► Need to use tools/actions?
│   │   └─► YES → ReAct Reasoner
│   │   └─► NO → Chain-of-Thought Agent
│   │
│   └─► Need self-improvement?
│       └─► YES → Reflection Agent
│       └─► NO → Chain-of-Thought Agent
│
├─► COORDINATE MULTIPLE AGENTS
│   │
│   ├─► Need top-down control?
│   │   └─► YES → Hierarchy Manager
│   │   └─► NO → Continue...
│   │
│   ├─► Need distributed parallelism?
│   │   └─► YES → Swarm Coordinator
│   │   └─► NO → Continue...
│   │
│   ├─► Need consensus/agreement?
│   │   └─► YES → Consensus Builder
│   │   └─► NO → Continue...
│   │
│   ├─► Need debate/perspectives?
│   │   └─► YES → Debate Moderator
│   │   └─► NO → Pipeline Orchestrator
│   │
│   └─► Sequential stages?
│       └─► YES → Pipeline Orchestrator
│       └─► NO → Swarm Coordinator
│
├─► BUILD AN ENTERPRISE SOLUTION
│   │
│   ├─► What domain?
│   │   ├─► Customer Support → Customer Support Suite
│   │   ├─► Security → Security Suite
│   │   ├─► Data Science → Data Science Suite
│   │   ├─► Development → Developer Productivity Suite
│   │   ├─► Finance → Financial Analysis Suite
│   │   ├─► Legal → Legal Document Suite
│   │   ├─► Marketing → Marketing Suite
│   │   └─► Projects → Project Management Suite
│   │
│   └─► Need custom combination? → See [Suite Builder](#suite-builder)
│
└─► OPTIMIZE COSTS / PERFORMANCE
    │
    ├─► Reducing LLM costs?
    │   └─► YES → Escalation Router (40x reduction)
    │   └─► NO → Continue...
    │
    ├─► Reducing token usage?
    │   └─► YES → Context Compressor (60% savings)
    │   └─► NO → Continue...
    │
    ├─► Eliminating redundant calls?
    │   └─► YES → Cache Manager (80% hit rate)
    │   └─► NO → Continue...
    │
    ├─► Tool calling issues?
    │   └─► YES → Tool Guardian (50% error reduction)
    │   └─► NO → Continue...
    │
    └─► Memory management?
        └─► YES → Hierarchical Memory
        └─► NO → Performance Tracker
```

---

## 🔧 Quick Tasks Tree

```
What type of quick task?
│
├─► DATA TRANSFORMATION
│   ├─► Format JSON → JSON Formatter
│   ├─► Format data → Data Transformer
│   └─► Build SQL → SQL Builder
│
├─► VALIDATION
│   ├─► Validate JSON → JSON Formatter
│   ├─► Validate SSL → SSL Checker
│   └─► Check domain → Domain Checker
│
├─► TEXT PROCESSING
│   ├─► Count tokens → Token Counter
│   ├─► Build regex → Regex Helper
│   └─► Convert timestamps → Timestamp Converter
│
├─► NETWORK
│   ├─► Test API → API Tester
│   ├─► Check SSL → SSL Checker
│   ├─► Lookup domain → Whois Lookup
│   └─► Trace redirects → Redirect Tracer
│
├─► GENERATION
│   ├─► Generate password → Password Generator
│   ├─► Generate mock data → Mock Data Generator
│   ├─► Generate QR → Text-to-QR
│   └─► Generate Dockerfile → Dockerfile Generator
│
└─► ANALYSIS
    ├─► View image metadata → EXIF Viewer
    ├─► Extract meta tags → Meta Tag Extractor
    ├─► Geolocate IP → IP Geolocator
    └─► Compare files → Diff Viewer
```

---

## 🧠 Reasoning Tree

```
What kind of reasoning do you need?
│
├─► STEP-BY-STEP LOGICAL REASONING
│   │
│   ├─► Is there a single clear path?
│   │   └─► YES → Chain-of-Thought Agent
│   │   └─► NO → Continue...
│   │
│   └─► Need to explore alternatives?
│       └─► YES → Tree-of-Thought Agent
│       └─► NO → Chain-of-Thought Agent
│
├─► INTERLEAVED THINKING AND ACTION
│   │
│   ├─► Need to use tools/APIs?
│   │   └─► YES → ReAct Reasoner
│   │   └─► NO → Chain-of-Thought Agent
│   │
│   └─► Unknown steps at start?
│       └─► YES → ReAct Reasoner
│       └─► NO → Plan-Execute Agent
│
├─► PLANNING AND EXECUTION
│   │
│   ├─► All steps known upfront?
│   │   └─► YES → Plan-Execute Agent
│   │   └─► NO → ReAct Reasoner
│   │
│   └─► Parallel execution possible?
│       └─► YES → Plan-Execute Agent (with parallel)
│       └─► NO → Pipeline Orchestrator
│
└─► SELF-IMPROVEMENT
    │
    ├─► Quality not good enough?
    │   └─► YES → Reflection Agent
    │   └─► NO → Chain-of-Thought Agent
    │
    └─► Need multiple perspectives?
        └─► YES → Tree-of-Thought Agent
        └─► NO → Reflection Agent
```

---

## 📚 Retrieval Tree

```
What kind of information retrieval?
│
├─► DOCUMENT-BASED Q&A
│   │
│   ├─► Large document collection?
│   │   └─► YES → RAG Pipeline
│   │   └─► NO → RAG Pipeline (simple config)
│   │
│   └─► Need citations?
│       └─► YES → RAG Pipeline (with citations)
│       └─► NO → Context Manager + simple search
│
├─► ENTITY RELATIONSHIPS
│   │
│   ├─► Complex relationships between entities?
│   │   └─► YES → Knowledge Graph Agent
│   │   └─► NO → RAG Pipeline
│   │
│   └─► Need path finding?
│       └─► YES → Knowledge Graph Agent
│       └─► NO → RAG Pipeline
│
├─► CONTEXT MANAGEMENT
│   │
│   ├─► Token limits an issue?
│   │   └─► YES → Context Manager
│   │   └─► NO → Standard retrieval
│   │
│   └─► Multiple sources?
│       └─► YES → Context Manager + RAG Pipeline
│       └─► NO → Simple retrieval
│
└─► KNOWLEDGE BASE BUILDING
    │
    ├─► From documents?
    │   └─► YES → RAG Pipeline + Knowledge Extractor
    │   └─► NO → Knowledge Graph Agent
    │
    └─► Structured knowledge?
        └─► YES → Knowledge Graph Agent
        └─► NO → RAG Pipeline
```

---

## 🎯 Specialized Tree

```
What specialized domain?
│
├─► SOFTWARE DEVELOPMENT
│   ├─► Architecture design → Code Architect
│   ├─► Code improvement → Refactoring Engine
│   ├─► Testing → Test Generator
│   ├─► Code review → Code Reviewer
│   └─► API design → API Designer
│
├─► SECURITY
│   ├─► Threat analysis → Threat Hunter
│   ├─► Incident response → Incident Responder
│   ├─► Compliance → Compliance Checker
│   └─► Full solution → Security Suite
│
├─► DATA & ANALYTICS
│   ├─► Data analysis → Data Transformer
│   ├─► Query optimization → Query Optimizer
│   ├─► ML pipelines → RAG Pipeline + Analysis
│   └─► Full solution → Data Science Suite
│
├─► CONTENT & WRITING
│   ├─► Content creation → Content Writer
│   ├─► Presentation design → Presentation Designer
│   ├─► Fiction writing → Fiction Writer
│   └─► Full solution → Marketing Suite
│
├─► CUSTOMER SUPPORT
│   ├─► Query routing → Escalation Router
│   ├─► Knowledge retrieval → RAG Pipeline
│   ├─► Quality monitoring → Feedback Processor
│   └─► Full solution → Customer Support Suite
│
└─► EXPERIMENTATION
    ├─► Run experiments → A/B Tester
    ├─► Generate variants → Variant Generator
    └─► Analyze results → Results Analyzer
```

---

## 🏗️ Suite Builder

```
Building a custom suite? Combine these components:

BASE LAYER (choose one):
├─► Reasoning → Chain-of-Thought or ReAct Reasoner
├─► Retrieval → RAG Pipeline
└─► Orchestration → Pipeline Orchestrator

ENHANCEMENT LAYER (add as needed):
├─► Memory → Hierarchical Memory
├─► Cost Optimization → Escalation Router
├─► Quality → Reflection Agent
├─► Reliability → Tool Guardian
└─► Context → Context Manager

DOMAIN LAYER (add as needed):
├─► Code → Code Architect + Test Generator
├─► Security → Threat Hunter + Incident Responder
├─► Analytics → Results Analyzer + A/B Tester
└─► Content → Content Writer + Presentation Designer

OUTPUT LAYER (choose one):
├─► Document → Document Processor
├─► Report → Results Analyzer
└─► API → API Designer

Example: Customer Support Suite
= Base: RAG Pipeline
+ Enhancement: Escalation Router + Memory
+ Domain: Feedback Processor
+ Output: Document Processor
```

---

## 🌐 Platform Selection

```
Where do you want to deploy?
│
├─► MONETIZATION FOCUSED
│   │
│   ├─► Credit-based marketplace?
│   │   └─► YES → MiniMax Experts
│   │   └─► NO → Continue...
│   │
│   ├─► Enterprise sales?
│   │   └─► YES → Claude MCP
│   │   └─► NO → MindStudio
│   │
│   └─► Quick monetization?
│       └─► YES → Skills.sh or ClawHub
│       └─► NO → AgentNode
│
├─► RAPID DEPLOYMENT
│   │
│   ├─► No-code preferred?
│   │   └─► YES → MindStudio or Dify
│   │   └─► NO → Continue...
│   │
│   ├─► Workflow automation?
│   │   └─► YES → Zapier AI or n8n
│   │   └─► NO → Continue...
│   │
│   └─► Enterprise integration?
│       └─► YES → Claude MCP
│       └─► NO → MindStudio
│
├─► DEVELOPER TOOLS
│   │
│   ├─► Multi-agent systems?
│   │   └─► YES → AutoGen
│   │   └─► NO → Continue...
│   │
│   ├─► Code generation?
│   │   └─► YES → GPT Engineer
│   │   └─► NO → Continue...
│   │
│   └─► Skill distribution?
│       └─► YES → Skills.sh or ClawHub
│       └─► NO → LangChain
│
└─► REGIONAL DEPLOYMENT
    │
    ├─► China market?
    │   └─► YES → Zhipu AI, Baidu, or MiniMax China
    │   └─► NO → Continue...
    │
    ├─► Japan market?
    │   └─► YES → JAPAN AI AGENT or miibo
    │   └─► NO → Continue...
    │
    ├─► Europe (GDPR focus)?
    │   └─► YES → Mistral AI or Aleph Alpha
    │   └─► NO → Global platforms
    │
    └─► Global?
        └─► MiniMax Experts or MindStudio
```

---

## 🚨 Emergency Decisions

```
URGENT: Something is broken/wrong
│
├─► LLM COSTS TOO HIGH
│   └─► IMMEDIATE: Escalation Router
│       └─► Additional: Cache Manager
│
├─► CONTEXT OVERFLOW
│   └─► IMMEDIATE: Context Compressor
│       └─► Additional: Hierarchical Memory
│
├─► TOOLS NOT WORKING
│   └─► IMMEDIATE: Tool Guardian
│       └─► Additional: Reflection Agent
│
├─► POOR OUTPUT QUALITY
│   └─► IMMEDIATE: Reflection Agent
│       └─► Additional: Feedback Processor
│
├─► SYSTEM TOO SLOW
│   └─► IMMEDIATE: Cache Manager
│       └─► Additional: Escalation Router
│
└─► AGENTS NOT COORDINATING
    └─► IMMEDIATE: Hierarchy Manager
        └─► Additional: Consensus Builder
```

---

## 📊 Complexity Assessment

```
How complex is your task?

SCORE YOUR TASK:
+1 point for each:
[ ] Multiple steps required
[ ] External data needed
[ ] Multiple tools/APIs involved
[ ] Decisions at each step
[ ] Multiple possible outcomes
[ ] Requires reasoning
[ ] Needs memory of previous steps
[ ] Parallel processing possible
[ ] Quality constraints strict
[ ] Cost constraints strict

SCORE → COMPLEXITY LEVEL:
0-2: Simple → Quick Tasks
3-4: Moderate → Reasoning Patterns
5-6: Complex → Multi-Agent Orchestration
7-8: Very Complex → Combined Suites
9-10: Enterprise → Custom Suite Build
```

---

*Last Updated: March 2026*
