# PDF Server MCP Server

## Overview

The PDF Server is a specialized MCP (Model Context Protocol) server for comprehensive PDF operations. It provides powerful capabilities for creating, reading, modifying, and manipulating PDF documents with support for forms, annotations, digital signatures, and more.

## Problem Statement

Working with PDFs is challenging:

- **Read Complexity**: Extracting text while preserving structure
- **Form Handling**: Filling and extracting form data
- **Document Security**: Encryption, permissions, signatures
- **Manipulation**: Merge, split, rotate, watermark
- **OCR Requirements**: Scanned documents need text recognition

## Solution

PDF Server provides a complete PDF toolkit:

```
┌─────────────────────────────────────────────────────────────┐
│                       PDF SERVER                             │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Reader    │  │   Writer    │  │  Modifier   │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│         ↓                ↓                ↓                  │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Forms     │  │  Security   │  │    OCR      │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
└─────────────────────────────────────────────────────────────┘
```

## Key Features

### PDF Reading
- **Text Extraction**: Extract text with position information
- **Table Extraction**: Convert PDF tables to structured data
- **Image Extraction**: Extract embedded images
- **Metadata Reading**: Access document properties

### PDF Creation
- **Generate from Scratch**: Create new PDFs
- **HTML to PDF**: Convert HTML content
- **Template-Based**: Generate from templates
- **Multi-Page Layouts**: Headers, footers, page numbers

### PDF Modification
- **Merge PDFs**: Combine multiple documents
- **Split PDFs**: Extract pages or ranges
- **Rotate Pages**: Fix orientation issues
- **Watermark**: Add text or image watermarks
- **Annotations**: Add comments, highlights, stamps

### Forms & Security
- **Form Filling**: Populate PDF forms
- **Form Extraction**: Get form field data
- **Digital Signatures**: Sign documents
- **Encryption**: Password protection

## Installation

```bash
git clone https://github.com/your-org/pdf-server-mcp.git
cd pdf-server-mcp
npm install && npm run build
npm start
```

## Configuration

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

## Pricing

See [monetization.md](./monetization.md) for details.
