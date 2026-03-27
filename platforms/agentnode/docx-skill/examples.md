# DOCX Skill API Examples

This document provides comprehensive examples for using the DOCX Skill API. All examples include request payloads and expected responses.

## Authentication

All API requests require authentication via API key:

```bash
curl -X POST "https://api.agentnode.io/v1/skills/docx/create" \
  -H "X-API-Key: your_api_key_here" \
  -H "Content-Type: application/json"
```

## Document Creation

### Basic Document Creation

Create a simple document with paragraphs:

```bash
POST /v1/skills/docx/create
```

**Request:**
```json
{
  "options": {
    "title": "Meeting Minutes",
    "author": "John Smith"
  },
  "content": [
    {
      "type": "paragraph",
      "paragraph": {
        "text": "Q4 Planning Meeting Minutes",
        "style": "Title",
        "alignment": "center"
      }
    },
    {
      "type": "paragraph",
      "paragraph": {
        "text": "Date: December 15, 2024",
        "style": "Normal"
      }
    },
    {
      "type": "paragraph",
      "paragraph": {
        "text": "Attendees",
        "style": "Heading1"
      }
    },
    {
      "type": "paragraph",
      "paragraph": {
        "text": "John Smith, Jane Doe, Bob Johnson",
        "style": "Normal"
      }
    }
  ]
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "doc_a1b2c3d4e5f6",
  "download_url": "https://storage.agentnode.io/docs/doc_a1b2c3d4e5f6.docx",
  "metadata": {
    "page_count": 1,
    "word_count": 18,
    "created_at": "2024-12-15T10:30:00Z",
    "expires_at": "2024-12-22T10:30:00Z"
  },
  "billing": {
    "operation": "document_create",
    "amount_charged": 0.05,
    "currency": "USD"
  }
}
```

### Document with Tables

Create a document containing a formatted table:

```bash
POST /v1/skills/docx/create
```

**Request:**
```json
{
  "options": {
    "title": "Sales Report Q4 2024",
    "author": "Analytics Team"
  },
  "content": [
    {
      "type": "paragraph",
      "paragraph": {
        "text": "Quarterly Sales Summary",
        "style": "Heading1"
      }
    },
    {
      "type": "table",
      "table": {
        "rows": [
          [
            {"content": [{"text": "Region", "bold": true}]},
            {"content": [{"text": "Q4 Sales", "bold": true}]},
            {"content": [{"text": "Growth", "bold": true}]}
          ],
          [
            {"content": [{"text": "North America"}]},
            {"content": [{"text": "$2,450,000"}]},
            {"content": [{"text": "+12%", "color": "#00AA00"}]}
          ],
          [
            {"content": [{"text": "Europe"}]},
            {"content": [{"text": "$1,890,000"}]},
            {"content": [{"text": "+8%", "color": "#00AA00"}]}
          ],
          [
            {"content": [{"text": "Asia Pacific"}]},
            {"content": [{"text": "$1,234,000"}]},
            {"content": [{"text": "+15%", "color": "#00AA00"}]}
          ]
        ],
        "style": "Table Grid",
        "border": {
          "style": "single",
          "width": 1,
          "color": "#000000"
        }
      }
    }
  ]
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "doc_table_abc123",
  "download_url": "https://storage.agentnode.io/docs/doc_table_abc123.docx",
  "metadata": {
    "page_count": 1,
    "word_count": 25,
    "tables": 1
  },
  "billing": {
    "operation": "document_create",
    "amount_charged": 0.05
  }
}
```

### Document with Images

Create a document with embedded images:

```bash
POST /v1/skills/docx/create
```

**Request:**
```json
{
  "content": [
    {
      "type": "paragraph",
      "paragraph": {
        "text": "Product Overview",
        "style": "Title"
      }
    },
    {
      "type": "image",
      "image": {
        "source": "https://example.com/product-image.png",
        "width": 4.5,
        "height": 3.0,
        "alignment": "center",
        "caption": "Figure 1: Product Dashboard Screenshot"
      }
    },
    {
      "type": "paragraph",
      "paragraph": {
        "text": "The dashboard provides real-time analytics...",
        "style": "Normal"
      }
    }
  ]
}
```

## Document Editing

### Basic Text Replacement

Replace text in an existing document:

```bash
POST /v1/skills/docx/edit
```

