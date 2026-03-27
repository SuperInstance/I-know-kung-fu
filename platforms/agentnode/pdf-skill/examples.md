# PDF Skill API Examples

This document provides comprehensive examples for using the PDF Skill API. All examples include request payloads and expected responses.

## Authentication

All API requests require authentication via API key:

```bash
curl -X POST "https://api.agentnode.io/v1/skills/pdf/create" \
  -H "X-API-Key: your_api_key_here" \
  -H "Content-Type: application/json"
```

## PDF Creation

### Create PDF from Content

Create a PDF document with text and formatting:

```bash
POST /v1/skills/pdf/create
```

**Request:**
```json
{
  "options": {
    "title": "Invoice #INV-2024-001",
    "author": "ACME Corporation",
    "page_size": "A4",
    "orientation": "portrait"
  },
  "content": [
    {
      "type": "text",
      "element": {
        "text": "INVOICE",
        "font_family": "Helvetica",
        "font_size": 24,
        "bold": true,
        "alignment": "center"
      }
    },
    {
      "type": "text",
      "element": {
        "text": "Invoice Number: INV-2024-001",
        "font_size": 12,
        "position": {"x": 50, "y": 100, "width": 500}
      }
    },
    {
      "type": "text",
      "element": {
        "text": "Date: December 15, 2024",
        "font_size": 12,
        "position": {"x": 50, "y": 120, "width": 500}
      }
    },
    {
      "type": "table",
      "table": {
        "headers": ["Description", "Quantity", "Unit Price", "Total"],
        "rows": [
          ["Consulting Services", "10", "$150.00", "$1,500.00"],
          ["Software License", "1", "$500.00", "$500.00"],
          ["Support Package", "1", "$200.00", "$200.00"]
        ],
        "position": {"x": 50, "y": 200}
      }
    }
  ]
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "pdf_invoice_123",
  "download_url": "https://storage.agentnode.io/pdfs/pdf_invoice_123.pdf",
  "metadata": {
    "page_count": 1,
    "file_size_kb": 45,
    "created_at": "2024-12-15T10:30:00Z"
  },
  "billing": {
    "operation": "create",
    "amount_charged": 0.05,
    "currency": "USD"
  }
}
```

### Create PDF from HTML

Convert HTML content to a PDF:

```bash
POST /v1/skills/pdf/create
```

**Request:**
```json
{
  "options": {
    "title": "Product Catalog",
    "page_size": "Letter"
  },
  "html": "<html><body><h1>Product Catalog</h1><table><tr><td>Product A</td><td>$99</td></tr><tr><td>Product B</td><td>$149</td></tr></table></body></html>"
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "pdf_catalog_456",
  "download_url": "https://storage.agentnode.io/pdfs/pdf_catalog_456.pdf",
  "metadata": {
    "page_count": 1,
    "file_size_kb": 32
  }
}
```

## Form Filling

### Fill PDF Form Fields

Fill form fields in a PDF document:

```bash
POST /v1/skills/pdf/fill-form
```

**Request:**
```json
{
  "document_id": "pdf_form_irs_w4",
  "fields": [
    {"field_name": "firstName", "value": "John"},
    {"field_name": "lastName", "value": "Smith"},
    {"field_name": "ssn", "value": "123-45-6789"},
    {"field_name": "address", "value": "123 Main Street, Apt 4B"},
    {"field_name": "city", "value": "New York"},
    {"field_name": "state", "value": "NY"},
    {"field_name": "zip", "value": "10001"},
    {"field_name": "filingStatus", "value": "Single"},
    {"field_name": "multipleJobs", "value": false},
    {"field_name": "dependents", "value": "0"},
    {"field_name": "signature", "value": "John Smith"},
    {"field_name": "date", "value": "12/15/2024"}
  ],
  "flatten": false
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "pdf_form_filled_789",
  "download_url": "https://storage.agentnode.io/pdfs/pdf_form_filled_789.pdf",
  "fields_filled": 12,
  "fields_failed": 0,
  "flattened": false,
  "billing": {
    "operation": "fill_form",
    "amount_charged": 0.04
  }
}
```

### Get Form Field Information

Retrieve all form fields in a PDF:

```bash
POST /v1/skills/pdf/get-form-fields
```

**Request:**
```json
{
  "document_url": "https://example.com/forms/application.pdf"
}
```

