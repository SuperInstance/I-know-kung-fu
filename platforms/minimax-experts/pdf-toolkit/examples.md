# PDF Toolkit Examples

## Example 1: Extracting Invoice Data

### User Request
```
Extract all tables from this invoice PDF: /invoices/vendor_invoice_2024.pdf
Convert to Excel format with each table on a separate sheet.
```

### Agent Response
```
Processing your invoice PDF for table extraction...

[Analyzing document structure...]
[Detecting tables...]
[Extracting data...]

✅ Table Extraction Complete:

**Document Analysis:**
- Source: vendor_invoice_2024.pdf
- Pages: 3
- Tables detected: 3

**Extracted Tables:**

📄 Table 1 - Invoice Header (Page 1)
| Field | Value |
|-------|-------|
| Invoice Number | INV-2024-4521 |
| Date | November 15, 2024 |
| Vendor | TechSupply Inc. |
| Due Date | December 15, 2024 |

📄 Table 2 - Line Items (Page 1)
| Item | Description | Qty | Unit Price | Total |
|------|-------------|-----|------------|-------|
| SKU-001 | Server Rack | 2 | $1,200.00 | $2,400.00 |
| SKU-002 | Cable Set | 50 | $15.00 | $750.00 |
| SKU-003 | UPS Battery | 4 | $350.00 | $1,400.00 |
| SKU-004 | Network Switch | 3 | $450.00 | $1,350.00 |

📄 Table 3 - Summary (Page 1)
| Description | Amount |
|-------------|--------|
| Subtotal | $5,900.00 |
| Tax (8%) | $472.00 |
| Total | $6,372.00 |

**Output File:** vendor_invoice_2024_tables.xlsx
- Sheet 1: Invoice Header
- Sheet 2: Line Items
- Sheet 3: Summary

Would you like me to:
1. Validate the extracted data for accuracy
2. Create a database-ready CSV format
3. Process additional invoices in the same format
```

---

## Example 2: Merging Quarterly Reports

### User Request
```
Merge these quarterly reports into a single annual report:
- /reports/Q1_2024.pdf
- /reports/Q2_2024.pdf
- /reports/Q3_2024.pdf
- /reports/Q4_2024.pdf

Add a cover page and table of contents. Maintain page numbering sequentially.
```

### Agent Response
```
Processing document merge with cover page and TOC...

[Loading documents...]
[Analyzing structure...]
[Generating cover page...]
[Creating table of contents...]
[Merging documents...]

✅ Annual Report Generated:

**Merge Summary:**
```
Cover Page (Auto-generated)
├── Company Annual Report 2024
├── Generated: December 2024
└── Confidential

Table of Contents (Auto-generated)
├── Q1 Report ............... Page 1
├── Q2 Report ............... Page 15
├── Q3 Report ............... Page 28
└── Q4 Report ............... Page 42

[Content]
Q1 Report (14 pages)
├── Executive Summary
├── Financial Highlights
├── Operational Metrics
└── Outlook

Q2 Report (13 pages)
├── Executive Summary
├── Financial Highlights
├── Operational Metrics
└── Outlook

Q3 Report (14 pages)
├── Executive Summary
├── Financial Highlights
├── Operational Metrics
└── Outlook

Q4 Report (15 pages)
├── Executive Summary
├── Financial Highlights
├── Operational Metrics
└── Year-End Summary
```

**Document Statistics:**
- Total pages: 58 (including cover and TOC)
- File size: 4.2 MB
- Sequential page numbering: Applied
- Bookmarks: Added for each quarter

**Output:** Annual_Report_2024.pdf

Would you like me to:
1. Add page headers with document title
2. Include page footers with page numbers
3. Apply password protection
```

---

## Example 3: Form Filling Automation

### User Request
```
Fill out the W-4 tax form at /forms/w4_template.pdf using this employee data:
- Name: Jennifer Martinez
- SSN: 234-56-7890
- Address: 123 Oak Street, Springfield, IL 62701
- Filing Status: Single
- Allowances: 2
- Additional withholding: $50
```

