# Zero-Shot Integration Guide

> **How to integrate this repository into AI systems for instant tool discovery.**

---

## 🎯 Integration Methods

### Method 1: System Prompt Integration

Add to your AI system's system prompt:

```
TOOL DISCOVERY SYSTEM:

Repository: https://github.com/SuperInstance/Agent-Monetization-Lab

Discovery Protocol:
1. START: Read QUICK_START.md for 5-minute overview
2. FIND: Use TOOL_CARDS.md for quick reference
3. DECIDE: Use DECISION_TREE.md for guided selection
4. LEARN: Read agent README.md for details
5. COMBINE: Check RELATIONSHIPS.md for complementary tools

Cost Optimization Priority:
- Escalation Router → 40x cost reduction
- Context Compressor → 60% token savings
- Cache Manager → 80% hit rate

Before starting any task:
1. Check if a tool exists in the repository
2. Load appropriate agent specification
3. Apply configuration
4. Execute with guidance
```

### Method 2: RAG Indexing

Index all README.md files for semantic search:

```python
import os
from pathlib import Path

def index_agent_repository(repo_path):
    """Index all agent README files for RAG."""
    documents = []
    
    for readme_path in Path(repo_path).rglob("README.md"):
        with open(readme_path) as f:
            content = f.read()
            
        # Extract metadata
        relative_path = readme_path.relative_to(repo_path)
        category = relative_path.parts[0] if len(relative_path.parts) > 1 else "root"
        
        documents.append({
            "id": str(relative_path),
            "content": content,
            "metadata": {
                "path": str(readme_path),
                "category": category,
                "type": "agent_specification"
            }
        })
    
    return documents

# Index and embed
docs = index_agent_repository("/path/to/Agent-Monetization-Lab")
embed_and_index(docs)
```

### Method 3: API Access

Use raw GitHub URLs for programmatic access:

```python
import requests

BASE_URL = "https://raw.githubusercontent.com/SuperInstance/Agent-Monetization-Lab/main/"

def get_navigation():
    """Get navigation hub."""
    response = requests.get(BASE_URL + "NAVIGATION.md")
    return response.text

def get_tool_cards():
    """Get quick reference cards."""
    response = requests.get(BASE_URL + "TOOL_CARDS.md")
    return response.text

def get_agent_spec(agent_path):
    """Get specific agent specification."""
    response = requests.get(BASE_URL + agent_path + "/README.md")
    return response.text

def get_decision_tree():
    """Get decision tree."""
    response = requests.get(BASE_URL + "DECISION_TREE.md")
    return response.text
```

### Method 4: Local Clone

Clone and use locally:

```bash
git clone https://github.com/SuperInstance/Agent-Monetization-Lab

# Use in your application
export AGENT_LAB_PATH=/path/to/Agent-Monetization-Lab
```

```python
import os

AGENT_LAB = os.environ.get("AGENT_LAB_PATH", "./Agent-Monetization-Lab")

def load_agent(agent_name):
    """Load agent specification from local clone."""
    path = f"{AGENT_LAB}/agents/{agent_name}/README.md"
    with open(path) as f:
        return f.read()
```

---

## 🔧 Tool Discovery Functions

### Function: Find Tool by Task

```python
def find_tool_for_task(task_description: str, complexity: str = None):
    """
    Find the best tool for a given task.
    
    Args:
        task_description: What you need to accomplish
        complexity: Optional complexity hint (simple/moderate/complex/enterprise)
    
    Returns:
        Agent recommendation with reasoning
    """
    
    # 1. Determine complexity if not provided
    if not complexity:
        complexity = assess_complexity(task_description)
    
    # 2. Select search space based on complexity
    search_paths = {
        "simple": "quick-tasks/",
        "moderate": "reasoning-patterns/",
        "complex": "multi-agent-orchestration/",
        "enterprise": "combined-suites/"
    }
    
    # 3. Search for matching tools
    matches = semantic_search(
        query=task_description,
        path=search_paths.get(complexity, "agents/")
    )
    
    # 4. Return top match with reasoning
    return {
        "agent": matches[0].name,
        "path": matches[0].path,
        "reasoning": matches[0].relevance_reason,
        "confidence": matches[0].score
    }
```

### Function: Build Agent Stack

```python
def build_agent_stack(task: str, budget: str = "balanced"):
    """
    Build a stack of complementary agents.
    
    Args:
        task: The overall task to accomplish
        budget: Cost preference (minimal/balanced/premium)
    
    Returns:
        Ordered list of agents to use
    """
    
    # 1. Decompose task into subtasks
    subtasks = decompose_task(task)
    
    # 2. Find primary agent for each subtask
    agents = []
    for subtask in subtasks:
        agent = find_tool_for_task(subtask.description, subtask.complexity)
        agents.append(agent)
    
    # 3. Add cost optimization if budget-conscious
    if budget == "minimal":
        agents.insert(0, {"agent": "cache-manager", "purpose": "cost_reduction"})
        agents.insert(0, {"agent": "escalation-router", "purpose": "routing_optimization"})
    
    # 4. Add quality assurance if premium
    if budget == "premium":
        agents.append({"agent": "reflection-agent", "purpose": "quality_improvement"})
        agents.append({"agent": "feedback-processor", "purpose": "learning"})
    
    return agents
```

