# Tool Guardian - Installation Guide

## Prerequisites

Before installing Tool Guardian, ensure you have:

- **Node.js** v18.0.0 or higher
- **npm** v9.0.0 or higher
- **Claude Desktop** or **Claude Code** installed
- Optional: Redis for distributed deployments

## Quick Start

### Step 1: Clone and Install

```bash
# Clone the repository
git clone https://github.com/your-org/tool-guardian-mcp.git

# Navigate to the project
cd tool-guardian-mcp

# Install dependencies
npm install

# Copy environment template
cp .env.example .env
```

### Step 2: Configure Environment

Edit `.env` with your settings:

```bash
# Server configuration
PORT=3000
LOG_LEVEL=info

# Default retry settings
DEFAULT_MAX_RETRIES=3
DEFAULT_RETRY_DELAY=1000

# Circuit breaker defaults
CIRCUIT_BREAKER_THRESHOLD=5
CIRCUIT_BREAKER_RESET_TIMEOUT=60000

# Optional: Redis for distributed mode
REDIS_URL=redis://localhost:6379
```

### Step 3: Build and Test

```bash
# Compile TypeScript
npm run build

# Run tests
npm test

# Start in development mode
npm run dev
```

### Step 4: Verify Installation

```bash
# Health check
curl http://localhost:3000/health

# Expected response:
# {"status":"healthy","version":"1.0.0","toolsRegistered":0}
```

## Claude Desktop Installation

### macOS

1. Open Claude Desktop
2. Go to **Settings** → **Developer** → **Edit Config**
3. Add the MCP server configuration:

```json
{
  "mcpServers": {
    "tool-guardian": {
      "command": "node",
      "args": ["/absolute/path/to/tool-guardian-mcp/dist/index.js"],
      "env": {
        "LOG_LEVEL": "info",
        "DEFAULT_MAX_RETRIES": "3"
      }
    }
  }
}
```

4. Save and restart Claude Desktop

### Windows

1. Open Claude Desktop Settings
2. Navigate to **Developer** → **Edit Config**
3. Add the configuration:

```json
{
  "mcpServers": {
    "tool-guardian": {
      "command": "node",
      "args": ["C:\\Users\\YourName\\tool-guardian-mcp\\dist\\index.js"],
      "env": {
        "LOG_LEVEL": "info"
      }
    }
  }
}
```

4. Save and restart Claude Desktop

### Linux

1. Edit `~/.config/claude/config.json`
2. Add the server configuration:

```json
{
  "mcpServers": {
    "tool-guardian": {
      "command": "node",
      "args": ["/home/yourname/tool-guardian-mcp/dist/index.js"],
      "env": {
        "LOG_LEVEL": "info"
      }
    }
  }
}
```

3. Restart Claude Desktop

## Claude Code Installation

For VS Code extension:

1. Open VS Code Settings (Cmd+,)
2. Search for "Claude Code MCP"
3. Add configuration:

```json
{
  "claude-code.mcpServers": {
    "tool-guardian": {
      "command": "node",
      "args": ["${workspaceFolder}/tool-guardian-mcp/dist/index.js"]
    }
  }
}
```

## Verification

After restarting Claude, verify the installation:

1. Open a new conversation
2. Ask: "What tools are available from tool-guardian?"

You should see tools like:
- `register_tool`
- `execute_tool`
- `validate_parameters`
- `get_tool_status`

## Configuration Options

### Global Settings

Configure in your `.env` file:

```bash
# Logging
LOG_LEVEL=debug|info|warn|error
LOG_FORMAT=json|text

# Retry defaults
DEFAULT_MAX_RETRIES=3
DEFAULT_RETRY_BACKOFF=exponential|linear|fixed
DEFAULT_RETRY_BASE_DELAY=1000
DEFAULT_RETRY_MAX_DELAY=30000
DEFAULT_RETRY_JITTER=true

# Circuit breaker defaults
CIRCUIT_BREAKER_ENABLED=true
CIRCUIT_BREAKER_THRESHOLD=5
CIRCUIT_BREAKER_RESET_TIMEOUT=60000

# Timeout defaults
DEFAULT_TIMEOUT=30000

# Validation defaults
VALIDATION_COERCE_TYPES=true
VALIDATION_APPLY_DEFAULTS=true
VALIDATION_STRICT=false
```

### Per-Tool Configuration

When registering tools, you can override defaults:

