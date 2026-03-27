# 🎯 Zero-Shot Design Principles

> **Design Agents That Find Themselves**
> 
> This document teaches you how to design agent specifications that are discoverable through zero-shot navigation—the key to making your agents usable without prior training.

---

## 🧠 What is Zero-Shot Navigation?

**Zero-shot navigation** means an AI agent can find the right tool in this repository without having seen it before—no training, no memorization, just semantic understanding.

**How it works**:
1. Agent reads the structure
2. Matches user intent to available options
3. Navigates to the correct location
4. Finds the exact tool needed

**Why it matters**: 
- No onboarding required
- Instant productivity
- Self-documenting architecture
- Scalable knowledge organization

---

## 🏗️ The Five Design Principles

### Principle 1: Semantic Clustering

**Concept**: Group related concepts together, separate unrelated ones.

**Bad Design**:
```
agents/
├── agent_001.md
├── agent_002.md
├── agent_003.md
├── agent_004.md
└── agent_005.md
```

**Good Design**:
```
agents/
├── reasoning-patterns/
│   ├── react-reasoner/
│   ├── chain-thought/
│   └── tree-thought/
├── code-generation/
│   ├── code-architect/
│   └── refactoring-engine/
└── analysis/
    ├── sentiment-analyzer/
    └── pattern-detector/
```

**Implementation**:
- Use descriptive category names
- Max 5-10 items per category
- Create subcategories when needed
- Use consistent naming conventions

---

### Principle 2: Intent-Reveal Naming

**Concept**: Names should reveal purpose instantly.

**Bad Names**:
- `agent_v2.py`
- `processor.js`
- `helper.md`
- `utils.py`

**Good Names**:
- `sentiment-analyzer/`
- `code-reviewer/`
- `pdf-extractor/`
- `email-composer/`

**Naming Formula**:
```
[domain]-[action]-[specialty]

Examples:
- fishing-catch-predictor
- code-security-scanner
- document-summary-generator
- email-tone-adjuster
```

---

### Principle 3: Progressive Disclosure

**Concept**: Start simple, reveal complexity on demand.

**Level 0: One-line summary**
```
# Sentiment Analyzer
> Analyzes emotional tone in text with confidence scores.
```

**Level 1: Key capabilities**
```
## Capabilities
- Binary sentiment (positive/negative)
- Multi-class emotion detection
- Aspect-based sentiment
- Confidence scoring
```

**Level 2: Detailed usage**
```
## Usage Examples
### Basic Sentiment
Input: "I love this product!"
Output: {"sentiment": "positive", "confidence": 0.95}

### Aspect-Based
Input: "The food was great but service was slow."
Output: {"aspects": {"food": "positive", "service": "negative"}}
```

**Level 3: Technical details**
```
## Configuration
[model specs, parameters, integration details]
```

---

### Principle 4: Cross-Linking

**Concept**: Every document links to related documents.

**Pattern**:
```markdown
## Related Agents
- `sentiment-analyzer/` - Basic sentiment detection
- `emotion-detector/` - Multi-class emotions
- `aspect-sentiment/` - Aspect-based analysis

## Used By
- `customer-support-suite/` - For ticket routing
- `social-media-monitor/` - For brand tracking

## Prerequisites
- `text-preprocessor/` - For cleaning input
```

**Why it works**: Agents can traverse the knowledge graph to find related tools.

---

### Principle 5: Consistent Structure

**Concept**: Same template everywhere, predictable locations.

**Standard Agent README Template**:
```markdown
# [Agent Name]

> [One-line description]

## Quick Info
| Attribute | Value |
|-----------|-------|
| Category | [category] |
| Complexity | [simple|moderate|complex] |
| Platform | [platforms] |
| Input | [input type] |
| Output | [output type] |

## What It Does
[2-3 sentences of detail]

## Capabilities
- [Capability 1]
- [Capability 2]
- [Capability 3]

## Usage
### Example 1
Input: `[example]`
Output: `[example]`

## Configuration
```json
{
  "agent_type": "[type]",
  "parameters": {}
}
```

## When To Use
- [Scenario 1]
- [Scenario 2]

## When NOT To Use
- [Scenario 1]
- [Scenario 2]

## Related Agents
- `related-agent-1/` - [Relationship]

## Monetization
- Platform: [Platform]
- Pricing: [Price model]
```

---

## 📐 Zero-Shot Metadata Schema

Every agent should have machine-readable metadata:

```json
{
  "metadata": {
    "id": "sentiment-analyzer-v1",
    "name": "Sentiment Analyzer",
    "category": "analysis",
    "subcategory": "text-analysis",
    "complexity": "simple",
    "tags": ["sentiment", "nlp", "text", "emotion", "analysis"],
    "keywords": ["sentiment analysis", "emotion detection", "text analysis"],
    "input_types": ["text"],
    "output_types": ["json", "structured"],
    "platforms": ["minimax", "claude-mcp", "agentnode"],
    "related": ["emotion-detector", "text-classifier"],
    "prerequisites": [],
    "alternatives": ["text-classifier", "opinion-miner"],
    "version": "1.0.0",
    "last_updated": "2026-03-28"
  }
}
```

---

## 🔍 Discoverability Optimization

### Keyword Optimization

**Think about how agents search**:

```
User: "I need to analyze customer feedback"

Agent searches for:
- "feedback" → might miss
- "sentiment" → might miss
- "analyze" → too broad

Solution: Include all relevant keywords
```