**Request:**
```json
{
  "document_id": "doc_a1b2c3d4e5f6",
  "operations": [
    {
      "action": "replace",
      "find": "December 15, 2024",
      "replace": "January 10, 2025"
    },
    {
      "action": "replace",
      "find": "John Smith",
      "replace": "Robert Smith"
    }
  ]
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "doc_a1b2c3d4e5f6_v2",
  "download_url": "https://storage.agentnode.io/docs/doc_a1b2c3d4e5f6_v2.docx",
  "changes_applied": 2,
  "billing": {
    "operation": "document_edit",
    "amount_charged": 0.03
  }
}
```

### Edit with Tracked Changes

Edit a document with revision tracking enabled:

```bash
POST /v1/skills/docx/edit
```

**Request:**
```json
{
  "document_id": "doc_contract_xyz",
  "track_changes": true,
  "operations": [
    {
      "action": "insert",
      "position": {
        "paragraph_index": 5,
        "character_index": 0
      },
      "content": {
        "text": "This amendment is effective as of the signature date below.",
        "author": "Legal Team"
      }
    },
    {
      "action": "delete",
      "position": {
        "paragraph_index": 8,
        "start": 15,
        "end": 45
      }
    }
  ]
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "doc_contract_xyz_tracked",
  "download_url": "https://storage.agentnode.io/docs/doc_contract_xyz_tracked.docx",
  "tracked_changes": {
    "insertions": 1,
    "deletions": 1,
    "authors": ["Legal Team"]
  },
  "billing": {
    "operation": "tracked_changes",
    "amount_charged": 0.04
  }
}
```

## Text Extraction

### Extract All Text

Extract plain text from a document:

```bash
POST /v1/skills/docx/extract-text
```

**Request:**
```json
{
  "document_id": "doc_a1b2c3d4e5f6"
}
```

**Response:**
```json
{
  "success": true,
  "text": "Q4 Planning Meeting Minutes\n\nDate: December 15, 2024\n\nAttendees\nJohn Smith, Jane Doe, Bob Johnson\n\nAgenda Items...",
  "pages": [
    {
      "page_number": 1,
      "text": "Q4 Planning Meeting Minutes\n\nDate: December 15, 2024..."
    },
    {
      "page_number": 2,
      "text": "Agenda Items..."
    }
  ],
  "metadata": {
    "page_count": 2,
    "word_count": 450,
    "character_count": 2890
  },
  "billing": {
    "operation": "text_extract",
    "amount_charged": 0.01
  }
}
```

### Extract with Page Range

Extract text from specific pages:

```bash
POST /v1/skills/docx/extract-text
```

**Request:**
```json
{
  "document_url": "https://example.com/documents/report.docx",
  "page_range": {
    "start": 1,
    "end": 5
  },
  "include_formatting": true
}
```

**Response:**
```json
{
  "success": true,
  "text": "**Executive Summary**\n\nThis report presents findings...",
  "pages": [
    {"page_number": 1, "text": "**Executive Summary**..."},
    {"page_number": 2, "text": "..."},
    {"page_number": 3, "text": "..."},
    {"page_number": 4, "text": "..."},
    {"page_number": 5, "text": "..."}
  ],
  "metadata": {
    "total_pages_in_document": 25,
    "pages_extracted": 5
  },
  "billing": {
    "operation": "text_extract",
    "amount_charged": 0.01
  }
}
```

## Document Merging

### Merge Multiple Documents

Combine multiple documents into one:

```bash
POST /v1/skills/docx/merge
```

**Request:**
```json
{
  "documents": [
    {"document_id": "doc_cover_page"},
    {"document_url": "https://example.com/docs/intro.docx"},
    {"document_id": "doc_main_content"}
  ],
  "insert_page_break": true,
  "preserve_formatting": true
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "doc_merged_xyz789",
  "download_url": "https://storage.agentnode.io/docs/doc_merged_xyz789.docx",
  "source_count": 3,
  "total_pages": 42,
  "merge_details": [
    {"source": "doc_cover_page", "pages_added": 1},
    {"source": "intro.docx", "pages_added": 5},
    {"source": "doc_main_content", "pages_added": 36}
  ],
  "billing": {
    "operation": "document_merge",
    "amount_charged": 0.08
  }
}
```

## Format Conversion

### Convert to PDF

Convert a DOCX document to PDF:

```bash
POST /v1/skills/docx/convert
```

