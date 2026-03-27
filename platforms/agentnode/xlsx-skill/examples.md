# XLSX Skill API Examples

This document provides comprehensive examples for using the XLSX Skill API.

## Authentication

All API requests require authentication via API key:

```bash
curl -X POST "https://api.agentnode.io/v1/skills/xlsx/create" \
  -H "X-API-Key: your_api_key_here" \
  -H "Content-Type: application/json"
```

## Workbook Creation

### Create Basic Workbook

Create a simple workbook with data:

```bash
POST /v1/skills/xlsx/create
```

**Request:**
```json
{
  "options": {
    "title": "Sales Report 2024",
    "author": "Analytics Team"
  },
  "worksheets": [
    {
      "name": "Q1 Sales",
      "data": [
        ["Product", "January", "February", "March", "Total"],
        ["Widget A", 1500, 1700, 1600, "=SUM(B2:D2)"],
        ["Widget B", 1200, 1300, 1400, "=SUM(B3:D3)"],
        ["Widget C", 800, 900, 1000, "=SUM(B4:D4)"],
        ["Total", "=SUM(B2:B4)", "=SUM(C2:C4)", "=SUM(D2:D4)", "=SUM(E2:E4)"]
      ]
    }
  ]
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "xlsx_sales_123",
  "download_url": "https://storage.agentnode.io/xlsx/xlsx_sales_123.xlsx",
  "worksheets": ["Q1 Sales"],
  "metadata": {
    "sheet_count": 1,
    "total_cells": 20,
    "formulas": 8
  },
  "billing": {
    "operation": "create",
    "amount_charged": 0.04
  }
}
```

### Create Workbook with Multiple Sheets

Create a workbook with formatted data across sheets:

```bash
POST /v1/skills/xlsx/create
```

**Request:**
```json
{
  "worksheets": [
    {
      "name": "Data",
      "data": [
        ["ID", "Name", "Department", "Salary"],
        [1, "John Smith", "Engineering", 95000],
        [2, "Jane Doe", "Marketing", 85000],
        [3, "Bob Johnson", "Sales", 78000]
      ],
      "column_widths": {"A": 8, "B": 20, "C": 15, "D": 12}
    },
    {
      "name": "Summary",
      "cells": [
        {
          "reference": "A1",
          "value": "Department Summary",
          "style": {"font": {"bold": true, "size": 14}}
        },
        {
          "reference": "A3",
          "value": "Total Employees"
        },
        {
          "reference": "B3",
          "formula": "COUNTA(Data!A2:A100)"
        },
        {
          "reference": "A4",
          "value": "Average Salary"
        },
        {
          "reference": "B4",
          "formula": "AVERAGE(Data!D2:D100)",
          "style": {"number_format": "\"$\"#,##0.00"}
        }
      ]
    }
  ],
  "named_ranges": [
    {"name": "EmployeeData", "reference": "Data!A1:D100"}
  ]
}
```

## Reading Data

### Read Cell Range

Read data from a specific range:

```bash
POST /v1/skills/xlsx/read
```

**Request:**
```json
{
  "document_id": "xlsx_data_456",
  "sheet_name": "Sheet1",
  "range": "A1:D10",
  "include_formulas": true,
  "include_styles": false
}
```

**Response:**
```json
{
  "success": true,
  "data": [
    ["Product", "Q1", "Q2", "Total"],
    ["Widget A", 1500, 1700, 3200],
    ["Widget B", 1200, 1300, 2500]
  ],
  "formulas": {
    "D2": "SUM(B2:C2)",
    "D3": "SUM(B3:C3)",
    "D4": "SUM(B4:C4)"
  },
  "metadata": {
    "sheet_name": "Sheet1",
    "range": "A1:D10",
    "rows": 3,
    "columns": 4
  },
  "billing": {
    "operation": "read",
    "amount_charged": 0.01
  }
}
```

### Read Full Sheet

Read all data from a worksheet:

```bash
POST /v1/skills/xlsx/read
```

