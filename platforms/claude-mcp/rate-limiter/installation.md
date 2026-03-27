# Rate Limiter - Installation Guide

## Prerequisites

- Node.js v18+
- Redis (optional, for distributed mode)

## Quick Start

```bash
git clone https://github.com/your-org/rate-limiter-mcp.git
cd rate-limiter-mcp
npm install

# Configure
cp .env.example .env

# Build and run
npm run build
npm start
```

## Claude Desktop Configuration

```json
{
  "mcpServers": {
    "rate-limiter": {
      "command": "node",
      "args": ["/path/to/rate-limiter/dist/index.js"],
      "env": {
        "REDIS_URL": "redis://localhost:6379"
      }
    }
  }
}
```

## Configuration

```bash
# Local mode (no Redis)
RATE_LIMIT_MODE=local

# Distributed mode
RATE_LIMIT_MODE=distributed
REDIS_URL=redis://localhost:6379

# Default limits
DEFAULT_WINDOW=60
DEFAULT_MAX_REQUESTS=100
```

## Verification

```bash
curl http://localhost:3000/health
```