**Keyword Placement**:
1. Title (highest weight)
2. One-line description
3. Capabilities section
4. Tags metadata
5. Usage examples

### Intent Matching

**Cover common intents**:

| User Intent | Keywords to Include |
|-------------|---------------------|
| "analyze text" | "analyze, text, nlp, processing" |
| "find patterns" | "pattern, detect, identify, recognize" |
| "generate content" | "generate, create, write, compose" |
| "transform data" | "transform, convert, process, format" |
| "make decisions" | "decide, recommend, suggest, choose" |

---

## 🎯 Decision Tree Integration

Your agent should be reachable via the decision tree:

```
DECISION_TREE.md
├── "What do you want to do?"
│   ├── "Analyze something"
│   │   ├── "Text data" → agents/analysis/sentiment-analyzer/
│   │   └── "Numerical data" → agents/analysis/pattern-detector/
│   ├── "Generate something"
│   │   ├── "Code" → agents/code-generation/
│   │   └── "Content" → agents/creative/
│   └── "Automate something"
│       └── agents/automation/
```

**Add your agent to the tree**:
1. Find the right branch
2. Add your agent as a leaf
3. Use clear, action-oriented labels

---

## 🧪 Zero-Shot Testing

### Test Your Agent's Discoverability

**Test Script**:
```
Prompt 1: "I need to [what your agent does]"
Expected: Agent finds your agent

Prompt 2: "Help me with [related task]"
Expected: Agent finds your agent as option

Prompt 3: "What tools do you have for [domain]?"
Expected: Agent lists your agent

Prompt 4: "I want to [alternative phrasing]"
Expected: Agent finds your agent
```

**If tests fail**:
- Add more keywords
- Improve description
- Add to more categories
- Cross-link from popular agents

---

## 📊 Zero-Shot Metrics

Track how discoverable your agents are:

| Metric | Target | Measurement |
|--------|--------|-------------|
| First-query hit rate | >80% | Agent finds it on first try |
| Navigation depth | ≤3 | Steps from NAVIGATION.md |
| Keyword coverage | >90% | Common intents matched |
| Cross-link density | 3+ | Links to/from other agents |

---

## 🛠️ Implementation Checklist

### For New Agents

- [ ] Descriptive name (intent-revealing)
- [ ] One-line description (semantic summary)
- [ ] Consistent README structure
- [ ] Metadata JSON with all fields
- [ ] Cross-links to related agents
- [ ] Added to NAVIGATION.md
- [ ] Added to DECISION_TREE.md
- [ ] Added to TOOL_CARDS.md (if core)
- [ ] Keyword coverage tested
- [ ] Zero-shot discovery tested

### For Existing Agents

- [ ] Audit naming conventions
- [ ] Verify semantic clustering
- [ ] Add missing cross-links
- [ ] Update metadata
- [ ] Test discoverability
- [ ] Add to navigation structures

---

## 🎨 Example: Complete Zero-Shot Agent

```markdown
# PDF Table Extractor

> Extracts structured tables from PDF documents with accuracy scoring.

## Quick Info
| Attribute | Value |
|-----------|-------|
| Category | document-processing |
| Complexity | moderate |
| Platform | minimax, claude-mcp, agentnode |
| Input | PDF file (base64) |
| Output | JSON tables |

## What It Does
Analyzes PDF documents to identify and extract tables, returning structured 
data with column headers, row data, and confidence scores for each extraction.

## Capabilities
- Multi-page table detection
- Merged cell handling
- Header identification
- Confidence scoring per cell
- Export to CSV, JSON, Excel formats

## Usage
### Example: Extract Invoice Table
Input: `invoice.pdf` (base64 encoded)
Output:
```json
{
  "tables": [
    {
      "page": 1,
      "headers": ["Item", "Quantity", "Price"],
      "rows": [["Widget A", "10", "$100"]],
      "confidence": 0.94
    }
  ]
}
```

## When To Use
- Invoice processing
- Report data extraction
- Financial statement parsing
- Research paper table extraction

## When NOT To Use
- Image-only PDFs (use OCR first)
- Handwritten tables
- Highly complex nested tables

## Related Agents
- `pdf-extractor/` - General PDF text extraction
- `ocr-processor/` - For scanned documents
- `data-validator/` - Validate extracted data

## Configuration
```json
{
  "agent_type": "pdf-table-extractor",
  "parameters": {
    "confidence_threshold": 0.8,
    "output_format": "json"
  }
}
```

## Monetization
- Platform: MiniMax Experts, AgentNode
- Pricing: 2 credits per page processed
```

---

## 🔄 Continuous Improvement

### Feedback Loop

```
1. Monitor agent discovery paths
2. Identify failed searches
3. Add missing keywords
4. Update cross-links
5. Re-test zero-shot discovery
```

### A/B Testing

**Test different descriptions**:
```
Variant A: "Extracts tables from PDFs"
Variant B: "Convert PDF tables to structured data automatically"

Measure: Which one gets found more often?
```

---

## 📚 Related Resources

- [NAVIGATION.md](./NAVIGATION.md) - The navigation hub
- [DECISION_TREE.md](./DECISION_TREE.md) - Guided discovery
- [TOOL_CARDS.md](./TOOL_CARDS.md) - Quick reference
- [AGENT_BUILDER_GUIDE.md](./AGENT_BUILDER_GUIDE.md) - Building agents

---

*Last Updated: March 28, 2026 - Zero-shot design principles for agent discoverability*