### Agent Response
```
Processing form fill operation...

[Loading form template...]
[Mapping fields...]
[Validating data...]
[Filling form fields...]

✅ Form Filled Successfully:

**W-4 Tax Form - Field Mapping:**

| Field | Value | Status |
|-------|-------|--------|
| First name and middle initial | Jennifer | ✅ |
| Last name | Martinez | ✅ |
| Social security number | 234-56-7890 | ✅ |
| Home address | 123 Oak Street | ✅ |
| City, state, ZIP | Springfield, IL 62701 | ✅ |
| Filing status (Step 1) | Single (c) | ✅ |
| Multiple jobs (Step 2) | Not applicable | ✅ |
| Dependents (Step 3) | $0 | ✅ |
| Other income (Step 4a) | $0 | ✅ |
| Deductions (Step 4b) | $0 | ✅ |
| Extra withholding (Step 4c) | $50 | ✅ |

**Form Validation:**
✅ All required fields completed
✅ SSN format valid
✅ Numerical values within range
✅ Signature field ready

**Output:** w4_jennifer_martinez_filled.pdf
- Status: Ready for signature
- Can be flattened for submission

Would you like me to:
1. Flatten the form to prevent editing
2. Generate a preview image
3. Process additional employee W-4 forms
```

---

## Example 4: PDF Security and Protection

### User Request
```
Add security to the contract at /contracts/client_agreement.pdf:
- Set user password: "Client2024"
- Allow printing only
- Prevent copying and editing
- Add a visible watermark "CONFIDENTIAL"
```

### Agent Response
```
Applying security settings to document...

[Loading document...]
[Applying encryption...]
[Setting permissions...]
[Adding watermark...]
[Generating protected PDF...]

✅ Security Applied Successfully:

**Protection Settings:**

🔐 Encryption
- Standard: AES-256
- User password: Client2024
- Owner password: [System-generated]

📋 Permissions
| Action | Status |
|--------|--------|
| Print | ✅ Allowed |
| Copy text | ❌ Denied |
| Edit document | ❌ Denied |
| Annotate | ❌ Denied |
| Fill forms | ❌ Denied |
| Extract pages | ❌ Denied |

💧 Watermark Applied
- Text: "CONFIDENTIAL"
- Position: Diagonal, center
- Font: Arial Bold, 72pt
- Color: Light gray, 30% opacity
- Applied to: All pages

**Output:** client_agreement_protected.pdf
- Original size: 856 KB
- Protected size: 862 KB
- Pages: 12

Would you like me to:
1. Test the password protection
2. Generate a shareable link with expiry
3. Apply the same settings to other documents
```

---

## Example 5: OCR and Text Extraction

### User Request
```
Extract text from this scanned document: /scanned/old_contract.pdf
The scan quality is not great, so please use OCR. Output as both text and searchable PDF.
```

### Agent Response
```
Processing scanned document with OCR...

[Analyzing scan quality...]
[Detecting text regions...]
[Running OCR engine...]
[Post-processing results...]
[Creating searchable PDF...]

✅ OCR Processing Complete:

**Document Analysis:**
- Source: old_contract.pdf
- Type: Scanned document
- Pages: 5
- Scan quality: Medium (200 DPI)
- Detected language: English

**OCR Results:**

📊 Extraction Statistics
| Metric | Value |
|--------|-------|
| Characters extracted | 12,456 |
| Words extracted | 2,128 |
| Confidence score | 94.2% |
| Low confidence areas | 8 |

⚠️ Areas Flagged for Review:
- Page 2, Line 15: "agreem_nt" → Likely: "agreement"
- Page 3, Line 8: "$1__,000" → Likely: "$1,500.00"
- Page 4, Line 22: Unclear signature text

**Extracted Text Preview:**
```
LEASE AGREEMENT

This Lease Agreement is entered into as of January 15, 1998, 
by and between ABC Properties LLC ("Landlord") and XYZ 
Corporation ("Tenant").

PROPERTY: The Landlord agrees to lease to Tenant the 
commercial property located at 456 Business Park Drive...

[Full text continues in output file]
```

**Output Files Generated:**
1. old_contract_text.txt (plain text)
2. old_contract_searchable.pdf (searchable PDF with invisible text layer)

**Recommendations:**
- Review flagged areas for accuracy
- Original scan could benefit from 300+ DPI for better OCR

Would you like me to:
1. Highlight low-confidence areas in the output
2. Extract specific sections or clauses
3. Compare with a modern contract template
```
