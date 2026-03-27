# Context Manager Agent

## Overview

The Context Manager agent optimizes context window usage to maximize the relevance of information included in prompts while staying within token limits.

## Core Concept

Context optimization:
1. **Token Budgeting** - Allocate tokens across sources
2. **Priority Ranking** - Rank context by relevance
3. **Compression** - Compress verbose content
4. **Dynamic Assembly** - Build optimal context
5. **Cache Management** - Cache frequently used context

## Skills

### Primary Skills
1. **Token Counting** - Accurate token counting
2. **Relevance Scoring** - Score context relevance
3. **Content Compression** - Summarize and compress
4. **Priority Management** - Handle priority conflicts
5. **Context Versioning** - Track context changes

### Secondary Skills
- Sliding window management
- Context deduplication
- Format optimization
- Cache strategies
- A/B testing context

## Use Cases

1. **Long Documents** - Fit long docs in context window
2. **Multi-Source Context** - Combine multiple sources
3. **Conversation History** - Manage chat history
4. **Code Context** - Include relevant code sections
5. **Research Synthesis** - Combine research findings

## Example Context Assembly

### Budget Allocation
```json
{
  "total_budget": 4096,
  "allocation": {
    "system_prompt": 200,
    "user_query": 100,
    "conversation_history": 1000,
    "retrieved_documents": 2000,
    "formatting_overhead": 196
  },
  "sources": [
    {"source": "history", "tokens_used": 950, "priority": "high"},
    {"source": "doc_1", "tokens_used": 800, "priority": "high"},
    {"source": "doc_2", "tokens_used": 600, "priority": "medium"},
    {"source": "doc_3", "tokens_used": 400, "priority": "low", "truncated": true}
  ]
}
```

### Compression Example
```json
{
  "original": "The quick brown fox jumps over the lazy dog. This classic pangram contains every letter of the English alphabet at least once. It has been used since the late 19th century for typing practice and font display.",
  "compressed": "Classic pangram 'quick brown fox...' contains all English letters, used for typing/fonts since 19th century.",
  "compression_ratio": 0.6,
  "information_retained": 0.95
}
```

## Configuration

```json
{
  "agent_type": "context-manager",
  "max_tokens": 4096,
  "compression_enabled": true,
  "compression_method": "extractive",
  "priority_levels": ["critical", "high", "medium", "low"],
  "cache_enabled": true,
  "cache_ttl": 3600,
  "deduplication": true
}
```

## Compression Strategies

### Extractive
Select important sentences:
```python
def extractive_compress(text, ratio=0.5):
    sentences = split_sentences(text)
    scores = score_importance(sentences)
    top_sentences = sorted(sentences, key=scores, reverse=True)
    return ' '.join(top_sentences[:int(len(sentences) * ratio)])
```

### Abstractive
Generate summary:
```python
def abstractive_compress(text, target_tokens):
    return llm.summarize(text, max_tokens=target_tokens)
```

### Semantic
Remove redundant information:
```python
def semantic_compress(chunks, similarity_threshold=0.9):
    unique_chunks = []
    for chunk in chunks:
        if not any(similarity(chunk, c) > similarity_threshold for c in unique_chunks):
            unique_chunks.append(chunk)
    return unique_chunks
```

## Performance Characteristics

| Metric | Value |
|--------|-------|
| Compression ratio | 40-60% |
| Information retention | 90-95% |
| Assembly time | 10-50ms |
| Token accuracy | 99%+ |

## Integration Points

- All LLM-based agents
- RAG pipelines
- Conversation systems
- Document processing

## Monetization Strategy

### Pricing Tiers
- **Basic**: $0.01/context assembly
- **Pro**: $0.03/context (with compression)
- **Enterprise**: $0.10/context (advanced optimization)

### Target Markets
1. Chat application developers
2. RAG system builders
3. Enterprise AI teams
4. Document processing services

## Related Agents

- `rag-pipeline/` - Context retrieval
- `context-compressor/` - Specialized compression
- `hierarchical-memory/` - Memory management
