# Escalation Router - Installation Guide

## Prerequisites

Before installing the Escalation Router MCP server, ensure you have:

- **Node.js** v18.0.0 or higher
- **npm** v9.0.0 or higher
- **API Keys** for at least one LLM provider (OpenAI or Anthropic)
- **Claude Desktop** or **Claude Code** installed

## Quick Start

### Step 1: Clone and Install

```bash
# Clone the repository
git clone https://github.com/your-org/escalation-router-mcp.git

# Navigate to the project directory
cd escalation-router-mcp

# Install dependencies
npm install

# Copy environment template
cp .env.example .env
```

### Step 2: Configure Environment Variables

Edit the `.env` file with your API credentials:

```bash
# Required: At least one provider
OPENAI_API_KEY=sk-your-openai-key-here
ANTHROPIC_API_KEY=sk-ant-your-anthropic-key-here

# Optional: Local model support
OLLAMA_HOST=http://localhost:11434

# Configuration
ROUTER_STRATEGY=cost-optimized
LOG_LEVEL=info
CACHE_ENABLED=true
```

### Step 3: Build the Server

```bash
# Compile TypeScript
npm run build

# Verify build
ls dist/index.js
```

### Step 4: Test the Server

```bash
# Run in test mode
npm run test:server

# Expected output:
# ✓ Escalation Router MCP Server started
# ✓ Connected to 2 LLM providers
# ✓ Model tiers configured: 4 tiers, 7 models
# ✓ Cache initialized (max 10000 entries)
```

## Claude Desktop Installation

### macOS

1. Open Claude Desktop Settings
2. Navigate to **Developer** → **Edit Config**
3. Add the server configuration:

```json
{
  "mcpServers": {
    "escalation-router": {
      "command": "node",
      "args": ["/absolute/path/to/escalation-router-mcp/dist/index.js"],
      "env": {
        "OPENAI_API_KEY": "your-key-here",
        "ANTHROPIC_API_KEY": "your-key-here",
        "ROUTER_STRATEGY": "cost-optimized"
      }
    }
  }
}
```

4. Save and restart Claude Desktop

### Windows

1. Open Claude Desktop Settings
2. Navigate to **Developer** → **Edit Config**
3. Add the server configuration:

```json
{
  "mcpServers": {
    "escalation-router": {
      "command": "node",
      "args": ["C:\\Users\\YourName\\escalation-router-mcp\\dist\\index.js"],
      "env": {
        "OPENAI_API_KEY": "your-key-here",
        "ANTHROPIC_API_KEY": "your-key-here",
        "ROUTER_STRATEGY": "cost-optimized"
      }
    }
  }
}
```

4. Save and restart Claude Desktop

### Linux

1. Locate Claude Desktop config at `~/.config/claude/config.json`
2. Add the server configuration:

```json
{
  "mcpServers": {
    "escalation-router": {
      "command": "node",
      "args": ["/home/yourname/escalation-router-mcp/dist/index.js"],
      "env": {
        "OPENAI_API_KEY": "your-key-here",
        "ANTHROPIC_API_KEY": "your-key-here",
        "ROUTER_STRATEGY": "cost-optimized"
      }
    }
  }
}
```

3. Restart Claude Desktop

## Claude Code Installation

For Claude Code (VS Code extension):

1. Open VS Code Settings
2. Search for "Claude Code MCP"
3. Add server configuration:

```json
{
  "claude-code.mcpServers": {
    "escalation-router": {
      "command": "node",
      "args": ["${workspaceFolder}/escalation-router-mcp/dist/index.js"],
      "env": {
        "OPENAI_API_KEY": "${env:OPENAI_API_KEY}",
        "ANTHROPIC_API_KEY": "${env:ANTHROPIC_API_KEY}"
      }
    }
  }
}
```

## Verification

### Test the Installation

After restarting Claude, verify the server is running:

1. Open Claude Desktop/Code
2. Start a new conversation
3. Ask: "What MCP tools are available?"

You should see `escalation-router` tools listed, including:
- `route_query`
- `classify_query`
- `get_model_tiers`
- `get_routing_stats`

### Test Query Routing

Try a test query:

```
"Use the escalation router to answer: What is 25 * 47?"
```

