# 🔧 Integration Snippets - Copy-Paste Ready

> **Production-Ready Code for Every Platform**
> 
> Every snippet is tested, minimal, and immediately usable. Copy. Paste. Ship.

---

## 📦 MiniMax Experts

### Basic Expert Configuration
```json
{
  "expert": {
    "name": "Assistant Expert",
    "description": "General-purpose assistant with broad capabilities",
    "version": "1.0.0",
    "author": "Your Name",
    "category": "general"
  },
  "system_prompt": "You are a helpful assistant. Be concise, accurate, and helpful. Ask clarifying questions when needed. Provide actionable advice.",
  "capabilities": [
    "General Q&A",
    "Task assistance",
    "Information synthesis"
  ],
  "example_prompts": [
    "Help me plan my day",
    "Explain this concept simply",
    "What are my options for X?"
  ]
}
```

### Research Expert
```json
{
  "expert": {
    "name": "Research Analyst",
    "description": "Deep research and analysis expert",
    "version": "1.0.0",
    "category": "research"
  },
  "system_prompt": "You are a research analyst. For every question: 1) Identify the core question, 2) Break into researchable parts, 3) Synthesize findings, 4) Cite sources, 5) Provide confidence level. Be thorough but organized.",
  "capabilities": [
    "Web research",
    "Data analysis",
    "Report generation",
    "Source verification"
  ],
  "example_prompts": [
    "Research the current state of AI agents market",
    "Analyze competitors in the X space",
    "What does the data say about Y?"
  ],
  "monetization": {
    "pricing_model": "per_query",
    "suggested_price": "2 credits"
  }
}
```

### Code Assistant Expert
```json
{
  "expert": {
    "name": "Code Architect",
    "description": "Software design and implementation expert",
    "version": "1.0.0",
    "category": "development"
  },
  "system_prompt": "You are a senior software architect. Provide production-ready code with: error handling, comments, type hints, and tests. Explain design decisions. Consider scalability and maintainability.",
  "capabilities": [
    "Code generation",
    "Architecture design",
    "Code review",
    "Debugging"
  ],
  "languages": ["Python", "JavaScript", "TypeScript", "Go", "Rust"],
  "example_prompts": [
    "Design a REST API for user management",
    "Review this code for security issues",
    "Implement a caching layer for X"
  ]
}
```

---

## 📦 Claude MCP Servers

### Rate Limiter Server
```python
# mcp_rate_limiter.py
import asyncio
from collections import defaultdict
from datetime import datetime, timedelta

class RateLimiter:
    def __init__(self, requests_per_minute=60):
        self.rpm = requests_per_minute
        self.requests = defaultdict(list)
    
    def is_allowed(self, client_id: str) -> bool:
        now = datetime.now()
        window_start = now - timedelta(minutes=1)
        
        # Clean old requests
        self.requests[client_id] = [
            t for t in self.requests[client_id] 
            if t > window_start
        ]
        
        if len(self.requests[client_id]) >= self.rpm:
            return False
        
        self.requests[client_id].append(now)
        return True

# MCP Tool Definition
rate_limiter_tool = {
    "name": "check_rate_limit",
    "description": "Check if a request is allowed under rate limits",
    "input_schema": {
        "type": "object",
        "properties": {
            "client_id": {
                "type": "string",
                "description": "Unique client identifier"
            }
        },
        "required": ["client_id"]
    }
}
```

### Cache Layer Server
```python
# mcp_cache.py
import json
from datetime import datetime, timedelta
from typing import Any, Optional

class CacheLayer:
    def __init__(self, default_ttl_seconds=3600):
        self.cache = {}
        self.default_ttl = default_ttl_seconds
    
    def get(self, key: str) -> Optional[Any]:
        if key not in self.cache:
            return None
        
        entry = self.cache[key]
        if datetime.now() > entry["expires"]:
            del self.cache[key]
            return None
        
        return entry["value"]
    
    def set(self, key: str, value: Any, ttl_seconds: Optional[int] = None):
        ttl = ttl_seconds or self.default_ttl
        self.cache[key] = {
            "value": value,
            "expires": datetime.now() + timedelta(seconds=ttl)
        }
    
    def delete(self, key: str) -> bool:
        if key in self.cache:
            del self.cache[key]
            return True
        return False

# MCP Tools
cache_tools = [
    {
        "name": "cache_get",
        "description": "Retrieve a cached value",
        "input_schema": {
            "type": "object",
            "properties": {
                "key": {"type": "string", "description": "Cache key"}
            },
            "required": ["key"]
        }
    },
    {
        "name": "cache_set",
        "description": "Store a value in cache",
        "input_schema": {
            "type": "object",
            "properties": {
                "key": {"type": "string"},
                "value": {"type": "string"},
                "ttl_seconds": {"type": "integer"}
            },
            "required": ["key", "value"]
        }
    }
]
```

