# Spreadsheet Server - Installation Guide

## Prerequisites

- Node.js v18+

## Quick Start

```bash
git clone https://github.com/your-org/spreadsheet-server-mcp.git
cd spreadsheet-server-mcp
npm install && npm run build
npm start
```

## Claude Desktop Configuration

```json
{
  "mcpServers": {
    "spreadsheet-server": {
      "command": "node",
      "args": ["/path/to/spreadsheet-server/dist/index.js"],
      "env": {
        "GOOGLE_SHEETS_API_KEY": "your-key"
      }
    }
  }
}
```

## Configuration

```bash
# File limits
MAX_FILE_SIZE=100MB
MAX_ROWS=1000000

# Google Sheets (optional)
GOOGLE_SHEETS_API_KEY=your-key
GOOGLE_SERVICE_ACCOUNT_KEY=path/to/key.json

# Caching
CACHE_ENABLED=true
```