Claude should:
1. Call the `route_query` tool
2. The router classifies this as Tier 1 (simple math)
3. Returns the answer with routing metadata

## Configuration Options

### Routing Strategies

Configure the routing strategy in your environment:

```bash
# Cost-focused routing (maximize savings)
ROUTER_STRATEGY=cost-optimized

# Speed-focused routing (minimize latency)
ROUTER_STRATEGY=latency-optimized

# Quality-focused routing (best results)
ROUTER_STRATEGY=quality-optimized

# Balanced approach (default)
ROUTER_STRATEGY=balanced
```

### Custom Model Tiers

Create a `tiers.json` file to customize model selection:

```json
{
  "tier1": {
    "models": ["gpt-3.5-turbo", "claude-3-haiku"],
    "maxTokens": 1000,
    "useCases": ["math", "formatting", "simple-qa"]
  },
  "tier2": {
    "models": ["gpt-4o-mini"],
    "maxTokens": 4000,
    "useCases": ["summarization", "translation", "code-review"]
  },
  "tier3": {
    "models": ["gpt-4-turbo", "claude-3-sonnet"],
    "maxTokens": 8000,
    "useCases": ["analysis", "writing", "reasoning"]
  },
  "tier4": {
    "models": ["gpt-4", "claude-3-opus"],
    "maxTokens": 32000,
    "useCases": ["expert-analysis", "complex-reasoning", "creative-writing"]
  }
}
```

### Budget Controls

Set spending limits:

```bash
# Daily budget limit (in dollars)
DAILY_BUDGET_LIMIT=50

# Per-query maximum cost
MAX_QUERY_COST=0.50

# Alert threshold (percentage of budget)
BUDGET_ALERT_THRESHOLD=80
```

## Advanced Configuration

### Redis for Distributed Caching

For production deployments with multiple instances:

```bash
# Enable Redis caching
CACHE_PROVIDER=redis
REDIS_URL=redis://localhost:6379

# Cache settings
CACHE_TTL=3600
CACHE_MAX_SIZE=100000
```

### Custom Provider Endpoints

Configure custom or self-hosted models:

```json
{
  "customProviders": [
    {
      "name": "company-llm",
      "baseUrl": "https://llm.company.com/v1",
      "models": ["company-model-v1"],
      "apiKey": "${COMPANY_LLM_KEY}",
      "tier": 2
    }
  ]
}
```

### Logging and Monitoring

```bash
# Log level
LOG_LEVEL=debug  # development
LOG_LEVEL=info   # production

# Enable metrics export
METRICS_ENABLED=true
METRICS_PORT=9090

# Sentry error tracking
SENTRY_DSN=https://your-sentry-dsn
```

## Troubleshooting

### Common Issues

**Server not showing in Claude:**
1. Check the config file path is correct
2. Verify Node.js is in your PATH
3. Restart Claude Desktop completely

**"API key invalid" errors:**
1. Verify API keys are correct in `.env`
2. Check keys have proper permissions
3. Ensure no extra whitespace in keys

**High latency on routing:**
1. Check network connectivity
2. Reduce `classificationTimeout` value
3. Enable caching for repeated queries

### Debug Mode

Enable verbose logging:

```bash
LOG_LEVEL=debug npm start
```

Check logs for:
- Classification decisions
- Model selection reasoning
- API call timing
- Cache hit/miss rates

### Health Check

Run the health check endpoint:

```bash
curl http://localhost:3000/health
```

Expected response:
```json
{
  "status": "healthy",
  "providers": {
    "openai": "connected",
    "anthropic": "connected"
  },
  "cache": {
    "entries": 1523,
    "hitRate": 0.34
  }
}
```

## Docker Deployment

For containerized deployments:

```bash
# Build the image
docker build -t escalation-router-mcp .

# Run the container
docker run -d \
  --name escalation-router \
  -e OPENAI_API_KEY=your-key \
  -e ANTHROPIC_API_KEY=your-key \
  -p 3000:3000 \
  escalation-router-mcp
```

## Next Steps

After successful installation:

1. Review [examples.md](./examples.md) for usage patterns
2. Configure custom routing rules for your use case
3. Set up monitoring and alerts
4. Join our Discord for community support