**Response:**
```json
{
  "success": true,
  "fields": [
    {
      "field_name": "applicant_name",
      "field_type": "text",
      "page": 1,
      "required": true,
      "current_value": "",
      "max_length": 100,
      "coordinates": {"x": 100, "y": 200, "width": 200, "height": 20}
    },
    {
      "field_name": "email",
      "field_type": "text",
      "page": 1,
      "required": true,
      "current_value": "",
      "format": "email"
    },
    {
      "field_name": "agree_terms",
      "field_type": "checkbox",
      "page": 2,
      "required": true,
      "current_value": false
    },
    {
      "field_name": "state",
      "field_type": "dropdown",
      "page": 1,
      "required": true,
      "options": ["CA", "NY", "TX", "FL", "Other"],
      "current_value": ""
    },
    {
      "field_name": "signature",
      "field_type": "signature",
      "page": 3,
      "required": true
    }
  ],
  "total_fields": 15,
  "required_fields": 10,
  "billing": {
    "operation": "get_form_fields",
    "amount_charged": 0.01
  }
}
```

## Text Extraction

### Extract Text from PDF

Extract text content from a PDF:

```bash
POST /v1/skills/pdf/extract-text
```

**Request:**
```json
{
  "document_id": "pdf_report_123",
  "pages": [1, 2, 3],
  "preserve_layout": true
}
```

**Response:**
```json
{
  "success": true,
  "text": "Annual Report 2024\n\nExecutive Summary\n\nThis report presents the financial results for fiscal year 2024...",
  "pages": [
    {
      "page_number": 1,
      "text": "Annual Report 2024\n\nExecutive Summary..."
    },
    {
      "page_number": 2,
      "text": "Financial Highlights\n\nRevenue: $10.5M (+15%)..."
    },
    {
      "page_number": 3,
      "text": "Market Analysis\n\nThe global market expanded..."
    }
  ],
  "metadata": {
    "total_pages_in_document": 25,
    "pages_extracted": 3,
    "word_count": 1250,
    "ocr_used": false
  },
  "billing": {
    "operation": "extract_text",
    "amount_charged": 0.01
  }
}
```

### Extract with OCR

Extract text from a scanned PDF:

```bash
POST /v1/skills/pdf/extract-text
```

**Request:**
```json
{
  "document_url": "https://example.com/scanned-document.pdf",
  "ocr_options": {
    "language": "eng",
    "detect_language": true,
    "preserve_layout": true
  }
}
```

**Response:**
```json
{
  "success": true,
  "text": "SCANNED DOCUMENT\n\nThis text was extracted using OCR...",
  "pages": [
    {
      "page_number": 1,
      "text": "SCANNED DOCUMENT...",
      "confidence": 0.95
    }
  ],
  "ocr_used": true,
  "ocr_details": {
    "language_detected": "eng",
    "confidence_average": 0.93,
    "pages_processed": 5
  },
  "billing": {
    "operation": "ocr",
    "amount_charged": 0.10,
    "pages_billed": 5
  }
}
```

## Table Extraction

### Extract Tables from PDF

Extract tabular data:

```bash
POST /v1/skills/pdf/extract-tables
```

**Request:**
```json
{
  "document_id": "pdf_financial_report",
  "pages": [5, 6, 7],
  "output_format": "json"
}
```

**Response:**
```json
{
  "success": true,
  "tables": [
    {
      "table_id": 1,
      "page": 5,
      "rows": 8,
      "columns": 5,
      "headers": ["Quarter", "Revenue", "Costs", "Profit", "Growth %"],
      "data": [
        ["Q1 2024", "$2,500,000", "$1,800,000", "$700,000", "+12%"],
        ["Q2 2024", "$2,750,000", "$1,900,000", "$850,000", "+10%"],
        ["Q3 2024", "$2,900,000", "$1,950,000", "$950,000", "+5%"],
        ["Q4 2024", "$3,100,000", "$2,000,000", "$1,100,000", "+7%"]
      ],
      "download_url": "https://storage.agentnode.io/tables/table_1.csv"
    },
    {
      "table_id": 2,
      "page": 6,
      "rows": 15,
      "columns": 4,
      "headers": ["Department", "Headcount", "Budget", "Variance"],
      "data": [
        ["Engineering", "45", "$4,500,000", "-2%"],
        ["Sales", "25", "$2,000,000", "+5%"],
        ["Marketing", "15", "$1,500,000", "0%"]
      ],
      "download_url": "https://storage.agentnode.io/tables/table_2.csv"
    }
  ],
  "total_tables": 2,
  "billing": {
    "operation": "extract_tables",
    "amount_charged": 0.03
  }
}
```

## PDF Merging

### Merge Multiple PDFs

Combine several PDFs into one:

```bash
POST /v1/skills/pdf/merge
```

**Request:**
```json
{
  "documents": [
    {"document_id": "pdf_cover_page"},
    {"document_id": "pdf_executive_summary"},
    {"document_url": "https://example.com/report-body.pdf"},
    {"document_id": "pdf_appendix", "pages": [1, 2, 3]}
  ],
  "add_bookmarks": true,
  "preserve_links": true
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "pdf_merged_report",
  "download_url": "https://storage.agentnode.io/pdfs/pdf_merged_report.pdf",
  "source_count": 4,
  "total_pages": 52,
  "bookmarks_added": true,
  "merge_details": [
    {"source": "pdf_cover_page", "pages_added": 1},
    {"source": "pdf_executive_summary", "pages_added": 3},
    {"source": "report-body.pdf", "pages_added": 40},
    {"source": "pdf_appendix", "pages_added": 8}
  ],
  "billing": {
    "operation": "merge",
    "amount_charged": 0.06
  }
}
```

## PDF Splitting

### Split PDF by Page Ranges

Split a PDF into sections:

```bash
POST /v1/skills/pdf/split
```

**Request:**
```json
{
  "document_id": "pdf_annual_report",
  "split_by": "ranges",
  "ranges": [
    {"start": 1, "end": 5, "name": "executive_summary"},
    {"start": 6, "end": 25, "name": "main_content"},
    {"start": 26, "end": 35, "name": "financials"},
    {"start": 36, "end": 50, "name": "appendix"}
  ]
}
```

**Response:**
```json
{
  "success": true,
  "split_documents": [
    {
      "document_id": "pdf_executive_summary",
      "download_url": "https://storage.agentnode.io/pdfs/executive_summary.pdf",
      "pages": "1-5",
      "file_size_kb": 120
    },
    {
      "document_id": "pdf_main_content",
      "download_url": "https://storage.agentnode.io/pdfs/main_content.pdf",
      "pages": "6-25",
      "file_size_kb": 450
    },
    {
      "document_id": "pdf_financials",
      "download_url": "https://storage.agentnode.io/pdfs/financials.pdf",
      "pages": "26-35",
      "file_size_kb": 280
    },
    {
      "document_id": "pdf_appendix",
      "download_url": "https://storage.agentnode.io/pdfs/appendix.pdf",
      "pages": "36-50",
      "file_size_kb": 320
    }
  ],
  "total_documents": 4,
  "billing": {
    "operation": "split",
    "amount_charged": 0.04
  }
}
```

## Format Conversion

### Convert PDF to Images

Convert PDF pages to PNG images:

```bash
POST /v1/skills/pdf/convert
```

**Request:**
```json
{
  "document_id": "pdf_presentation",
  "output_format": "png",
  "pages": [1, 2, 3, 4, 5],
  "options": {
    "dpi": 150,
    "quality": 90
  }
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "pdf_converted_images",
  "format": "png",
  "pages_converted": 5,
  "images": [
    {
      "page": 1,
      "download_url": "https://storage.agentnode.io/images/page_1.png",
      "width": 1275,
      "height": 1650
    },
    {
      "page": 2,
      "download_url": "https://storage.agentnode.io/images/page_2.png",
      "width": 1275,
      "height": 1650
    }
  ],
  "billing": {
    "operation": "convert",
    "amount_charged": 0.03
  }
}
```

## Digital Signatures

### Apply Digital Signature

Sign a PDF with a digital certificate:

```bash
POST /v1/skills/pdf/sign
```

**Request:**
```json
{
  "document_id": "pdf_contract_123",
  "certificate": "base64_encoded_certificate_data",
  "password": "certificate_password",
  "reason": "Contract Agreement",
  "location": "New York, NY",
  "contact_info": "legal@company.com",
  "signature_appearance": {
    "page": 5,
    "x": 100,
    "y": 500,
    "width": 150,
    "height": 50,
    "show_date": true,
    "show_reason": true
  }
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "pdf_signed_contract",
  "download_url": "https://storage.agentnode.io/pdfs/pdf_signed_contract.pdf",
  "signed_at": "2024-12-15T10:30:00Z",
  "signature_valid": true,
  "signature_details": {
    "signer": "John Smith",
    "issuer": "DigiCert Inc",
    "valid_from": "2024-01-01",
    "valid_to": "2025-01-01"
  },
  "billing": {
    "operation": "sign",
    "amount_charged": 0.10
  }
}
```

## Watermarks

### Add Text Watermark

Add a watermark to a PDF:

```bash
POST /v1/skills/pdf/watermark
```