**Request:**
```json
{
  "document_id": "doc_a1b2c3d4e5f6",
  "output_format": "pdf",
  "options": {
    "page_size": "A4",
    "embed_fonts": true,
    "quality": "high"
  }
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "doc_a1b2c3d4e5f6_pdf",
  "download_url": "https://storage.agentnode.io/docs/doc_a1b2c3d4e5f6_pdf.pdf",
  "format": "pdf",
  "file_size_kb": 245,
  "billing": {
    "operation": "format_conversion",
    "amount_charged": 0.03
  }
}
```

### Convert to HTML

Convert a document to HTML format:

```bash
POST /v1/skills/docx/convert
```

**Request:**
```json
{
  "document_id": "doc_report_123",
  "output_format": "html",
  "options": {
    "include_styles": true,
    "embed_images": true,
    "encoding": "UTF-8"
  }
}
```

## Document Analysis

### Analyze Document Structure

Analyze the structure and content of a document:

```bash
POST /v1/skills/docx/analyze
```

**Request:**
```json
{
  "document_id": "doc_report_123",
  "analysis_type": ["structure", "headings", "tables", "metadata"]
}
```

**Response:**
```json
{
  "success": true,
  "structure": {
    "headings": [
      {"level": 1, "text": "Executive Summary", "page": 1},
      {"level": 1, "text": "Introduction", "page": 2},
      {"level": 2, "text": "Background", "page": 2},
      {"level": 2, "text": "Objectives", "page": 3},
      {"level": 1, "text": "Methodology", "page": 4}
    ],
    "sections": 8,
    "tables": 3,
    "images": 5,
    "footnotes": 12
  },
  "tables_summary": [
    {"index": 1, "rows": 5, "columns": 4, "page": 6},
    {"index": 2, "rows": 10, "columns": 3, "page": 12},
    {"index": 3, "rows": 8, "columns": 5, "page": 18}
  ],
  "metadata": {
    "title": "Annual Report 2024",
    "author": "Finance Department",
    "created": "2024-12-01T09:00:00Z",
    "modified": "2024-12-15T14:30:00Z",
    "word_count": 8500,
    "page_count": 35
  },
  "billing": {
    "operation": "analyze",
    "amount_charged": 0.02
  }
}
```

## Tracked Changes Management

### List All Tracked Changes

Retrieve all tracked changes in a document:

```bash
POST /v1/skills/docx/tracked-changes
```

**Request:**
```json
{
  "document_id": "doc_contract_v2",
  "action": "list"
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "doc_contract_v2",
  "changes": [
    {
      "change_id": "tc_001",
      "type": "insert",
      "author": "John Smith",
      "date": "2024-12-10T14:30:00Z",
      "text": "Additional clause for warranty terms.",
      "position": {"paragraph": 12, "start": 0, "end": 45}
    },
    {
      "change_id": "tc_002",
      "type": "delete",
      "author": "Jane Doe",
      "date": "2024-12-11T09:15:00Z",
      "text": "Original payment terms paragraph",
      "position": {"paragraph": 15}
    },
    {
      "change_id": "tc_003",
      "type": "insert",
      "author": "John Smith",
      "date": "2024-12-12T11:45:00Z",
      "text": "Revised payment terms with 30-day extension option."
    }
  ],
  "total_changes": 3,
  "billing": {
    "operation": "tracked_changes",
    "amount_charged": 0.04
  }
}
```

### Accept All Changes

Accept all tracked changes:

```bash
POST /v1/skills/docx/tracked-changes
```

**Request:**
```json
{
  "document_id": "doc_contract_v2",
  "action": "accept_all"
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "doc_contract_v2_accepted",
  "download_url": "https://storage.agentnode.io/docs/doc_contract_v2_accepted.docx",
  "changes_accepted": 3,
  "billing": {
    "operation": "tracked_changes",
    "amount_charged": 0.04
  }
}
```

## Comments Management

### Add Comment

Add a comment to a document:

```bash
POST /v1/skills/docx/comments
```

**Request:**
```json
{
  "document_id": "doc_report_123",
  "action": "add",
  "comment": {
    "text": "Please verify these figures with the finance team.",
    "author": "Reviewer",
    "position": {
      "paragraph_index": 15,
      "start": 20,
      "end": 45
    }
  }
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "doc_report_123",
  "comment_id": "cmt_abc123",
  "billing": {
    "operation": "comments",
    "amount_charged": 0.02
  }
}
```

