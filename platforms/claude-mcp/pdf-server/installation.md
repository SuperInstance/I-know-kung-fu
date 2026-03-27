# PDF Server - Installation Guide

## Prerequisites

- Node.js v18+
- Tesseract OCR (optional, for OCR features)

## Quick Start

```bash
git clone https://github.com/your-org/pdf-server-mcp.git
cd pdf-server-mcp
npm install && npm run build
npm start
```

## Claude Desktop Configuration

```json
{
  "mcpServers": {
    "pdf-server": {
      "command": "node",
      "args": ["/path/to/pdf-server/dist/index.js"]
    }
  }
}
```

## Configuration

```bash
# OCR settings
OCR_ENGINE=tesseract
TESSERACT_PATH=/usr/bin/tesseract

# File limits
MAX_FILE_SIZE=500MB
TEMP_DIR=/tmp/pdf-server

# Security
ALLOW_ENCRYPTION=true
```