**Request:**
```json
{
  "document_id": "pdf_confidential_report",
  "watermark": {
    "type": "text",
    "content": "CONFIDENTIAL",
    "opacity": 0.3,
    "rotation": -45,
    "position": "diagonal",
    "font_size": 48,
    "color": "#FF0000"
  },
  "pages": "all"
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "pdf_watermarked_report",
  "download_url": "https://storage.agentnode.io/pdfs/pdf_watermarked_report.pdf",
  "watermark_applied": true,
  "pages_affected": 25,
  "billing": {
    "operation": "watermark",
    "amount_charged": 0.02
  }
}
```

## Encryption

### Encrypt PDF with Password

Add password protection:

```bash
POST /v1/skills/pdf/encrypt
```

**Request:**
```json
{
  "document_id": "pdf_sensitive_data",
  "user_password": "secure_password_123",
  "owner_password": "admin_password_456",
  "permissions": {
    "print": true,
    "copy": false,
    "modify": false,
    "annotate": false,
    "fill_forms": true
  },
  "encryption_level": "256bit"
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "pdf_encrypted_doc",
  "download_url": "https://storage.agentnode.io/pdfs/pdf_encrypted_doc.pdf",
  "encrypted": true,
  "encryption_level": "256bit",
  "permissions_set": {
    "print": true,
    "copy": false,
    "modify": false
  },
  "billing": {
    "operation": "encrypt",
    "amount_charged": 0.03
  }
}
```

## Document Analysis

### Analyze PDF Structure

Get detailed information about a PDF:

```bash
POST /v1/skills/pdf/analyze
```

**Request:**
```json
{
  "document_id": "pdf_complex_document"
}
```

**Response:**
```json
{
  "success": true,
  "metadata": {
    "title": "Complex Document",
    "author": "Document Author",
    "subject": "Technical Specification",
    "keywords": ["specification", "technical", "v2.0"],
    "creator": "Microsoft Word",
    "producer": "AgentNode PDF Engine",
    "created": "2024-11-15T09:00:00Z",
    "modified": "2024-12-10T14:30:00Z",
    "page_count": 45,
    "file_size_kb": 1250,
    "is_encrypted": false,
    "is_linear": false,
    "has_forms": true,
    "pdf_version": "1.7"
  },
  "structure": {
    "bookmarks": [
      {"title": "Introduction", "level": 1, "page": 1},
      {"title": "Background", "level": 2, "page": 2}
    ],
    "links": 25,
    "images": 15,
    "fonts": ["Helvetica", "Times-Roman", "Courier"],
    "form_fields": 12
  },
  "billing": {
    "operation": "analyze",
    "amount_charged": 0.01
  }
}
```

## Error Handling

### Common Error Responses

**Encrypted PDF Without Password:**
```json
{
  "success": false,
  "error": {
    "code": "ENCRYPTED_PDF",
    "message": "Cannot process encrypted PDF without password",
    "details": {
      "document_id": "pdf_encrypted_123",
      "requires_password": true
    }
  }
}
```

**No Form Fields Found:**
```json
{
  "success": false,
  "error": {
    "code": "NO_FORM_FIELDS",
    "message": "The PDF does not contain fillable form fields",
    "details": {
      "document_id": "pdf_static_123"
    }
  }
}
```

## SDK Examples

### Python SDK

```python
from agentnode import PDFSkill

# Initialize the client
pdf = PDFSkill(api_key="your_api_key")

# Create a PDF
result = pdf.create(
    title="My Document",
    content=[
        {"type": "text", "element": {"text": "Hello, World!"}}
    ]
)

print(f"PDF created: {result['download_url']}")

# Fill a form
filled = pdf.fill_form(
    document_id="form_123",
    fields=[
        {"field_name": "name", "value": "John Smith"},
        {"field_name": "email", "value": "john@example.com"}
    ]
)

# Extract text
text = pdf.extract_text(document_id="doc_123")
print(f"Extracted: {text['text'][:100]}...")
```

### JavaScript SDK

```javascript
const { PDFSkill } = require('@agentnode/skills');

const pdf = new PDFSkill({ apiKey: 'your_api_key' });

// Create PDF from HTML
const result = await pdf.create({
  html: '<h1>Report</h1><p>Content here...</p>',
  options: { title: 'Generated Report' }
});

console.log(`PDF created: ${result.download_url}`);

// Extract tables
const tables = await pdf.extractTables({
  documentId: 'doc_123',
  outputFormat: 'json'
});

console.log(`Found ${tables.total_tables} tables`);
```
