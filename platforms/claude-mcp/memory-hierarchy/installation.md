# Memory Hierarchy - Installation Guide

## Prerequisites

Before installing Memory Hierarchy, ensure you have:

- **Node.js** v18.0.0 or higher
- **npm** v9.0.0 or higher
- **Redis** (optional, for persistence)
- **Vector Database** (optional, for long-term memory)
- **Claude Desktop** or **Claude Code** installed

## Quick Start

### Step 1: Clone and Install

```bash
# Clone the repository
git clone https://github.com/your-org/memory-hierarchy-mcp.git

# Navigate to project
cd memory-hierarchy-mcp

# Install dependencies
npm install

# Copy environment template
cp .env.example .env
```

### Step 2: Configure Environment

Edit `.env`:

```bash
# Basic configuration
PORT=3000
LOG_LEVEL=info

# Tier 2-3 Storage (Redis)
REDIS_URL=redis://localhost:6379

# Tier 4-5 Storage (Vector DB)
VECTOR_DB_PROVIDER=pinecone  # or weaviate, qdrant, milvus
PINECONE_API_KEY=your-key
PINECONE_ENVIRONMENT=production
PINECONE_INDEX=memory-hierarchy

# Embedding configuration
EMBEDDING_PROVIDER=openai  # or local
OPENAI_API_KEY=your-key
```

### Step 3: Build and Test

```bash
# Build
npm run build

# Run tests
npm test

# Start server
npm start
```

### Step 4: Verify Installation

```bash
# Health check
curl http://localhost:3000/health

# Expected response:
# {
#   "status": "healthy",
#   "version": "1.0.0",
#   "tiers": {
#     "tier0": "ready",
#     "tier1": "ready",
#     "tier2": "connected",
#     "tier3": "connected",
#     "tier4": "connected",
#     "tier5": "connected"
#   }
# }
```

## Claude Desktop Installation

### macOS

1. Open Claude Desktop
2. Go to **Settings** → **Developer** → **Edit Config**
3. Add configuration:

```json
{
  "mcpServers": {
    "memory-hierarchy": {
      "command": "node",
      "args": ["/absolute/path/to/memory-hierarchy-mcp/dist/index.js"],
      "env": {
        "REDIS_URL": "redis://localhost:6379",
        "PINECONE_API_KEY": "your-key",
        "PINECONE_ENVIRONMENT": "production"
      }
    }
  }
}
```

4. Save and restart Claude Desktop

### Windows

```json
{
  "mcpServers": {
    "memory-hierarchy": {
      "command": "node",
      "args": ["C:\\Users\\YourName\\memory-hierarchy-mcp\\dist\\index.js"],
      "env": {
        "REDIS_URL": "redis://localhost:6379"
      }
    }
  }
}
```

### Linux

```json
{
  "mcpServers": {
    "memory-hierarchy": {
      "command": "node",
      "args": ["/home/yourname/memory-hierarchy-mcp/dist/index.js"],
      "env": {
        "REDIS_URL": "redis://localhost:6379"
      }
    }
  }
}
```

## Storage Configuration

### Tier 0-1: In-Memory (Default)

No configuration needed. Memories are stored in RAM.

```bash
# Optional: Configure memory limits
TIER0_MAX_TOKENS=128000
TIER1_MAX_TOKENS=1000000
```

### Tier 2-3: Redis

```bash
# Redis connection
REDIS_URL=redis://localhost:6379
REDIS_PASSWORD=optional-password

# Tier-specific settings
TIER2_TTL=86400      # 24 hours
TIER3_TTL=604800     # 7 days
TIER2_MAX_MEMORY=100mb
TIER3_MAX_MEMORY=500mb
```

### Tier 4: Vector Database

#### Pinecone

```bash
VECTOR_DB_PROVIDER=pinecone
PINECONE_API_KEY=your-api-key
PINECONE_ENVIRONMENT=production
PINECONE_INDEX=memory-hierarchy
```

#### Weaviate

```bash
VECTOR_DB_PROVIDER=weaviate
WEAVIATE_URL=http://localhost:8080
WEAVIATE_API_KEY=optional
```

#### Qdrant

```bash
VECTOR_DB_PROVIDER=qdrant
QDRANT_URL=http://localhost:6333
QDRANT_API_KEY=optional
```

### Tier 5: Object Storage

