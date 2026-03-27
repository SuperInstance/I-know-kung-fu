# Document Server - Installation Guide

## Prerequisites

- Node.js v18+
- LibreOffice (optional, for advanced conversions)

## Quick Start

```bash
git clone https://github.com/your-org/document-server-mcp.git
cd document-server-mcp
npm install && npm run build
npm start
```

## Claude Desktop Configuration

```json
{
  "mcpServers": {
    "document-server": {
      "command": "node",
      "args": ["/path/to/document-server/dist/index.js"]
    }
  }
}
```

## Configuration

```bash
# Supported formats
SUPPORTED_FORMATS=docx,pdf,txt,md,html,rtf

# File size limits
MAX_FILE_SIZE=100MB

# Conversion options
LIBREOFFICE_PATH=/usr/bin/libreoffice
```