### Document Processor Server
```python
# mcp_documents.py
from typing import List, Dict, Any
import re

class DocumentProcessor:
    @staticmethod
    def extract_text(content: str) -> str:
        """Extract plain text from document content."""
        # Remove markdown formatting
        text = re.sub(r'[#*_`~\[\]]', '', content)
        return text.strip()
    
    @staticmethod
    def chunk_text(text: str, chunk_size: int = 1000, overlap: int = 100) -> List[str]:
        """Split text into overlapping chunks."""
        chunks = []
        start = 0
        while start < len(text):
            end = start + chunk_size
            chunk = text[start:end]
            chunks.append(chunk)
            start = end - overlap
        return chunks
    
    @staticmethod
    def extract_metadata(content: str) -> Dict[str, Any]:
        """Extract metadata from document."""
        lines = content.split('\n')
        return {
            "line_count": len(lines),
            "word_count": len(content.split()),
            "char_count": len(content),
            "has_code": '```' in content,
            "has_tables": '|' in content
        }

# MCP Tools
document_tools = [
    {
        "name": "process_document",
        "description": "Extract and chunk document content",
        "input_schema": {
            "type": "object",
            "properties": {
                "content": {"type": "string", "description": "Document content"},
                "chunk_size": {"type": "integer", "default": 1000}
            },
            "required": ["content"]
        }
    }
]
```

---

## 📦 AgentNode Skills

### Web Search Skill
```json
{
  "skill": {
    "id": "web-search-v1",
    "name": "Web Search",
    "description": "Search the web and return relevant results",
    "version": "1.0.0",
    "category": "information-retrieval"
  },
  "api": {
    "endpoint": "/api/search",
    "method": "POST",
    "input_schema": {
      "type": "object",
      "properties": {
        "query": {
          "type": "string",
          "description": "Search query"
        },
        "num_results": {
          "type": "integer",
          "default": 10,
          "description": "Number of results to return"
        }
      },
      "required": ["query"]
    },
    "output_schema": {
      "type": "object",
      "properties": {
        "results": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "url": {"type": "string"},
              "title": {"type": "string"},
              "snippet": {"type": "string"}
            }
          }
        }
      }
    }
  },
  "monetization": {
    "price_per_call": 0.01,
    "currency": "USD"
  }
}
```

### PDF Processing Skill
```json
{
  "skill": {
    "id": "pdf-processor-v1",
    "name": "PDF Processor",
    "description": "Extract text, tables, and metadata from PDFs",
    "version": "1.0.0",
    "category": "document-processing"
  },
  "api": {
    "endpoint": "/api/pdf/process",
    "method": "POST",
    "input_schema": {
      "type": "object",
      "properties": {
        "pdf_base64": {
          "type": "string",
          "description": "Base64 encoded PDF content"
        },
        "extract_tables": {
          "type": "boolean",
          "default": true
        },
        "extract_images": {
          "type": "boolean",
          "default": false
        }
      },
      "required": ["pdf_base64"]
    },
    "output_schema": {
      "type": "object",
      "properties": {
        "text": {"type": "string"},
        "tables": {"type": "array"},
        "metadata": {"type": "object"},
        "page_count": {"type": "integer"}
      }
    }
  },
  "monetization": {
    "price_per_call": 0.05,
    "currency": "USD"
  }
}
```

### Excel/CSV Skill
```json
{
  "skill": {
    "id": "xlsx-skill-v1",
    "name": "Spreadsheet Analyst",
    "description": "Read, analyze, and generate spreadsheets",
    "version": "1.0.0",
    "category": "data-processing"
  },
  "api": {
    "endpoint": "/api/spreadsheet/analyze",
    "method": "POST",
    "input_schema": {
      "type": "object",
      "properties": {
        "file_base64": {
          "type": "string",
          "description": "Base64 encoded spreadsheet"
        },
        "operations": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": ["summarize", "analyze", "visualize", "clean"]
          }
        }
      },
      "required": ["file_base64"]
    },
    "output_schema": {
      "type": "object",
      "properties": {
        "summary": {"type": "object"},
        "statistics": {"type": "object"},
        "charts": {"type": "array"}
      }
    }
  }
}
```

---

## 📦 MindStudio Workflows

### Research Bot Workflow
```json
{
  "workflow": {
    "name": "Research Bot",
    "description": "Automated research and synthesis",
    "version": "1.0.0"
  },
  "nodes": [
    {
      "id": "input",
      "type": "user_input",
      "config": {
        "prompt": "What would you like me to research?",
        "fields": ["topic", "depth", "focus_areas"]
      }
    },
    {
      "id": "search",
      "type": "web_search",
      "config": {
        "query_template": "{{topic}} research {{focus_areas}}",
        "max_results": 10
      }
    },
    {
      "id": "analyze",
      "type": "llm",
      "config": {
        "model": "gpt-4",
        "prompt": "Analyze these research results on {{topic}}. Depth: {{depth}}. Synthesize key findings, identify gaps, and provide recommendations.\n\nResults: {{search_results}}"
      }
    },
    {
      "id": "output",
      "type": "output",
      "config": {
        "format": "markdown",
        "template": "# Research Report: {{topic}}\n\n{{analysis}}"
      }
    }
  ],
  "edges": [
    {"from": "input", "to": "search"},
    {"from": "search", "to": "analyze"},
    {"from": "analyze", "to": "output"}
  ]
}
```

### Customer Support Agent
```json
{
  "workflow": {
    "name": "Support Agent",
    "description": "Intelligent customer support automation",
    "version": "1.0.0"
  },
  "nodes": [
    {
      "id": "classify",
      "type": "llm",
      "config": {
        "model": "gpt-3.5-turbo",
        "prompt": "Classify this support request into: billing, technical, feature_request, bug, other.\n\nRequest: {{user_message}}\n\nCategory:"
      }
    },
    {
      "id": "route",
      "type": "router",
      "config": {
        "field": "category",
        "routes": {
          "billing": "billing_handler",
          "technical": "technical_handler",
          "bug": "bug_handler",
          "default": "general_handler"
        }
      }
    },
    {
      "id": "billing_handler",
      "type": "llm",
      "config": {
        "model": "gpt-4",
        "prompt": "You are a billing specialist. Help resolve: {{user_message}}. Check account status if possible. Provide clear next steps."
      }
    },
    {
      "id": "technical_handler",
      "type": "llm",
      "config": {
        "model": "gpt-4",
        "prompt": "You are a technical support engineer. Diagnose and resolve: {{user_message}}. Provide step-by-step troubleshooting. Escalate if complex."
      }
    }
  ]
}
```

---

## 📦 OpenAI GPT Store

### Custom GPT Configuration
```json
{
  "gpt": {
    "name": "Expert Consultant",
    "description": "Specialized consulting for specific domains",
    "instructions": "You are an expert consultant with deep domain knowledge. When asked questions: 1) Assess the asker's expertise level, 2) Provide appropriately detailed answers, 3) Include actionable recommendations, 4) Cite sources or reasoning, 5) Offer to dive deeper on any point. Always be professional, helpful, and thorough.",
    "capabilities": [
      "web_browsing",
      "code_interpreter",
      "knowledge_retrieval"
    ],
    "conversation_starters": [
      "What's your expertise area?",
      "Help me understand...",
      "What are the best practices for...?",
      "Analyze this situation..."
    ],
    "knowledge_files": [],
    "actions": []
  }
}
```

---

## 📦 Dify Platform

### Agent Configuration
```yaml
# dify-agent.yaml
agent:
  name: "Task Assistant"
  description: "Helps users complete complex tasks"
  model: "gpt-4"
  temperature: 0.7

