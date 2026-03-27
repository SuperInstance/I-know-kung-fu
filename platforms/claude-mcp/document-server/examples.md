# Document Server - Usage Examples

## Read Document

```json
{
  "name": "read_document",
  "arguments": {
    "path": "/documents/report.docx",
    "options": {
      "extractMetadata": true
    }
  }
}
```

**Response:**
```json
{
  "content": "# Annual Report 2024\n\n## Executive Summary\n...",
  "metadata": {
    "title": "Annual Report 2024",
    "author": "John Smith",
    "pages": 25,
    "wordCount": 5000
  }
}
```

## Create Document

```json
{
  "name": "create_document",
  "arguments": {
    "path": "/output/report.docx",
    "format": "docx",
    "content": "# Monthly Report\n\nThis is the monthly report content.",
    "metadata": {
      "title": "Monthly Report",
      "author": "AI Agent"
    }
  }
}
```

## Convert Document

```json
{
  "name": "convert_document",
  "arguments": {
    "inputPath": "/documents/report.docx",
    "outputPath": "/output/report.pdf",
    "outputFormat": "pdf"
  }
}
```

## Merge Documents

```json
{
  "name": "merge_documents",
  "arguments": {
    "inputPaths": ["/docs/part1.pdf", "/docs/part2.pdf"],
    "outputPath": "/output/combined.pdf"
  }
}
```

## Apply Template

```json
{
  "name": "apply_template",
  "arguments": {
    "templatePath": "/templates/invoice.docx",
    "outputPath": "/output/invoice-001.docx",
    "data": {
      "invoiceNumber": "001",
      "customerName": "Acme Corp",
      "items": [
        {"description": "Service A", "amount": 100},
        {"description": "Service B", "amount": 200}
      ]
    }
  }
}
```
