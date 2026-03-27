# Circuit Breaker - Installation Guide

## Prerequisites

- Node.js v18+
- Redis (optional, for distributed state)

## Quick Start

```bash
git clone https://github.com/your-org/circuit-breaker-mcp.git
cd circuit-breaker-mcp
npm install && npm run build
npm start
```

## Claude Desktop Configuration

```json
{
  "mcpServers": {
    "circuit-breaker": {
      "command": "node",
      "args": ["/path/to/circuit-breaker/dist/index.js"],
      "env": {
        "REDIS_URL": "redis://localhost:6379"
      }
    }
  }
}
```

## Configuration

```bash
# Default thresholds
DEFAULT_FAILURE_THRESHOLD=5
DEFAULT_SUCCESS_THRESHOLD=2
DEFAULT_TIMEOUT=30000
DEFAULT_RESET_TIMEOUT=60000

# Distributed state
REDIS_URL=redis://localhost:6379
```