**Request:**
```json
{
  "document_url": "https://example.com/spreadsheet.xlsx",
  "sheet_name": "Data"
}
```

**Response:**
```json
{
  "success": true,
  "data": [
    ["Header1", "Header2", "Header3"],
    ["Value1", "Value2", "Value3"]
  ],
  "metadata": {
    "sheet_name": "Data",
    "total_rows": 100,
    "total_columns": 10,
    "used_range": "A1:J100"
  }
}
```

## Writing Data

### Write Cells with Formulas

Write data with formulas and formatting:

```bash
POST /v1/skills/xlsx/write
```

**Request:**
```json
{
  "document_id": "xlsx_report_789",
  "sheet_name": "Summary",
  "cells": [
    {
      "reference": "A1",
      "value": "Financial Summary",
      "style": {
        "font": {"bold": true, "size": 16, "color": "#1F497D"},
        "alignment": {"horizontal": "center"}
      }
    },
    {
      "reference": "A3",
      "value": "Revenue"
    },
    {
      "reference": "B3",
      "formula": "SUM(Data!B:B)",
      "style": {"number_format": "\"$\"#,##0.00"}
    },
    {
      "reference": "A4",
      "value": "Expenses"
    },
    {
      "reference": "B4",
      "formula": "SUM(Data!C:C)",
      "style": {"number_format": "\"$\"#,##0.00"}
    },
    {
      "reference": "A5",
      "value": "Net Profit",
      "style": {"font": {"bold": true}}
    },
    {
      "reference": "B5",
      "formula": "B3-B4",
      "style": {
        "font": {"bold": true},
        "number_format": "\"$\"#,##0.00"
      }
    }
  ]
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "xlsx_report_789_v2",
  "download_url": "https://storage.agentnode.io/xlsx/xlsx_report_789_v2.xlsx",
  "cells_updated": 6,
  "formulas_added": 3,
  "billing": {
    "operation": "write",
    "amount_charged": 0.02
  }
}
```

### Write 2D Array Data

Write a 2D array of data:

```bash
POST /v1/skills/xlsx/write
```

**Request:**
```json
{
  "document_id": "xlsx_data_123",
  "sheet_name": "Sheet1",
  "data": [
    ["Date", "Product", "Quantity", "Price", "Total"],
    ["2024-01-15", "Widget A", 10, 25.99, 259.90],
    ["2024-01-16", "Widget B", 5, 15.50, 77.50],
    ["2024-01-17", "Widget C", 8, 12.00, 96.00]
  ],
  "start_cell": "A1"
}
```

## Formula Calculation

### Calculate Workbook Formulas

Trigger formula calculation:

```bash
POST /v1/skills/xlsx/calculate
```

**Request:**
```json
{
  "document_id": "xlsx_model_123",
  "full_calculation": true
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "xlsx_model_123",
  "calculation_complete": true,
  "cells_calculated": 250,
  "calculation_time_ms": 850,
  "errors": [
    {
      "cell": "D15",
      "error": "#DIV/0!",
      "message": "Division by zero"
    }
  ],
  "billing": {
    "operation": "calculate",
    "amount_charged": 0.03
  }
}
```

## Pivot Tables

### Create Pivot Table

Create a pivot table from source data:

```bash
POST /v1/skills/xlsx/pivot-table
```

**Request:**
```json
{
  "document_id": "xlsx_sales_data",
  "sheet_name": "Data",
  "source_range": "A1:F1000",
  "destination": "Summary!A1",
  "rows": ["Region"],
  "columns": ["Product"],
  "values": [
    {
      "field": "Sales",
      "function": "sum",
      "name": "Total Sales"
    },
    {
      "field": "Sales",
      "function": "average",
      "name": "Avg Sales"
    }
  ],
  "filters": [
    {
      "field": "Year",
      "values": ["2024"]
    }
  ]
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "xlsx_pivot_123",
  "download_url": "https://storage.agentnode.io/xlsx/xlsx_pivot_123.xlsx",
  "pivot_table": {
    "name": "PivotTable1",
    "location": "Summary!A1",
    "row_count": 10,
    "column_count": 8,
    "source_rows": 1000
  },
  "billing": {
    "operation": "pivot_table",
    "amount_charged": 0.05
  }
}
```