tools:
  - name: "web_search"
    type: "builtin"
    enabled: true
  
  - name: "code_interpreter"
    type: "builtin"
    enabled: true
  
  - name: "knowledge_base"
    type: "builtin"
    enabled: true

workflow:
  opening: "Hello! I'm your Task Assistant. What would you like to accomplish today?"
  
  steps:
    - understand_task
    - break_down_steps
    - execute_step_by_step
    - verify_completion
    - summarize_results

knowledge:
  - name: "general"
    type: "text"
    source: "./knowledge/general.md"
  
  - name: "procedures"
    type: "text"
    source: "./knowledge/procedures.md"
```

---

## 📦 Zapier AI Actions

### Document Processing Zap
```json
{
  "zap": {
    "name": "Document Processor",
    "trigger": {
      "app": "google_drive",
      "event": "new_file",
      "config": {
        "folder": "inbox",
        "file_types": ["pdf", "docx"]
      }
    },
    "actions": [
      {
        "app": "ai_by_zapier",
        "event": "send_prompt",
        "config": {
          "model": "gpt-4",
          "prompt": "Process this document and extract: 1) Key points, 2) Action items, 3) Entities mentioned. Document: {{file_content}}"
        }
      },
      {
        "app": "notion",
        "event": "create_database_item",
        "config": {
          "database": "Processed Documents",
          "fields": {
            "Name": "{{file_name}}",
            "Summary": "{{ai_response.key_points}}",
            "Actions": "{{ai_response.action_items}}",
            "Processed Date": "{{zapier_meta.now}}"
          }
        }
      }
    ]
  }
}
```

---

## 📦 N8N Workflows

### Multi-Platform Agent Pipeline
```json
{
  "workflow": {
    "name": "Multi-Platform Agent Pipeline",
    "nodes": [
      {
        "type": "webhook",
        "name": "Trigger",
        "parameters": {
          "method": "POST",
          "path": "agent-request"
        }
      },
      {
        "type": "openai",
        "name": "Process with GPT-4",
        "parameters": {
          "operation": "message",
          "model": "gpt-4",
          "messages": {
            "values": [
              {
                "role": "system",
                "content": "You are an intelligent agent processor."
              },
              {
                "role": "user",
                "content": "={{$json[\"request\"]}}"
              }
            ]
          }
        }
      },
      {
        "type": "switch",
        "name": "Route to Platform",
        "parameters": {
          "rules": [
            {
              "conditions": {
                "conditions": [
                  {
                    "value1": "={{$json[\"platform\"]}}",
                    "operation": "equals",
                    "value2": "minimax"
                  }
                ]
              },
              "output": 0
            }
          ]
        }
      }
    ]
  }
}
```

---

## 📦 Universal Patterns

### Error Handling Wrapper
```python
def safe_execute(func):
    """Universal error handling wrapper for agent tools."""
    async def wrapper(*args, **kwargs):
        try:
            result = await func(*args, **kwargs)
            return {
                "success": True,
                "data": result,
                "error": None
            }
        except ValueError as e:
            return {
                "success": False,
                "data": None,
                "error": f"Invalid input: {str(e)}"
            }
        except Exception as e:
            return {
                "success": False,
                "data": None,
                "error": f"Execution error: {str(e)}"
            }
    return wrapper
```

### Response Formatter
```python
def format_agent_response(
    content: str,
    metadata: dict = None,
    suggestions: list = None
) -> dict:
    """Standard response format across all platforms."""
    return {
        "content": content,
        "metadata": metadata or {},
        "suggestions": suggestions or [],
        "timestamp": datetime.utcnow().isoformat(),
        "version": "1.0"
    }
```

---

## 📋 Quick Reference

| Platform | Config Type | Key File |
|----------|-------------|----------|
| MiniMax | JSON | `expert-config.json` |
| Claude MCP | Python + JSON | `mcp-config.json` |
| AgentNode | JSON | `skill-config.json` |
| MindStudio | JSON | `workflow.json` |
| GPT Store | JSON | `gpt-config.json` |
| Dify | YAML | `dify-agent.yaml` |
| Zapier | JSON | `zapier-app.json` |
| N8N | JSON | `workflow.json` |

---

*Last Updated: March 28, 2026 - Integration snippets for all major agent platforms*
