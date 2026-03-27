# PDF Server - Usage Examples

## Read PDF

```json
{
  "name": "read_pdf",
  "arguments": {
    "path": "/documents/report.pdf",
    "options": {
      "pages": "1-5",
      "extractTables": true
    }
  }
}
```

**Response:**
```json
{
  "pages": 25,
  "content": "Page 1:\n\n# Annual Report 2024\n\nExecutive Summary...",
  "tables": [
    {
      "page": 3,
      "rows": [["Q1", "Q2", "Q3", "Q4"], ["$1M", "$1.2M", "$1.5M", "$1.8M"]]
    }
  ]
}
```

## Create PDF

```json
{
  "name": "create_pdf",
  "arguments": {
    "path": "/output/report.pdf",
    "content": "<h1>Monthly Report</h1><p>Content here...</p>",
    "options": {
      "pageSize": "A4",
      "header": "Monthly Report - {{date}}",
      "footer": "Page {{page}}"
    }
  }
}
```

## Merge PDFs

```json
{
  "name": "merge_pdfs",
  "arguments": {
    "inputPaths": ["/docs/cover.pdf", "/docs/content.pdf", "/docs/appendix.pdf"],
    "outputPath": "/output/complete.pdf"
  }
}
```

## Fill Form

```json
{
  "name": "fill_form",
  "arguments": {
    "inputPath": "/forms/tax-form.pdf",
    "outputPath": "/output/filled-form.pdf",
    "fields": {
      "name": "John Smith",
      "ssn": "123-45-6789",
      "income": "75000",
      "date": "2024-01-15"
    },
    "flatten": true
  }
}
```

## Extract Form Data

```json
{
  "name": "extract_form_data",
  "arguments": {
    "path": "/forms/application.pdf"
  }
}
```

**Response:**
```json
{
  "fields": {
    "firstName": { "value": "John", "type": "text" },
    "lastName": { "value": "Smith", "type": "text" },
    "email": { "value": "john@example.com", "type": "text" },
    "subscribe": { "value": true, "type": "checkbox" }
  }
}
```

## Add Watermark

```json
{
  "name": "add_watermark",
  "arguments": {
    "inputPath": "/documents/report.pdf",
    "outputPath": "/output/watermarked.pdf",
    "text": "CONFIDENTIAL",
    "options": {
      "position": "center",
      "opacity": 0.3,
      "rotation": 45
    }
  }
}
```