## Charts

### Create Column Chart

Add a chart to a worksheet:

```bash
POST /v1/skills/xlsx/chart
```

**Request:**
```json
{
  "document_id": "xlsx_report_456",
  "sheet_name": "Sheet1",
  "chart": {
    "type": "column",
    "title": "Monthly Sales Performance",
    "data_range": "A1:D5",
    "categories": {
      "range": "A2:A5"
    },
    "series": [
      {
        "name": "Q1",
        "range": "B2:B5"
      },
      {
        "name": "Q2",
        "range": "C2:C5"
      },
      {
        "name": "Q3",
        "range": "D2:D5"
      }
    ],
    "axes": {
      "x_axis": {"title": "Product"},
      "y_axis": {"title": "Units Sold"}
    },
    "legend": {
      "show": true,
      "position": "bottom"
    },
    "position": {
      "sheet": "Sheet1",
      "anchor_cell": "F2",
      "width": 15,
      "height": 10
    }
  }
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "xlsx_chart_789",
  "download_url": "https://storage.agentnode.io/xlsx/xlsx_chart_789.xlsx",
  "chart": {
    "id": "chart_001",
    "type": "column",
    "title": "Monthly Sales Performance"
  },
  "billing": {
    "operation": "chart",
    "amount_charged": 0.03
  }
}
```

### Create Combo Chart

Create a combination chart with multiple types:

```bash
POST /v1/skills/xlsx/chart
```

**Request:**
```json
{
  "document_id": "xlsx_financial_123",
  "chart": {
    "type": "combo",
    "title": "Revenue and Growth Rate",
    "series": [
      {
        "name": "Revenue",
        "range": "B2:B13",
        "chart_type": "column",
        "axis": "primary"
      },
      {
        "name": "Growth %",
        "range": "C2:C13",
        "chart_type": "line",
        "axis": "secondary"
      }
    ]
  }
}
```

## Data Analysis

### Statistical Summary

Perform statistical analysis:

```bash
POST /v1/skills/xlsx/analyze
```

**Request:**
```json
{
  "document_id": "xlsx_data_analysis",
  "sheet_name": "Data",
  "range": "B2:B1000",
  "analysis_type": ["summary", "distribution", "outliers"]
}
```

**Response:**
```json
{
  "success": true,
  "summary": {
    "count": 999,
    "sum": 125000.50,
    "mean": 125.125,
    "median": 118.00,
    "mode": 100.00,
    "std_dev": 35.5,
    "variance": 1260.25,
    "min": 45.00,
    "max": 250.00,
    "range": 205.00
  },
  "distribution": {
    "quartiles": {
      "q1": 95.00,
      "q2": 118.00,
      "q3": 145.00
    },
    "iqr": 50.00,
    "skewness": 0.45,
    "kurtosis": -0.12
  },
  "outliers": {
    "lower_bound": 20.00,
    "upper_bound": 220.00,
    "outliers_found": 12,
    "outlier_values": [250.00, 245.00, 238.00]
  },
  "billing": {
    "operation": "analyze",
    "amount_charged": 0.04
  }
}
```

## Conditional Formatting

### Add Conditional Formatting Rules

Apply conditional formatting:

```bash
POST /v1/skills/xlsx/conditional-format
```