```bash
# AWS S3
ARCHIVE_PROVIDER=s3
AWS_ACCESS_KEY_ID=your-key
AWS_SECRET_ACCESS_KEY=your-secret
S3_BUCKET=memory-archive

# Or local filesystem
ARCHIVE_PROVIDER=filesystem
ARCHIVE_PATH=/var/memory-archive
```

## Embedding Configuration

### OpenAI Embeddings

```bash
EMBEDDING_PROVIDER=openai
OPENAI_API_KEY=your-key
EMBEDDING_MODEL=text-embedding-3-small
```

### Local Embeddings

```bash
EMBEDDING_PROVIDER=local
EMBEDDING_MODEL=all-MiniLM-L6-v2
EMBEDDING_DEVICE=cpu  # or cuda
```

### Cohere Embeddings

```bash
EMBEDDING_PROVIDER=cohere
COHERE_API_KEY=your-key
EMBEDDING_MODEL=embed-english-v3.0
```

## Verification

After restarting Claude:

1. Open a new conversation
2. Ask: "What memory tools are available?"

You should see:
- `store_memory`
- `retrieve_memory`
- `search_memories`
- `get_memory_context`
- And more...

### Test Memory Storage

```
"Store this memory: I prefer dark mode in all applications"
```

### Test Memory Retrieval

```
"What do you know about my UI preferences?"
```

## Advanced Configuration

### Auto-Promotion Settings

```bash
AUTO_PROMOTION_ENABLED=true
AUTO_PROMOTION_ACCESS_THRESHOLD=3
AUTO_PROMOTION_TIME_WINDOW=3600  # 1 hour
```

### Auto-Demotion Settings

```bash
AUTO_DEMOTION_ENABLED=true
AUTO_DEMOTION_ACCESS_THRESHOLD=0
AUTO_DEMOTION_TIME_WINDOW=86400  # 24 hours
```

### Compression Settings

```bash
COMPRESSION_ENABLED=true
COMPRESSION_THRESHOLD=10  # memories
COMPRESSION_ALGORITHM=semantic
```

### Memory Expiration

```bash
DEFAULT_EXPIRATION_ENABLED=true
TIER2_DEFAULT_TTL=86400
TIER3_DEFAULT_TTL=604800
TIER4_DEFAULT_TTL=2592000  # 30 days
```

## Docker Deployment

### Docker Compose

```yaml
version: '3.8'
services:
  memory-hierarchy:
    build: .
    ports:
      - "3000:3000"
    environment:
      - REDIS_URL=redis://redis:6379
      - PINECONE_API_KEY=${PINECONE_API_KEY}
      - PINECONE_ENVIRONMENT=${PINECONE_ENVIRONMENT}
    depends_on:
      - redis
  
  redis:
    image: redis:7-alpine
    volumes:
      - redis-data:/data
    command: redis-server --maxmemory 500mb --maxmemory-policy allkeys-lru

volumes:
  redis-data:
```

### Run with Docker

```bash
# Build
docker build -t memory-hierarchy-mcp .

# Run
docker run -d \
  -p 3000:3000 \
  -e REDIS_URL=redis://host.docker.internal:6379 \
  memory-hierarchy-mcp
```

## Monitoring

### Prometheus Metrics

```bash
METRICS_ENABLED=true
METRICS_PORT=9090
```

Available metrics:
- `memory_hierarchy_stored_total`
- `memory_hierarchy_retrieved_total`
- `memory_hierarchy_tier_usage`
- `memory_hierarchy_retrieval_latency`

### Health Endpoints

```bash
# Basic health
curl http://localhost:3000/health

# Detailed diagnostics
curl http://localhost:3000/diagnostics

# Tier status
curl http://localhost:3000/tiers/status
```

## Troubleshooting

### Common Issues

**Redis connection failed:**
1. Verify Redis is running: `redis-cli ping`
2. Check REDIS_URL is correct
3. Ensure no firewall blocking

**Vector DB errors:**
1. Verify API keys are correct
2. Check index exists
3. Verify dimension matching

**Memory not persisting:**
1. Check tier configuration
2. Verify storage backends are connected
3. Check logs for errors

### Debug Mode

```bash
LOG_LEVEL=debug npm start
```

## Next Steps

1. Review [examples.md](./examples.md) for usage patterns
2. Configure memory types for your use case
3. Set up monitoring and alerts
4. Join Discord for support