### List Comments

Retrieve all comments:

```bash
POST /v1/skills/docx/comments
```

**Request:**
```json
{
  "document_id": "doc_report_123",
  "action": "list"
}
```

**Response:**
```json
{
  "success": true,
  "comments": [
    {
      "comment_id": "cmt_abc123",
      "author": "Reviewer",
      "text": "Please verify these figures...",
      "resolved": false,
      "created": "2024-12-15T10:00:00Z",
      "position": {"paragraph": 15}
    },
    {
      "comment_id": "cmt_def456",
      "author": "Editor",
      "text": "Good section, no changes needed",
      "resolved": true,
      "created": "2024-12-14T15:30:00Z"
    }
  ],
  "total_comments": 2,
  "unresolved": 1
}
```

## Batch Operations

### Process Multiple Documents

Execute multiple operations in a single request:

```bash
POST /v1/skills/docx/batch
```

**Request:**
```json
{
  "operations": [
    {
      "operation_id": "op_001",
      "type": "create",
      "params": {
        "content": [{"type": "paragraph", "paragraph": {"text": "Document 1"}}]
      }
    },
    {
      "operation_id": "op_002",
      "type": "extract",
      "params": {
        "document_id": "doc_existing_123"
      }
    },
    {
      "operation_id": "op_003",
      "type": "convert",
      "params": {
        "document_id": "doc_existing_456",
        "output_format": "pdf"
      }
    }
  ]
}
```

**Response:**
```json
{
  "success": true,
  "batch_id": "batch_xyz789",
  "status": "completed",
  "results": [
    {
      "operation_id": "op_001",
      "status": "success",
      "document_id": "doc_new_001",
      "download_url": "https://storage.agentnode.io/docs/doc_new_001.docx"
    },
    {
      "operation_id": "op_002",
      "status": "success",
      "text": "Extracted content..."
    },
    {
      "operation_id": "op_003",
      "status": "success",
      "download_url": "https://storage.agentnode.io/docs/doc_existing_456.pdf"
    }
  ],
  "billing": {
    "total_charged": 0.09,
    "breakdown": {
      "create": 0.05,
      "extract": 0.01,
      "convert": 0.03
    }
  }
}
```

## Error Handling

### Common Error Responses

**Document Not Found:**
```json
{
  "success": false,
  "error": {
    "code": "DOCUMENT_NOT_FOUND",
    "message": "The specified document could not be found",
    "details": {
      "document_id": "doc_invalid_123"
    }
  }
}
```

**Rate Limit Exceeded:**
```json
{
  "success": false,
  "error": {
    "code": "RATE_LIMIT_EXCEEDED",
    "message": "Rate limit exceeded. Please retry after 60 seconds",
    "details": {
      "retry_after": 60,
      "limit": "100 requests per minute"
    }
  }
}
```

**Invalid Format:**
```json
{
  "success": false,
  "error": {
    "code": "INVALID_FORMAT",
    "message": "The document format is not supported",
    "details": {
      "provided_format": ".odt",
      "supported_formats": [".docx", ".doc", ".dotx"]
    }
  }
}
```

## SDK Examples

### Python SDK

```python
from agentnode import DocxSkill

# Initialize the client
client = DocxSkill(api_key="your_api_key")

# Create a document
result = client.create(
    title="My Document",
    author="Developer",
    content=[
        {"type": "paragraph", "text": "Hello, World!", "style": "Title"},
        {"type": "paragraph", "text": "This is the content."}
    ]
)

print(f"Document created: {result['download_url']}")

# Extract text
text = client.extract_text(document_id=result['document_id'])
print(f"Extracted: {text['text']}")
```

### JavaScript SDK

```javascript
const { DocxSkill } = require('@agentnode/skills');

const docx = new DocxSkill({ apiKey: 'your_api_key' });

// Create a document
const result = await docx.create({
  title: 'My Document',
  content: [
    { type: 'paragraph', paragraph: { text: 'Hello, World!', style: 'Title' } }
  ]
});

console.log(`Document created: ${result.download_url}`);

// Convert to PDF
const pdf = await docx.convert({
  documentId: result.document_id,
  outputFormat: 'pdf'
});

console.log(`PDF available: ${pdf.download_url}`);
```