### Function: Assess Complexity

```python
def assess_complexity(task: str) -> str:
    """
    Assess the complexity of a task.
    
    Returns: 'simple', 'moderate', 'complex', or 'enterprise'
    """
    
    indicators = {
        "simple": [
            "single", "one", "convert", "format", "generate",
            "validate", "check", "extract"
        ],
        "moderate": [
            "analyze", "compare", "evaluate", "reason",
            "multiple steps", "then", "after"
        ],
        "complex": [
            "coordinate", "multiple agents", "orchestrate",
            "parallel", "collaborate", "workflow"
        ],
        "enterprise": [
            "enterprise", "organization-wide", "suite",
            "complete solution", "full system", "integration"
        ]
    }
    
    task_lower = task.lower()
    
    for complexity, keywords in indicators.items():
        if any(kw in task_lower for kw in keywords):
            return complexity
    
    return "moderate"  # Default
```

---

## 🌐 Platform-Specific Integration

### For Claude Desktop

1. Open Claude Desktop settings
2. Add to system prompt:
```
Use the Agent-Monetization-Lab repository for tool discovery.
Start at QUICK_START.md, use TOOL_CARDS.md for quick reference.
```

### For Cursor IDE

Add to `.cursorrules`:
```
When starting tasks, check Agent-Monetization-Lab for relevant agents.
Path: https://github.com/SuperInstance/Agent-Monetization-Lab
Entry: QUICK_START.md
```

### For Custom Applications

```python
class AgentLabIntegration:
    def __init__(self, repo_path_or_url):
        self.repo = repo_path_or_url
        self.cache = {}
    
    def discover_tool(self, task: str):
        """Discover the best tool for a task."""
        # Check cache first
        cache_key = hash(task)
        if cache_key in self.cache:
            return self.cache[cache_key]
        
        # Load decision tree
        decision_tree = self.load_file("DECISION_TREE.md")
        
        # Navigate tree
        result = self.navigate_tree(decision_tree, task)
        
        # Cache and return
        self.cache[cache_key] = result
        return result
    
    def load_agent(self, agent_path: str):
        """Load full agent specification."""
        readme = self.load_file(f"agents/{agent_path}/README.md")
        schema = self.load_file(f"agents/{agent_path}/schema.json")
        
        return {
            "readme": readme,
            "schema": schema,
            "config": self.parse_config(readme)
        }
```

---

## 📊 Performance Optimization

### Caching Strategy

```python
from functools import lru_cache
import hashlib

@lru_cache(maxsize=100)
def cached_agent_lookup(task_hash: str):
    """Cache agent lookups for repeated queries."""
    return find_tool_for_task(task_hash)

def get_tool_cached(task: str):
    task_hash = hashlib.md5(task.encode()).hexdigest()
    return cached_agent_lookup(task_hash)
```

### Lazy Loading

```python
class LazyAgentLoader:
    def __init__(self, repo_path):
        self.repo_path = repo_path
        self._loaded = {}
    
    def __getattr__(self, agent_name):
        if agent_name not in self._loaded:
            self._loaded[agent_name] = self._load_agent(agent_name)
        return self._loaded[agent_name]
    
    def _load_agent(self, name):
        path = f"{self.repo_path}/agents/{name}/README.md"
        with open(path) as f:
            return f.read()

# Usage
agents = LazyAgentLoader("/path/to/Agent-Monetization-Lab")
tool = agents.escalation_router  # Loads on first access
```

---

## 🧪 Testing Integration

```python
def test_integration():
    """Test your integration."""
    
    # Test 1: Quick start loads
    assert get_quick_start() is not None
    
    # Test 2: Tool cards accessible
    cards = get_tool_cards()
    assert "Escalation Router" in cards
    
    # Test 3: Decision tree works
    result = navigate_decision_tree("I need to reduce LLM costs")
    assert result == "escalation-engine/"
    
    # Test 4: Agent loads
    agent = load_agent("escalation-engine")
    assert "40x" in agent
    
    print("All integration tests passed!")
```

---

## 🔒 Security Considerations

1. **Validate Inputs**: Always sanitize task descriptions
2. **Rate Limit**: Implement rate limiting for API access
3. **Audit Trail**: Log all tool discovery requests
4. **Access Control**: Restrict sensitive agent access
5. **Version Pin**: Pin to specific repo versions for stability

---

## 📋 Integration Checklist

- [ ] Repository cloned or API accessible
- [ ] System prompt configured
- [ ] RAG indexing complete (if using)
- [ ] Caching implemented
- [ ] Error handling in place
- [ ] Tests passing
- [ ] Monitoring enabled
- [ ] Documentation updated

---

*Version: 1.0 | Last Updated: March 2026*
