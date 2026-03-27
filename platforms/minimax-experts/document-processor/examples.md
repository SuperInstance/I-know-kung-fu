# Document Processor Examples

## Example 1: Creating a Business Report

### User Request
```
Create a quarterly sales report for Q3 2024. Include sections for:
- Executive Summary
- Regional Performance
- Key Metrics
- Recommendations
Use our company template with blue accent colors.
```

### Agent Response
```
I'll create your Q3 2024 Sales Report using your company template. Let me 
set up the document with the requested sections.

[Creating document...]

Document created successfully! Here's what I've included:

📄 Q3 2024 Sales Report
├── Title Page with company branding
├── Table of Contents
├── Executive Summary (placeholder)
├── Regional Performance
│   ├── North America
│   ├── Europe
│   ├── Asia-Pacific
│   └── Latin America
├── Key Metrics
│   ├── Revenue by Product
│   ├── Customer Acquisition
│   └── Churn Analysis
├── Recommendations
└── Appendix

Style applied: Company Blue Theme
- Headings: Dark Blue (#1E3A5F)
- Accent: Light Blue (#4A90D9)
- Body: Calibri 11pt

The document is ready for your data input. Would you like me to:
1. Add sample data for review
2. Insert specific charts or tables
3. Apply any additional formatting
```

---

## Example 2: Modifying an Existing Contract

### User Request
```
Update the employment contract at /contracts/standard_employment.docx:
- Change the notice period from 2 weeks to 4 weeks
- Add a non-compete clause after section 5
- Update the effective date to January 1, 2025
Keep track changes enabled for legal review.
```

### Agent Response
```
I'll process your contract modifications with tracked changes enabled.

[Processing document...]

Modifications Applied:

✅ Notice Period Updated
- Location: Section 3, Paragraph 2
- Original: "two (2) weeks' written notice"
- New: "four (4) weeks' written notice"
- Status: Tracked (awaiting acceptance)

✅ Non-Compete Clause Added
- Location: After Section 5
- Content inserted:
  "Section 6: Non-Competition Agreement
   For a period of twelve (12) months following termination..."
- Status: Tracked (awaiting acceptance)

✅ Effective Date Updated
- Location: Preamble
- Original: "effective as of July 1, 2024"
- New: "effective as of January 1, 2025"
- Status: Tracked (awaiting acceptance)

Document Summary:
- Total changes: 3
- Deletions: 2
- Insertions: 2
- Word count: 2,847

Ready for legal review. Would you like me to:
1. Generate a clean copy alongside the tracked version
2. Add comments explaining the changes
3. Export to PDF for signature preparation
```

---

## Example 3: Extracting and Analyzing Document Structure

### User Request
```
Analyze the document at /reports/annual_report.docx and tell me:
1. How many sections does it have?
2. Are there any formatting inconsistencies?
3. Extract all table data to CSV
```

### Agent Response
```
Analyzing your annual report document...

[Processing document...]

📊 Document Analysis Results:

**Structure Summary:**
- Total Pages: 24
- Total Words: 8,432
- Sections: 12 main sections
- Subsections: 34
- Tables: 7
- Images: 15

**Section Breakdown:**
1. Executive Summary (1 page)
2. Company Overview (2 pages)
3. Financial Performance (4 pages)
4. Market Analysis (3 pages)
5. Product Development (2 pages)
6. Human Resources (2 pages)
7. Risk Management (2 pages)
8. Sustainability Report (3 pages)
9. Corporate Governance (2 pages)
10. Future Outlook (1 page)
11. Appendices (3 pages)
12. Glossary (1 page)

⚠️ Formatting Inconsistencies Found:

| Issue | Location | Details |
|-------|----------|---------|
| Font mismatch | Section 4, para 3 | Arial instead of Calibri |
| Inconsistent spacing | Section 7 | 1.5 line spacing vs 1.0 |
| Heading style | Section 9 | H3 instead of H2 |
| Table border | Table 5 | Mixed border styles |

**Tables Extracted:**
✅ table_1_financial_summary.csv
✅ table_2_regional_revenue.csv
✅ table_3_product_performance.csv
✅ table_4_employee_metrics.csv
✅ table_5_market_share.csv
✅ table_6_sustainability_kpis.csv
✅ table_7_risk_matrix.csv

All CSV files saved to /exports/

Would you like me to:
1. Fix the formatting inconsistencies automatically
2. Generate a formatting guide for this document
3. Create a summary document from the extracted tables
```

---

## Example 4: Merging Multiple Documents

### User Request
```
Merge these three proposal documents into one consolidated proposal:
- /proposals/technical_approach.docx
- /proposals/pricing_model.docx
- /proposals/team_qualifications.docx
Add page breaks between sections and create a unified table of contents.
```

### Agent Response
```
Merging your proposal documents with unified formatting...

[Processing 3 documents...]

🔄 Document Merge Complete:

**Consolidated Structure:**
```
Technical Approach
├── Introduction
├── Methodology
├── Timeline
├── Deliverables
└── Quality Assurance

[Page Break]

Pricing Model
├── Cost Breakdown
├── Payment Schedule
├── Terms and Conditions
└── Optional Services

[Page Break]

Team Qualifications
├── Key Personnel
├── Organizational Chart
├── Past Performance
└── Certifications
```

**Formatting Applied:**
✅ Unified heading styles (Heading 1-3)
✅ Consistent fonts (Calibri body, Arial headings)
✅ Page breaks between sections
✅ Generated Table of Contents
✅ Updated page numbers
✅ Unified header/footer

**Document Statistics:**
- Combined pages: 28
- Total words: 9,847
- Tables: 12
- Images: 8

Saved to: /proposals/consolidated_proposal.docx

Would you like me to:
1. Add a cover page with project details
2. Include an executive summary
3. Export to PDF for submission
```

---

## Example 5: Template-Based Document Generation

### User Request
```
Generate 50 personalized offer letters using the template at 
/templates/offer_letter.docx and the candidate data in 
/data/candidates.csv. Each letter should include:
- Candidate name
- Position title
- Start date
- Salary
- Manager name
```

### Agent Response
```
Processing bulk document generation from template and data source...

[Loading template...]
[Reading 50 candidate records...]
[Generating personalized letters...]

✅ Bulk Generation Complete:

**Summary:**
- Template: offer_letter.docx
- Records processed: 50
- Documents generated: 50
- Errors: 0

**Output Location:** /generated/offers/

**Sample Output (first 3):**
1. offer_john_smith_20241215.docx
   - Position: Senior Developer
   - Start Date: January 15, 2025
   - Manager: Sarah Johnson

2. offer_emily_chen_20241215.docx
   - Position: Product Manager
   - Start Date: February 1, 2025
   - Manager: Michael Brown

3. offer_robert_williams_20241215.docx
   - Position: UX Designer
   - Start Date: January 22, 2025
   - Manager: Lisa Park

**Fields Mapped:**
✅ {{candidate_name}} → Name column
✅ {{position}} → Job_Title column
✅ {{start_date}} → Start_Date column
✅ {{salary}} → Annual_Salary column (formatted with commas)
✅ {{manager_name}} → Hiring_Manager column

All documents maintain consistent formatting from the template.

Would you like me to:
1. Convert all letters to PDF for email distribution
2. Generate a summary spreadsheet of all offers
3. Set up email merge for distribution
```
