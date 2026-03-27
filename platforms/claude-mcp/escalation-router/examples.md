# Escalation Router - Usage Examples

## Basic Usage

### Example 1: Simple Query Routing

**Tool Call:**
```json
{
  "name": "route_query",
  "arguments": {
    "query": "What is the capital of France?"
  }
}
```

**Response:**
```json
{
  "result": "The capital of France is Paris.",
  "routing": {
    "classifiedTier": 1,
    "selectedModel": "gpt-3.5-turbo",
    "confidence": 0.98,
    "reasoning": "Simple factual query requiring no complex reasoning"
  },
  "metrics": {
    "classificationTime": 12,
    "executionTime": 234,
    "totalTime": 246,
    "tokensUsed": 18,
    "cost": 0.000009
  }
}
```

**Savings Analysis:**
- Routed to Tier 1 ($0.0005/1K tokens) vs Tier 4 ($0.03/1K tokens)
- **Cost savings: 98%**

---

### Example 2: Code Generation Task

**Tool Call:**
```json
{
  "name": "route_query",
  "arguments": {
    "query": "Write a Python function that calculates the Fibonacci sequence using memoization",
    "constraints": {
      "minQuality": "high"
    }
  }
}
```

**Response:**
```json
{
  "result": "```python\ndef fibonacci(n, memo={}):\n    \"\"\"Calculate the nth Fibonacci number using memoization.\"\"\"\n    if n in memo:\n        return memo[n]\n    if n <= 1:\n        return n\n    memo[n] = fibonacci(n-1, memo) + fibonacci(n-2, memo)\n    return memo[n]\n```\n\nThis implementation uses a dictionary to cache previously computed values, reducing time complexity from O(2^n) to O(n).",
  "routing": {
    "classifiedTier": 3,
    "selectedModel": "claude-3-sonnet",
    "confidence": 0.92,
    "reasoning": "Code generation with specific requirements requires mid-tier model"
  },
  "metrics": {
    "classificationTime": 18,
    "executionTime": 892,
    "totalTime": 910,
    "tokensUsed": 187,
    "cost": 0.00112
  }
}
```

---

### Example 3: Complex Analysis (Forced Escalation)

**Tool Call:**
```json
{
  "name": "route_query",
  "arguments": {
    "query": "Analyze the legal implications of using AI-generated content in commercial applications under current EU regulations",
    "forceTier": 4
  }
}
```

**Response:**
```json
{
  "result": "## Legal Analysis: AI-Generated Content in EU Commercial Applications\n\n### Regulatory Framework\n\nUnder the EU AI Act (2024), AI-generated content used commercially falls under several regulatory categories:\n\n**1. Transparency Requirements**\n- Article 52 requires disclosure when users interact with AI systems\n- Generated content must be labeled as AI-created in many contexts\n\n**2. Copyright Considerations**\n- The Copyright Directive (2019/790) implications:\n  - AI training data compliance\n  - Originality requirements for copyright protection\n  - Current CJEU precedents suggest AI outputs may not qualify for copyright\n\n**3. Liability Framework**\n- Product Liability Directive implications for AI-generated outputs\n- GDPR considerations for personal data in training sets\n\n### Recommendations\n\n1. **Implement Clear Labeling**: All AI-generated content should be clearly marked\n2. **Document Training Data**: Maintain records of training data sources\n3. **Human Oversight**: Establish review processes for sensitive content\n4. **Regular Compliance Audits**: Schedule quarterly reviews of AI practices\n\n### Risk Assessment\n\n| Risk Area | Level | Mitigation Priority |\n|-----------|-------|---------------------|\n| Transparency | Medium | High |\n| Copyright | High | Critical |\n| Liability | Medium | Medium |\n| Data Protection | High | Critical |",
  "routing": {
    "classifiedTier": 4,
    "selectedModel": "claude-3-opus",
    "confidence": 0.95,
    "reasoning": "Forced escalation - complex legal analysis requiring expert-level reasoning"
  },
  "metrics": {
    "classificationTime": 15,
    "executionTime": 4230,
    "totalTime": 4245,
    "tokensUsed": 847,
    "cost": 0.02541
  }
}
```

---

## Classification Examples

### Example 4: Query Classification Only

**Tool Call:**
```json
{
  "name": "classify_query",
  "arguments": {
    "query": "Translate 'Hello, how are you?' to Spanish",
    "includeReasoning": true
  }
}
```

**Response:**
```json
{
  "classification": {
    "recommendedTier": 2,
    "recommendedModel": "gpt-4o-mini",
    "confidence": 0.94
  },
  "reasoning": {
    "taskType": "translation",
    "complexity": "low",
    "contextRequired": false,
    "reasoningNeeded": false,
    "factors": [
      "Simple, well-defined translation task",
      "No ambiguous terms or idioms",
      "Common language pair (English-Spanish)",
      "Short input length"
    ]
  },
  "alternatives": [
    {
      "tier": 1,
      "model": "gpt-3.5-turbo",
      "confidence": 0.75,
      "tradeoffs": "Slightly lower translation quality for idiomatic expressions"
    },
    {
      "tier": 3,
      "model": "claude-3-sonnet",
      "confidence": 0.96,
      "tradeoffs": "Higher cost with marginal quality improvement"
    }
  ],
  "estimatedCost": {
    "tier2": 0.00012,
    "savingsVsTier4": "96%"
  }
}
```

---

## Statistics and Analytics

### Example 5: Getting Routing Statistics

**Tool Call:**
```json
{
  "name": "get_routing_stats",
  "arguments": {
    "period": "7d",
    "groupBy": "tier"
  }
}
```

**Response:**
```json
{
  "period": "7d",
  "summary": {
    "totalQueries": 12543,
    "totalCost": 23.47,
    "averageLatency": 342,
    "cacheHitRate": 0.34
  },
  "tierDistribution": [
    {
      "tier": 1,
      "count": 6234,
      "percentage": 49.7,
      "avgLatency": 187,
      "avgCost": 0.00008
    },
    {
      "tier": 2,
      "count": 3756,
      "percentage": 29.9,
      "avgLatency": 412,
      "avgCost": 0.00034
    },
    {
      "tier": 3,
      "count": 2124,
      "percentage": 16.9,
      "avgLatency": 823,
      "avgCost": 0.00212
    },
    {
      "tier": 4,
      "count": 429,
      "percentage": 3.4,
      "avgLatency": 2341,
      "avgCost": 0.01876
    }
  ],
  "savings": {
    "costIfAlwaysTopTier": 941.23,
    "actualCost": 23.47,
    "savings": 917.76,
    "savingsPercentage": 97.5,
    "savingsMultiple": "40x"
  },
  "modelUsage": [
    {"model": "gpt-3.5-turbo", "calls": 5234, "cost": 4.23},
    {"model": "gpt-4o-mini", "calls": 3756, "cost": 3.45},
    {"model": "claude-3-sonnet", "calls": 2124, "cost": 8.12},
    {"model": "claude-3-opus", "calls": 389, "cost": 7.67}
  ]
}
```

---

## Custom Rules

### Example 6: Adding a Custom Routing Rule

**Tool Call:**
```json
{
  "name": "add_custom_rule",
  "arguments": {
    "name": "support-tickets",
    "pattern": "(?i)(ticket|support|help\\s*desk|customer\\s*service)",
    "targetTier": 2,
    "priority": 150
  }
}
```

**Response:**
```json
{
  "success": true,
  "rule": {
    "id": "rule_abc123",
    "name": "support-tickets",
    "pattern": "(?i)(ticket|support|help\\s*desk|customer\\s*service)",
    "targetTier": 2,
    "priority": 150,
    "createdAt": "2024-01-15T10:30:00Z"
  },
  "message": "Custom routing rule 'support-tickets' created successfully. Queries matching this pattern will be routed to Tier 2."
}
```

### Example 7: Rule in Action

**Tool Call:**
```json
{
  "name": "route_query",
  "arguments": {
    "query": "I need help with my support ticket #12345"
  }
}
```

**Response:**
```json
{
  "result": "I'd be happy to help you with your support ticket #12345. Could you please provide more details about the issue you're experiencing?",
  "routing": {
    "classifiedTier": 2,
    "selectedModel": "gpt-4o-mini",
    "confidence": 1.0,
    "matchedRule": "support-tickets",
    "reasoning": "Matched custom rule 'support-tickets' (priority 150)"
  },
  "metrics": {
    "classificationTime": 5,
    "executionTime": 312,
    "totalTime": 317,
    "tokensUsed": 34,
    "cost": 0.00012
  }
}
```

---

## Caching

### Example 8: Cache Lookup

**Tool Call:**
```json
{
  "name": "cache_lookup",
  "arguments": {
    "query": "What is the capital of France?",
    "fuzzyMatch": true
  }
}
```

**Response:**
```json
{
  "found": true,
  "cachedResponse": "The capital of France is Paris.",
  "similarity": 1.0,
  "cachedAt": "2024-01-15T09:45:00Z",
  "originalQuery": "What is the capital of France?"
}
```

### Example 9: Cache Invalidation

**Tool Call:**
```json
{
  "name": "cache_invalidate",
  "arguments": {
    "pattern": "capital of.*"
  }
}
```

**Response:**
```json
{
  "success": true,
  "invalidatedCount": 47,
  "message": "Invalidated 47 cache entries matching pattern 'capital of.*'"
}
```

---

## Cost Estimation

### Example 10: Pre-Query Cost Estimate

**Tool Call:**
```json
{
  "name": "get_cost_estimate",
  "arguments": {
    "query": "Write a comprehensive 2000-word analysis of the economic impact of AI on the healthcare industry",
    "includeComparison": true
  }
}
```

**Response:**
```json
{
  "estimate": {
    "recommendedTier": 4,
    "estimatedTokens": 3500,
    "estimatedCost": 0.105
  },
  "comparison": [
    {
      "tier": 1,
      "model": "gpt-3.5-turbo",
      "estimatedCost": 0.00175,
      "qualityScore": 45,
      "suitable": false,
      "reason": "Task requires complex analysis and extended output"
    },
    {
      "tier": 2,
      "model": "gpt-4o-mini",
      "estimatedCost": 0.00525,
      "qualityScore": 72,
      "suitable": "partial",
      "reason": "Can handle but may lack depth in analysis"
    },
    {
      "tier": 3,
      "model": "claude-3-sonnet",
      "estimatedCost": 0.0315,
      "qualityScore": 88,
      "suitable": true,
      "reason": "Good balance of quality and cost for this task"
    },
    {
      "tier": 4,
      "model": "claude-3-opus",
      "estimatedCost": 0.105,
      "qualityScore": 96,
      "suitable": true,
      "reason": "Highest quality output for comprehensive analysis"
    }
  ],
  "recommendation": "Consider Tier 3 (claude-3-sonnet) for excellent quality at 70% lower cost than Tier 4"
}
```

---

## Strategy Configuration

### Example 11: Setting Routing Strategy

**Tool Call:**
```json
{
  "name": "set_routing_strategy",
  "arguments": {
    "strategy": "custom",
    "customWeights": {
      "cost": 0.5,
      "latency": 0.3,
      "quality": 0.2
    }
  }
}
```

**Response:**
```json
{
  "success": true,
  "strategy": {
    "type": "custom",
    "weights": {
      "cost": 0.5,
      "latency": 0.3,
      "quality": 0.2
    }
  },
  "message": "Custom routing strategy configured. Queries will be routed optimizing for 50% cost, 30% latency, 20% quality."
}
```

---

## Model Tier Information

### Example 12: Getting Available Tiers

**Tool Call:**
```json
{
  "name": "get_model_tiers",
  "arguments": {
    "includeModels": true,
    "includePricing": true
  }
}
```

**Response:**
```json
{
  "tiers": [
    {
      "tier": 1,
      "name": "Simple/Fast",
      "models": [
        {"name": "gpt-3.5-turbo", "provider": "openai"},
        {"name": "claude-3-haiku", "provider": "anthropic"}
      ],
      "pricing": {
        "inputPerMillion": 0.50,
        "outputPerMillion": 1.50
      },
      "capabilities": ["simple-qa", "math", "formatting", "short-translations"],
      "avgLatency": 150
    },
    {
      "tier": 2,
      "name": "Moderate",
      "models": [
        {"name": "gpt-4o-mini", "provider": "openai"}
      ],
      "pricing": {
        "inputPerMillion": 0.15,
        "outputPerMillion": 0.60
      },
      "capabilities": ["summarization", "translation", "code-review", "simple-writing"],
      "avgLatency": 350
    },
    {
      "tier": 3,
      "name": "Complex",
      "models": [
        {"name": "gpt-4-turbo", "provider": "openai"},
        {"name": "claude-3-sonnet", "provider": "anthropic"}
      ],
      "pricing": {
        "inputPerMillion": 10.00,
        "outputPerMillion": 30.00
      },
      "capabilities": ["analysis", "writing", "reasoning", "code-generation"],
      "avgLatency": 800
    },
    {
      "tier": 4,
      "name": "Expert",
      "models": [
        {"name": "gpt-4", "provider": "openai"},
        {"name": "claude-3-opus", "provider": "anthropic"}
      ],
      "pricing": {
        "inputPerMillion": 30.00,
        "outputPerMillion": 60.00
      },
      "capabilities": ["expert-analysis", "complex-reasoning", "creative-writing", "legal-medical"],
      "avgLatency": 2500
    }
  ],
  "providerSupport": {
    "openai": 4,
    "anthropic": 3,
    "local": 0
  }
}
```

---

## Error Handling

### Example 13: Handling Budget Exceeded

**Tool Call:**
```json
{
  "name": "route_query",
  "arguments": {
    "query": "Complex analysis query...",
    "constraints": {
      "maxCost": 0.001
    }
  }
}
```

**Response (when budget exceeded):**
```json
{
  "error": {
    "code": "BUDGET_EXCEEDED",
    "message": "Query would exceed specified budget",
    "details": {
      "requestedMaxCost": 0.001,
      "estimatedCost": 0.025,
      "suggestedTier": 2,
      "suggestedCost": 0.0008
    }
  },
  "alternatives": [
    {
      "tier": 2,
      "model": "gpt-4o-mini",
      "estimatedCost": 0.0008,
      "estimatedQualityDrop": "15%"
    },
    {
      "tier": 1,
      "model": "gpt-3.5-turbo",
      "estimatedCost": 0.0002,
      "estimatedQualityDrop": "35%"
    }
  ]
}
```
