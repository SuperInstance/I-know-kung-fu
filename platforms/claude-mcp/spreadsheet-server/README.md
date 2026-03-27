# Spreadsheet Server MCP Server

## Overview

The Spreadsheet Server is a powerful MCP (Model Context Protocol) server for spreadsheet operations. It provides comprehensive capabilities for creating, reading, modifying, and analyzing spreadsheets with support for XLSX, XLS, CSV, and Google Sheets integration.

## Problem Statement

Working with spreadsheets programmatically is challenging:

- **Complex APIs**: Different libraries for each format
- **Formula Handling**: Preserving formulas while editing
- **Large Files**: Memory issues with big spreadsheets
- **Data Analysis**: Computing statistics, pivots, charts
- **Multi-Format Support**: Converting between formats

## Solution

Spreadsheet Server provides a unified spreadsheet toolkit:

```
┌─────────────────────────────────────────────────────────────┐
│                   SPREADSHEET SERVER                         │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Reader    │  │   Writer    │  │  Analyzer   │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│         ↓                ↓                ↓                  │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   XLSX/XLS  │  │    CSV      │  │ Google Sheets│         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
└─────────────────────────────────────────────────────────────┘
```

## Key Features

### Multi-Format Support
- **Excel**: XLSX, XLS (read/write)
- **CSV**: Read/write with configurable delimiters
- **Google Sheets**: Read/write via API
- **OpenDocument**: ODS support

### Spreadsheet Operations
- **Read**: Extract data, formulas, formatting
- **Write**: Create new spreadsheets
- **Modify**: Edit cells, add sheets, styling
- **Convert**: Transform between formats

### Data Analysis
- **Statistics**: Sum, average, min, max, count
- **Filtering**: Filter rows by conditions
- **Sorting**: Sort by multiple columns
- **Pivot Tables**: Generate pivot summaries
- **Charts**: Create embedded charts

### Advanced Features
- **Formula Preservation**: Keep formulas intact
- **Conditional Formatting**: Apply rules
- **Cell Merging**: Merge cells, rows, columns
- **Data Validation**: Set validation rules

## Installation

```bash
git clone https://github.com/your-org/spreadsheet-server-mcp.git
cd spreadsheet-server-mcp
npm install && npm run build
npm start
```

## Configuration

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

## Pricing

See [monetization.md](./monetization.md) for details.
