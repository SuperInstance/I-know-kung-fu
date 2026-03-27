# Dify Platform Guide

## Overview

Dify is an open-source agentic workflow builder that enables development, deployment, and management of autonomous agents, RAG pipelines, and AI applications at scale. It's particularly popular for teams building production AI applications.

## Platform Characteristics

| Aspect | Details |
|--------|---------|
| Type | Open-source platform |
| Self-hosted | Yes |
| Cloud | Available |
| Best for | Teams building AI apps |
| Complexity | Medium |

## Key Features

1. **Visual Workflow Builder** - Drag-and-drop agent design
2. **Agent Nodes** - LLM with autonomous tool control
3. **RAG Pipeline** - Retrieval-augmented generation
4. **Multi-Model Support** - Various LLM backends
5. **Knowledge Management** - Built-in vector stores
6. **API Access** - RESTful API for integration

## Agent Types Supported

### Chatbot Agents
Conversational AI with context management

### Workflow Agents
Multi-step automated processes

### RAG Agents
Knowledge-grounded responses

### Tool-Using Agents
Agents with external tool access

## Agent Specification Format

```yaml
app:
  name: "Document Processor"
  description: "Process and analyze documents"
  mode: "agent"
  
agent:
  model: "gpt-4"
  tools:
    - name: "document_reader"
      type: "builtin"
    - name: "web_search"
      type: "builtin"
    - name: "custom_analyzer"
      type: "api"
      config:
        endpoint: "https://api.example.com/analyze"
  
  prompt:
    system: |
      You are a document analysis expert.
      Process documents thoroughly and provide structured insights.
      
  memory:
    type: "conversation"
    window: 10
    
knowledge:
  - name: "company_docs"
    type: "vector_store"
    embedding: "text-embedding-3-small"
```

## Creating Agents

### Via Web Interface
1. Create new application
2. Select agent mode
3. Configure model and tools
4. Design prompt
5. Add knowledge bases
6. Test and deploy

### Via API
```python
import requests

response = requests.post(
    "https://api.dify.ai/v1/apps",
    headers={"Authorization": "Bearer YOUR_API_KEY"},
    json={
        "name": "My Agent",
        "mode": "agent",
        "model_config": {
            "model": "gpt-4",
            "temperature": 0.7
        },
        "tools": ["web_search", "document_reader"]
    }
)
```

## Tool Integration

### Built-in Tools
- Web Search
- Document Reader
- Calculator
- Code Interpreter
- Image Generator

### Custom Tools
```json
{
  "name": "custom_api",
  "type": "api",
  "config": {
    "endpoint": "https://your-api.com/endpoint",
    "method": "POST",
    "headers": {
      "Authorization": "Bearer ${API_KEY}"
    },
    "request_body": {
      "query": "${input}"
    }
  }
}
```

## Knowledge Base Setup

```python
# Create knowledge base
knowledge = dify.knowledge.create(
    name="Company Documents",
    embedding_model="text-embedding-3-small"
)

# Add documents
knowledge.add_documents([
    {"content": "Document content...", "metadata": {"source": "policy.pdf"}},
    {"content": "More content...", "metadata": {"source": "guide.pdf"}}
])
```

## Monetization Strategy

### Self-Hosted
- Free to use
- Pay for compute/LLM costs
- Full control over data

### Cloud Version
- Pay-per-use model
- Managed infrastructure
- Team collaboration features

### Selling Agents
1. Build useful agent
2. Package as template
3. Share publicly or sell access
4. Charge for API usage

## Integration Examples

### LangChain Integration
```python
from langchain.agents import DifyAgent

agent = DifyAgent(
    dify_api_key="your-key",
    app_id="your-app-id"
)

result = agent.run("Analyze this document")
```

### n8n Integration
```json
{
  "nodes": [
    {
      "type": "dify",
      "operation": "runAgent",
      "appId": "your-app-id",
      "input": "={{$json.query}}"
    }
  ]
}
```

## Pricing Comparison

| Plan | Price | Features |
|------|-------|----------|
| Free (Self-hosted) | $0 | Full features, self-managed |
| Sandbox | $0 | Limited usage, cloud |
| Pro | $59/mo | Production usage |
| Team | $159/mo | Collaboration features |
| Enterprise | Custom | Full enterprise features |

## Best Practices

1. **Start Simple** - Begin with basic agent, add complexity
2. **Test Thoroughly** - Use built-in testing tools
3. **Monitor Costs** - Track LLM usage
4. **Version Control** - Export and version configurations
5. **Document Prompts** - Comment your prompt designs

## Related Platform Links

- Official Site: https://dify.ai
- Documentation: https://docs.dify.ai
- GitHub: https://github.com/langgenius/dify
- Community: Discord

## Agents We Recommend for Dify

1. **Document Processor** - `platforms/minimax-experts/document-processor/`
2. **Research Assistant** - `platforms/minimax-experts/research-assistant/`
3. **Customer Support** - `platforms/mindstudio/customer-support-agent/`
4. **Knowledge Extractor** - `agents/knowledge-management/knowledge-extractor/`
