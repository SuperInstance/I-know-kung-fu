# Vector Search Server - Installation Guide

## Prerequisites

- Node.js v18+
- WebGPU-compatible browser (for GPU acceleration)
- OpenAI API key (for embeddings)

## Quick Start

```bash
# Clone and install
git clone https://github.com/your-org/vector-search-server-mcp.git
cd vector-search-server-mcp
npm install

# Configure
cp .env.example .env
# Edit .env with your API keys

# Build and run
npm run build
npm start
```

## Claude Desktop Configuration

Add to `~/Library/Application Support/Claude/claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "vector-search-server": {
      "command": "node",
      "args": ["/path/to/vector-search-server/dist/index.js"],
      "env": {
        "OPENAI_API_KEY": "your-key"
      }
    }
  }
}
```

## WebGPU Setup

For GPU acceleration, ensure:
- Chrome 113+ or Edge 113+ with WebGPU enabled
- Or use `WEBGPU_ENABLED=false` for CPU fallback

## Verification

```bash
# Test the server
curl http://localhost:3000/health
```

## Configuration Options

```bash
# .env file
OPENAI_API_KEY=your-key
WEBGPU_ENABLED=true
INDEX_STORAGE_PATH=./data/indices
DEFAULT_EMBEDDING_MODEL=text-embedding-3-small
```
