# Cache Layer - Installation Guide

## Prerequisites

- Node.js v18+
- Redis (optional, for L2 cache)

## Quick Start

```bash
git clone https://github.com/your-org/cache-layer-mcp.git
cd cache-layer-mcp
npm install && npm run build
npm start
```

## Claude Desktop Configuration

```json
{
  "mcpServers": {
    "cache-layer": {
      "command": "node",
      "args": ["/path/to/cache-layer/dist/index.js"],
      "env": {
        "REDIS_URL": "redis://localhost:6379"
      }
    }
  }
}
```

## Configuration

```bash
# L1 (Memory) Settings
L1_MAX_SIZE=100mb
L1_DEFAULT_TTL=300

# L2 (Redis) Settings
REDIS_URL=redis://localhost:6379
L2_DEFAULT_TTL=3600

# L3 (Disk) Settings
L3_PATH=/var/cache/layer
L3_MAX_SIZE=10gb

# Semantic Matching
SEMANTIC_MATCHING_ENABLED=true
EMBEDDING_MODEL=text-embedding-3-small
```