```json
{
  "name": "my-api",
  "retry": {
    "maxAttempts": 5,
    "backoff": "exponential",
    "baseDelay": 500
  },
  "circuitBreaker": {
    "enabled": true,
    "failureThreshold": 3
  }
}
```

## Authentication Setup

Tool Guardian supports multiple authentication methods:

### Bearer Token

```json
{
  "authentication": {
    "type": "bearer",
    "key": "your-token-here"
  }
}
```

### API Key

```json
{
  "authentication": {
    "type": "api_key",
    "header": "X-API-Key",
    "key": "your-api-key"
  }
}
```

### Basic Auth

```json
{
  "authentication": {
    "type": "basic",
    "key": "base64(username:password)"
  }
}
```

### OAuth 2.0

```json
{
  "authentication": {
    "type": "oauth2",
    "key": "your-access-token"
  }
}
```

## Distributed Deployment

For multi-instance deployments with shared state:

### Redis Configuration

```bash
# Enable Redis
REDIS_ENABLED=true
REDIS_URL=redis://localhost:6379
REDIS_PREFIX=tool-guardian:

# Circuit breaker state sharing
REDIS_CIRCUIT_BREAKER_TTL=300

# Rate limit state sharing
REDIS_RATE_LIMIT_TTL=3600
```

### Docker Compose

```yaml
version: '3.8'
services:
  tool-guardian:
    build: .
    ports:
      - "3000:3000"
    environment:
      - REDIS_URL=redis://redis:6379
      - LOG_LEVEL=info
    depends_on:
      - redis
  
  redis:
    image: redis:7-alpine
    volumes:
      - redis-data:/data

volumes:
  redis-data:
```

## Monitoring Setup

### Prometheus Metrics

Enable the metrics endpoint:

```bash
METRICS_ENABLED=true
METRICS_PORT=9090
```

Available metrics:
- `tool_guardian_executions_total`
- `tool_guardian_executions_successful`
- `tool_guardian_executions_failed`
- `tool_guardian_retry_attempts`
- `tool_guardian_circuit_breaker_state`
- `tool_guardian_validation_errors`

### OpenTelemetry Tracing

```bash
OTEL_ENABLED=true
OTEL_EXPORTER_OTLP_ENDPOINT=http://localhost:4317
OTEL_SERVICE_NAME=tool-guardian
```

### Sentry Error Tracking

```bash
SENTRY_DSN=https://your-sentry-dsn
SENTRY_ENVIRONMENT=production
```

## Advanced Configuration

### Custom Validators

Create custom validation functions:

```javascript
// validators/custom.js
module.exports = {
  phoneNumber: (value) => {
    const pattern = /^\+?[\d\s-]{10,}$/;
    if (!pattern.test(value)) {
      throw new Error('Invalid phone number format');
    }
    return value;
  },
  
  email: (value) => {
    const pattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!pattern.test(value)) {
      throw new Error('Invalid email format');
    }
    return value.toLowerCase();
  }
};
```

Register validators:

```bash
VALIDATORS_PATH=./validators/custom.js
```

### Dead Letter Queue

Configure failed operation storage:

```bash
DLQ_ENABLED=true
DLQ_MAX_SIZE=10000
DLQ_RETENTION_DAYS=7
```

### Webhook Notifications

```bash
WEBHOOK_URL=https://your-webhook.com/notify
WEBHOOK_EVENTS=tool_failed,circuit_opened,retry_exhausted
```

## Troubleshooting

### Common Issues

**Tool not appearing in Claude:**
1. Check config file path is correct
2. Verify Node.js is in PATH
3. Restart Claude Desktop completely

**Validation always failing:**
1. Check your JSON schema is valid
2. Enable debug logging: `LOG_LEVEL=debug`
3. Verify parameter types match schema

**Circuit breaker stuck open:**
1. Check if underlying issue is resolved
2. Use `reset_circuit_breaker` tool
3. Consider increasing `failureThreshold`

### Debug Mode

Enable verbose logging:

```bash
LOG_LEVEL=debug npm start
```

### Health Diagnostics

Run diagnostics endpoint:

```bash
curl http://localhost:3000/diagnostics
```

Returns:
```json
{
  "status": "healthy",
  "checks": {
    "redis": "connected",
    "memory": "ok",
    "tools": 5
  },
  "metrics": {
    "totalExecutions": 1234,
    "successRate": 0.987,
    "avgLatency": 45
  }
}
```

## Next Steps

1. Review [examples.md](./examples.md) for usage patterns
2. Register your first tool
3. Configure monitoring and alerts
4. Join our Discord for community support