**Request:**
```json
{
  "document_id": "xlsx_dashboard_123",
  "sheet_name": "Dashboard",
  "rules": [
    {
      "range": "B2:B100",
      "type": "color_scale",
      "color_scale": {
        "min_color": "#63BE7B",
        "mid_color": "#FFEB84",
        "max_color": "#F8696B"
      }
    },
    {
      "range": "C2:C100",
      "type": "data_bar",
      "data_bar": {
        "color": "#5B9BD5",
        "show_value": true
      }
    },
    {
      "range": "D2:D100",
      "type": "cell_value",
      "criteria": {
        "operator": "greaterThan",
        "value": 1000
      },
      "format": {
        "font": {"bold": true, "color": "#FF0000"},
        "fill": {"color": "#FFEB9C"}
      }
    }
  ]
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "xlsx_conditional_456",
  "rules_applied": 3,
  "ranges_affected": ["B2:B100", "C2:C100", "D2:D100"],
  "billing": {
    "operation": "conditional_format",
    "amount_charged": 0.02
  }
}
```

## Data Validation

### Add Dropdown Validation

Add data validation with dropdown:

```bash
POST /v1/skills/xlsx/data-validation
```

**Request:**
```json
{
  "document_id": "xlsx_form_123",
  "sheet_name": "Input",
  "validations": [
    {
      "range": "B2:B100",
      "type": "list",
      "formula1": "\"High,Medium,Low\"",
      "show_error": true,
      "error_title": "Invalid Priority",
      "error_message": "Please select High, Medium, or Low"
    },
    {
      "range": "C2:C100",
      "type": "whole",
      "criteria": {
        "operator": "between",
        "value1": 1,
        "value2": 100
      },
      "error_message": "Enter a number between 1 and 100"
    }
  ]
}
```

## Format Conversion

### Convert to CSV

Export spreadsheet as CSV:

```bash
POST /v1/skills/xlsx/convert
```

**Request:**
```json
{
  "document_id": "xlsx_data_export",
  "output_format": "csv",
  "sheet_name": "Data",
  "options": {
    "delimiter": ",",
    "include_headers": true,
    "encoding": "UTF-8"
  }
}
```

**Response:**
```json
{
  "success": true,
  "document_id": "xlsx_converted_csv",
  "download_url": "https://storage.agentnode.io/xlsx/data_export.csv",
  "format": "csv",
  "rows_exported": 1000,
  "billing": {
    "operation": "convert",
    "amount_charged": 0.02
  }
}
```

## Error Handling

### Common Error Responses

**Invalid Range:**
```json
{
  "success": false,
  "error": {
    "code": "INVALID_RANGE",
    "message": "The specified range is invalid",
    "details": {
      "range": "Z999:ZZZ999",
      "max_column": "XFD"
    }
  }
}
```

**Formula Error:**
```json
{
  "success": false,
  "error": {
    "code": "FORMULA_ERROR",
    "message": "Formula calculation error",
    "details": {
      "cell": "D15",
      "formula": "=A15/B15",
      "error_type": "#DIV/0!"
    }
  }
}
```

## SDK Examples

### Python SDK

```python
from agentnode import XLSXSkill

xlsx = XLSXSkill(api_key="your_api_key")

# Create workbook with data
result = xlsx.create(
    worksheets=[{
        "name": "Sales",
        "data": [
            ["Product", "Q1", "Q2"],
            ["Widget A", 1500, 1700]
        ]
    }]
)

print(f"Workbook: {result['download_url']}")

# Add pivot table
pivot = xlsx.pivot_table(
    document_id=result['document_id'],
    source_range="A1:D100",
    rows=["Product"],
    values=[{"field": "Sales", "function": "sum"}]
)

# Calculate formulas
xlsx.calculate(document_id=result['document_id'])
```

### JavaScript SDK

```javascript
const { XLSXSkill } = require('@agentnode/skills');

const xlsx = new XLSXSkill({ apiKey: 'your_api_key' });

// Create with formulas
const result = await xlsx.create({
  worksheets: [{
    name: 'Budget',
    cells: [
      { reference: 'A1', value: 'Total', style: { font: { bold: true } } },
      { reference: 'B1', formula: 'SUM(B2:B100)' }
    ]
  }]
});

console.log(`Created: ${result.download_url}`);

// Read data
const data = await xlsx.read({
  documentId: result.document_id,
  range: 'A1:D10'
});

console.log(`Data: ${JSON.stringify(data.data)}`);
```
