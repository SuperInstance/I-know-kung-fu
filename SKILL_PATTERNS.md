# Skill Patterns Library

> **Reusable skill patterns for building consistent, high-quality agents.**

---

## 📚 Pattern Catalog

### Input Processing Patterns

| Pattern | Purpose | When To Use |
|---------|---------|-------------|
| [Input Validation](#input-validation) | Validate and sanitize inputs | All agents |
| [Input Normalization](#input-normalization) | Standardize input formats | Multi-format agents |
| [Input Enrichment](#input-enrichment) | Add context to inputs | Analysis agents |
| [Input Decomposition](#input-decomposition) | Split complex inputs | Multi-step agents |

### Processing Patterns

| Pattern | Purpose | When To Use |
|---------|---------|-------------|
| [Chain Processing](#chain-processing) | Sequential processing | Pipelines |
| [Parallel Processing](#parallel-processing) | Concurrent execution | Performance-critical |
| [Iterative Refinement](#iterative-refinement) | Improve over iterations | Quality-focused |
| [Conditional Branching](#conditional-branching) | Dynamic routing | Complex logic |

### Output Patterns

| Pattern | Purpose | When To Use |
|---------|---------|-------------|
| [Output Formatting](#output-formatting) | Structure outputs | All agents |
| [Output Validation](#output-validation) | Verify outputs | Quality-critical |
| [Output Transformation](#output-transformation) | Convert formats | Integration agents |
| [Streaming Output](#streaming-output) | Real-time delivery | Long processes |

### Resilience Patterns

| Pattern | Purpose | When To Use |
|---------|---------|-------------|
| [Error Recovery](#error-recovery) | Handle failures | All agents |
| [Caching](#caching) | Avoid redundant work | Repeated queries |
| [Rate Limiting](#rate-limiting) | Control throughput | API-dependent |
| [Circuit Breaker](#circuit-breaker) | Prevent cascading failures | External dependencies |

### Memory Patterns

| Pattern | Purpose | When To Use |
|---------|---------|-------------|
| [Short-term Memory](#short-term-memory) | Context within session | Conversations |
| [Long-term Memory](#long-term-memory) | Persistent storage | Learning agents |
| [Working Memory](#working-memory) | Active processing | Complex reasoning |
| [Episodic Memory](#episodic-memory) | Event sequences | Learning from history |

---

## 🔧 Pattern Specifications

### Input Validation

**Purpose**: Ensure inputs are valid, safe, and correctly formatted.

```json
{
  "pattern": "input_validation",
  "implementation": {
    "checks": [
      {
        "type": "type_check",
        "enabled": true,
        "strict": false
      },
      {
        "type": "format_check",
        "enabled": true,
        "formats": ["json", "text", "file"]
      },
      {
        "type": "range_check",
        "enabled": true,
        "min": null,
        "max": null
      },
      {
        "type": "sanitization",
        "enabled": true,
        "escape_html": true,
        "trim_whitespace": true
      }
    ],
    "on_failure": {
      "action": "reject",
      "message": "Invalid input: {reason}",
      "status_code": 400
    }
  }
}
```

**Example Usage**:
```python
def validate_input(data, schema):
    validator = InputValidator(schema)
    result = validator.validate(data)
    if not result.valid:
        return {"error": result.message, "status": 400}
    return {"data": result.sanitized, "status": 200}
```

---

### Input Normalization

**Purpose**: Convert varied input formats to a standard internal format.

```json
{
  "pattern": "input_normalization",
  "implementation": {
    "target_format": "json",
    "converters": {
      "csv": "csv_to_json",
      "xml": "xml_to_json",
      "yaml": "yaml_to_json",
      "text": "text_to_json"
    },
    "preserve_original": true,
    "metadata_fields": ["source_format", "conversion_time"]
  }
}
```

**Example Usage**:
```python
def normalize_input(raw_input, detected_format):
    normalizer = InputNormalizer()
    normalized = normalizer.convert(raw_input, detected_format)
    normalized["_meta"] = {
        "original_format": detected_format,
        "normalized_at": datetime.now().isoformat()
    }
    return normalized
```

---

### Input Enrichment

**Purpose**: Add contextual information to inputs before processing.

```json
{
  "pattern": "input_enrichment",
  "implementation": {
    "enrichments": [
      {
        "type": "timestamp",
        "field": "processing_time"
      },
      {
        "type": "user_context",
        "fields": ["user_id", "preferences", "history"]
      },
      {
        "type": "environment",
        "fields": ["timezone", "locale", "device"]
      },
      {
        "type": "derived",
        "calculations": ["sentiment_hint", "complexity_score"]
      }
    ]
  }
}
```

---

### Input Decomposition

**Purpose**: Split complex inputs into manageable components.

```json
{
  "pattern": "input_decomposition",
  "implementation": {
    "strategy": "semantic",
    "max_chunk_size": 1000,
    "overlap": 100,
    "preserve_context": true,
    "metadata": {
      "include_position": true,
      "include_chunk_id": true
    }
  }
}
```

---

### Chain Processing

**Purpose**: Process data through a sequence of steps.

```json
{
  "pattern": "chain_processing",
  "implementation": {
    "steps": [
      {"name": "extract", "agent": "extractor"},
      {"name": "transform", "agent": "transformer"},
      {"name": "validate", "agent": "validator"},
      {"name": "load", "agent": "loader"}
    ],
    "stop_on_failure": true,
    "checkpoint_frequency": "per_step",
    "rollback_enabled": true
  }
}
```

**Example Usage**:
```python
class ChainProcessor:
    def __init__(self, steps):
        self.steps = steps
        self.checkpoints = []
    
    def process(self, input_data):
        data = input_data
        for step in self.steps:
            try:
                data = step.agent.process(data)
                self.checkpoints.append({
                    "step": step.name,
                    "timestamp": datetime.now(),
                    "data": data
                })
            except Exception as e:
                if self.stop_on_failure:
                    return self.rollback()
                raise
        return data
```

---

### Parallel Processing

**Purpose**: Execute multiple tasks concurrently.

```json
{
  "pattern": "parallel_processing",
  "implementation": {
    "max_workers": 10,
    "timeout_per_task": 30,
    "aggregation_strategy": "merge",
    "error_handling": "continue_on_error",
    "progress_tracking": true
  }
}
```

---

### Iterative Refinement

**Purpose**: Improve output quality through iterations.

```json
{
  "pattern": "iterative_refinement",
  "implementation": {
    "max_iterations": 5,
    "stopping_criteria": {
      "quality_threshold": 0.9,
      "no_improvement_count": 2
    },
    "refinement_strategy": "critique_and_improve",
    "convergence_check": true
  }
}
```

**Example Usage**:
```python
def iterative_refine(initial_output, quality_threshold=0.9):
    output = initial_output
    for i in range(max_iterations):
        critique = critique_output(output)
        if critique.quality >= quality_threshold:
            break
        output = improve_output(output, critique)
    return output
```

---

### Conditional Branching

**Purpose**: Route processing based on conditions.

```json
{
  "pattern": "conditional_branching",
  "implementation": {
    "branches": [
      {
        "condition": "complexity > 0.8",
        "agent": "advanced_processor"
      },
      {
        "condition": "complexity <= 0.8 AND complexity > 0.5",
        "agent": "standard_processor"
      },
      {
        "condition": "complexity <= 0.5",
        "agent": "simple_processor"
      }
    ],
    "default_branch": "standard_processor",
    "condition_evaluation": "sequential"
  }
}
```

---

### Output Formatting

**Purpose**: Structure outputs consistently.

```json
{
  "pattern": "output_formatting",
  "implementation": {
    "format": "json",
    "schema": {
      "type": "object",
      "properties": {
        "result": {},
        "metadata": {},
        "confidence": {"type": "number"}
      }
    },
    "options": {
      "pretty_print": false,
      "include_nulls": false,
      "date_format": "iso8601",
      "number_precision": 4
    }
  }
}
```

---

### Output Validation

**Purpose**: Verify outputs meet quality standards.

```json
{
  "pattern": "output_validation",
  "implementation": {
    "validations": [
      {
        "type": "schema",
        "strict": true
      },
      {
        "type": "completeness",
        "required_fields": ["result", "confidence"]
      },
      {
        "type": "quality_score",
        "minimum": 0.7
      },
      {
        "type": "custom",
        "function": "validate_business_rules"
      }
    ],
    "on_failure": "retry_with_feedback"
  }
}
```

---

### Error Recovery

**Purpose**: Handle failures gracefully.

```json
{
  "pattern": "error_recovery",
  "implementation": {
    "strategies": [
      {
        "error_type": "timeout",
        "action": "retry",
        "max_retries": 3,
        "backoff": "exponential"
      },
      {
        "error_type": "validation_error",
        "action": "reject",
        "message": "Input validation failed"
      },
      {
        "error_type": "external_api_error",
        "action": "fallback",
        "fallback_agent": "cached_response"
      },
      {
        "error_type": "unknown",
        "action": "log_and_escalate"
      }
    ]
  }
}
```

---

### Caching

**Purpose**: Store results to avoid redundant processing.

```json
{
  "pattern": "caching",
  "implementation": {
    "enabled": true,
    "storage": "redis",
    "ttl_seconds": 3600,
    "key_strategy": {
      "type": "content_hash",
      "include": ["input", "configuration", "model_version"]
    },
    "eviction_policy": "lru",
    "max_entries": 10000,
    "cache_warming": false
  }
}
```

**Example Usage**:
```python
class CachedProcessor:
    def __init__(self, cache_client, processor):
        self.cache = cache_client
        self.processor = processor
    
    def process(self, input_data):
        cache_key = self.generate_key(input_data)
        
        # Check cache
        cached = self.cache.get(cache_key)
        if cached:
            return cached
        
        # Process and cache
        result = self.processor.process(input_data)
        self.cache.set(cache_key, result, ttl=3600)
        return result
```

---

### Rate Limiting

**Purpose**: Control request throughput.

```json
{
  "pattern": "rate_limiting",
  "implementation": {
    "enabled": true,
    "algorithm": "token_bucket",
    "limits": {
      "requests_per_second": 10,
      "requests_per_minute": 500,
      "requests_per_hour": 10000
    },
    "burst_allowance": 20,
    "on_limit_exceeded": {
      "action": "queue",
      "max_queue_size": 100,
      "queue_timeout": 60
    }
  }
}
```

---

### Circuit Breaker

**Purpose**: Prevent cascading failures.

```json
{
  "pattern": "circuit_breaker",
  "implementation": {
    "enabled": true,
    "failure_threshold": 5,
    "failure_window_seconds": 60,
    "open_duration_seconds": 30,
    "half_open_requests": 3,
    "on_open": {
      "action": "fallback",
      "fallback_response": "Service temporarily unavailable"
    }
  }
}
```

---

### Short-term Memory

**Purpose**: Maintain context within a session.

```json
{
  "pattern": "short_term_memory",
  "implementation": {
    "type": "sliding_window",
    "window_size": 10,
    "include_fields": ["user_input", "agent_response", "timestamp"],
    "summarization": {
      "enabled": true,
      "trigger_at": 8,
      "preserve_last": 3
    }
  }
}
```

---

### Long-term Memory

**Purpose**: Store information across sessions.

```json
{
  "pattern": "long_term_memory",
  "implementation": {
    "storage": "vector_database",
    "embedding_model": "text-embedding-3-small",
    "index_strategy": "similarity",
    "retention_policy": {
      "duration_days": 365,
      "max_entries": 100000
    },
    "privacy": {
      "user_isolation": true,
      "encryption": "aes-256"
    }
  }
}
```

---

### Working Memory

**Purpose**: Manage active processing state.

```json
{
  "pattern": "working_memory",
  "implementation": {
    "max_items": 7,
    "eviction_policy": "lru",
    "persistence": "session",
    "fields": {
      "current_task": {},
      "intermediate_results": {},
      "context": {}
    }
  }
}
```

---

## 🧩 Composite Patterns

### Reliable Processor (Composite)

Combines: Input Validation + Error Recovery + Caching + Output Validation

```json
{
  "composite_pattern": "reliable_processor",
  "patterns": [
    {"pattern": "input_validation", "priority": 1},
    {"pattern": "caching", "priority": 2},
    {"pattern": "error_recovery", "priority": 3},
    {"pattern": "output_validation", "priority": 4}
  ],
  "execution_order": "sequential"
}
```

### Resilient API Client (Composite)

Combines: Rate Limiting + Circuit Breaker + Caching + Error Recovery

```json
{
  "composite_pattern": "resilient_api_client",
  "patterns": [
    {"pattern": "rate_limiting", "priority": 1},
    {"pattern": "caching", "priority": 2},
    {"pattern": "circuit_breaker", "priority": 3},
    {"pattern": "error_recovery", "priority": 4}
  ]
}
```

---

## 📋 Pattern Selection Guide

```
AGENT TYPE → RECOMMENDED PATTERNS

Quick Task:
├── Input Validation
├── Output Formatting
└── Error Recovery

Reasoning Agent:
├── Input Validation
├── Working Memory
├── Iterative Refinement
└── Output Validation

Multi-Agent Orchestrator:
├── Input Decomposition
├── Parallel Processing
├── Short-term Memory
├── Error Recovery
└── Output Aggregation

Enterprise Suite:
├── All Input Patterns
├── All Processing Patterns
├── All Resilience Patterns
├── All Memory Patterns
└── All Output Patterns
```

---

*Patterns: 20+ | Version: 1.0 | Last Updated: March 2026*
