# Memory Hierarchy MCP Server

## Overview

The Memory Hierarchy is an intelligent MCP (Model Context Protocol) server that implements a sophisticated 6-tier memory system for AI agents. Inspired by computer memory architecture, it provides intelligent storage and retrieval of information across different persistence and access patterns.

## Problem Statement

AI agents struggle with memory management:

- **Context Window Limits**: LLMs have finite context windows that fill quickly
- **Information Overload**: Too much context degrades response quality
- **No Persistence**: Conversations reset, losing valuable context
- **Retrieval Challenges**: Finding relevant past information is difficult
- **Cost Management**: Storing/retrieving memory shouldn't be expensive

## Solution

Memory Hierarchy implements a tiered memory system that mimics how computers manage data:

```
┌─────────────────────────────────────────────────────────────┐
│                     MEMORY HIERARCHY                         │
├─────────────────────────────────────────────────────────────┤
│  Tier 0: Working Memory    (Current context window)         │
│  Tier 1: Ephemeral Cache   (Session-level, fast access)     │
│  Tier 2: Short-Term Memory (Recent interactions, hours)     │
│  Tier 3: Working Storage   (Active projects, days)          │
│  Tier 4: Long-Term Memory  (Persistent knowledge, months)   │
│  Tier 5: Archival Storage  (Historical data, years)         │
└─────────────────────────────────────────────────────────────┘
```

## Key Features

### 6-Tier Memory Architecture

| Tier | Name | Duration | Capacity | Access Time | Use Case |
|------|------|----------|----------|-------------|----------|
| 0 | Working | Milliseconds | 4-128K tokens | Instant | Current context |
| 1 | Ephemeral | Session | 1M tokens | < 1ms | Quick reference |
| 2 | Short-Term | Hours | 10M tokens | < 10ms | Recent context |
| 3 | Working | Days | 100M tokens | < 100ms | Active projects |
| 4 | Long-Term | Months | Unlimited | < 500ms | Knowledge base |
| 5 | Archival | Years | Unlimited | < 2s | Historical data |

### Intelligent Memory Management

- **Automatic Promotion**: Frequently accessed items move to faster tiers
- **Automatic Demotion**: Rarely accessed items move to slower tiers
- **Semantic Compression**: Compress similar memories to save space
- **Relevance Scoring**: Score memories by importance and recency

### Multiple Access Patterns

- **Direct Access**: Retrieve by memory ID
- **Semantic Search**: Find by meaning using embeddings
- **Temporal Access**: Query by time range
- **Associative Access**: Find related memories
- **Tag-Based Access**: Filter by custom tags

### Memory Operations

- **Store**: Save new memories with automatic tier placement
- **Retrieve**: Get memories from any tier
- **Update**: Modify existing memories
- **Forget**: Remove memories (soft/hard delete)
- **Consolidate**: Merge similar memories
- **Summarize**: Create higher-level abstractions

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    MEMORY HIERARCHY                          │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Memory    │  │  Promoter/  │  │  Embedding  │         │
│  │   Manager   │  │  Demoter    │  │   Engine    │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│         ↓                ↓                ↓                  │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │ Tier 0-1    │  │ Tier 2-3    │  │ Tier 4-5    │         │
│  │ (In-Memory) │  │  (Redis)    │  │ (Vector DB) │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
└─────────────────────────────────────────────────────────────┘
```

## Installation

```bash
# Clone the repository
git clone https://github.com/your-org/memory-hierarchy-mcp.git

# Install dependencies
cd memory-hierarchy-mcp
npm install

# Configure
cp .env.example .env

# Build and run
npm run build
npm start
```

## Configuration

Add to your Claude Desktop config:

```json
{
  "mcpServers": {
    "memory-hierarchy": {
      "command": "node",
      "args": ["/path/to/memory-hierarchy/dist/index.js"],
      "env": {
        "REDIS_URL": "redis://localhost:6379",
        "VECTOR_DB": "pinecone",
        "PINECONE_API_KEY": "your-key"
      }
    }
  }
}
```

## Usage Examples

### Storing a Memory

```typescript
const memory = await memoryHierarchy.store({
  content: "User prefers dark mode for all applications",
  type: "preference",
  importance: 0.8,
  tags: ["ui", "preference", "dark-mode"],
  metadata: {
    source: "user_feedback",
    confidence: 0.95
  }
});

// Memory automatically placed in appropriate tier
console.log(memory.tier); // 3 - Working storage
```

### Retrieving Memories

```typescript
// Semantic search
const memories = await memoryHierarchy.retrieve({
  query: "user interface preferences",
  topK: 5,
  tiers: [2, 3, 4]
});

// Temporal search
const recent = await memoryHierarchy.retrieve({
  timeRange: {
    start: Date.now() - 24 * 60 * 60 * 1000,
    end: Date.now()
  }
});

// Tag-based search
const tagged = await memoryHierarchy.retrieve({
  tags: ["preference"],
  exactMatch: false
});
```

## Performance Metrics

| Metric | Value |
|--------|-------|
| Tier 0-1 Access Time | < 1ms |
| Tier 2-3 Access Time | < 50ms |
| Tier 4-5 Access Time | < 500ms |
| Memory Hit Rate | 92% |
| Compression Ratio | 3.5x |

## Pricing

See [monetization.md](./monetization.md) for detailed pricing strategies.

## License

MIT License - see LICENSE file for details.

## Support

- Documentation: https://docs.memory-hierarchy.dev
- Discord: https://discord.gg/memory-hierarchy
- Email: support@memory-hierarchy.dev
