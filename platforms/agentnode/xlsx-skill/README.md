# XLSX Skill - Spreadsheet Analysis and Formulas

## Overview

The XLSX Skill provides comprehensive spreadsheet creation, editing, and analysis capabilities with full support for formulas, formatting, data analysis, and visualization. This skill enables AI agents to programmatically manipulate Excel workbooks, making it essential for financial analysis, reporting, data processing, and business intelligence workflows.

## Key Features

### Spreadsheet Creation
- **Workbook Generation**: Create new Excel workbooks with multiple worksheets
- **Template-Based Creation**: Use pre-defined templates for standard reports
- **Data Import**: Import data from CSV, JSON, databases, and APIs
- **Multi-Sheet Support**: Create and manage multiple worksheets per workbook

### Data Management
- **Cell Operations**: Read, write, and format individual cells and ranges
- **Row/Column Operations**: Insert, delete, hide, and resize rows and columns
- **Data Validation**: Apply validation rules to cells and ranges
- **Conditional Formatting**: Apply dynamic formatting based on cell values

### Formula Support
- **Full Formula Engine**: Support for 400+ Excel functions
- **Array Formulas**: Handle complex array calculations
- **Cross-Sheet References**: Reference data across worksheets
- **Named Ranges**: Create and use named ranges in formulas
- **Formula Auditing**: Trace precedents and dependents

### Data Analysis
- **Pivot Tables**: Create and manipulate pivot tables
- **Charts & Graphs**: Generate visualizations from data
- **Statistical Functions**: Perform statistical analysis on datasets
- **Data Aggregation**: Summarize and group data efficiently

### Advanced Features
- **Macros Support**: Read and execute VBA macros (limited)
- **Protection**: Apply sheet and workbook protection
- **Comments**: Add and manage cell comments
- **Hyperlinks**: Insert links to external resources
- **Styles & Themes**: Apply consistent formatting

## Use Cases

### Financial Applications
- **Financial Modeling**: Build complex financial models and projections
- **Budget Planning**: Create and manage budget spreadsheets
- **Investment Analysis**: Analyze investment portfolios and returns
- **Expense Tracking**: Automate expense report generation

### Business Intelligence
- **Sales Analytics**: Create sales dashboards and reports
- **KPI Tracking**: Monitor key performance indicators
- **Data Consolidation**: Merge data from multiple sources
- **Automated Reporting**: Generate recurring reports automatically

### Operations
- **Inventory Management**: Track and analyze inventory data
- **Project Planning**: Create project schedules and Gantt charts
- **Resource Allocation**: Optimize resource distribution
- **Quality Control**: Analyze quality metrics and trends

### Data Science
- **Data Cleaning**: Prepare and clean datasets for analysis
- **Exploratory Analysis**: Perform initial data exploration
- **Feature Engineering**: Create derived features for ML
- **Results Reporting**: Present analysis results professionally

## Technical Specifications

### Supported Formats
- Input: .xlsx, .xlsm, .xls, .csv, .tsv, .ods
- Output: .xlsx, .xlsm, .csv, .pdf, .html

### Document Limits
- Maximum file size: 100 MB
- Maximum worksheets: 256
- Maximum rows: 1,048,576
- Maximum columns: 16,384
- Maximum cell styles: 64,000

### Formula Support
- 400+ built-in Excel functions
- Custom function support
- Array formulas
- Dynamic arrays (Excel 365 style)
- Lambda functions

### API Performance
- Workbook creation: 2-5 seconds
- Data read: 1-3 seconds per 10,000 cells
- Formula calculation: 1-10 seconds
- Chart generation: 2-4 seconds

## Integration Capabilities

### Native Integrations
- Google Sheets (import/export)
- Microsoft OneDrive (import/export)
- AWS S3 (import/export)
- Azure Blob Storage (import/export)
- Database connectors (MySQL, PostgreSQL, SQL Server)

### Data Source Support
- REST APIs (JSON import)
- SQL databases
- CSV/TSV files
- XML data
- JSON files

## Security and Compliance

- **Data Encryption**: AES-256 encryption for workbooks at rest
- **Transmission Security**: TLS 1.3 for all API communications
- **Data Retention**: Configurable retention policies
- **Access Control**: Role-based access with API key authentication
- **Formula Security**: Protection against malicious formulas

## Chart Types Supported

- Column charts (clustered, stacked, 100% stacked)
- Bar charts (clustered, stacked, 100% stacked)
- Line charts (simple, stacked, 100% stacked)
- Area charts (simple, stacked, 100% stacked)
- Pie and doughnut charts
- Scatter plots
- Bubble charts
- Combo charts
- Histograms
- Box and whisker plots
- Waterfall charts
- Funnel charts
- Treemap
- Sunburst

## Getting Started

1. **Install the Skill**: Add the XLSX skill to your AgentNode workspace
2. **Configure Authentication**: Set up your API credentials
3. **Choose Your Operation**: Create, edit, analyze, or convert
4. **Process Spreadsheets**: Upload or reference your Excel files

## Pricing

See [monetization.md](./monetization.md) for detailed pricing information.

## Examples

See [examples.md](./examples.md) for API usage examples and code snippets.

## Support

- Documentation: [docs.agentnode.io/skills/xlsx](https://docs.agentnode.io/skills/xlsx)
- Community: [community.agentnode.io](https://community.agentnode.io)
- Enterprise Support: enterprise@agentnode.io
