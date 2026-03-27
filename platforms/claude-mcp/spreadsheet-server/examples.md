# Spreadsheet Server - Usage Examples

## Read Spreadsheet

```json
{
  "name": "read_spreadsheet",
  "arguments": {
    "path": "/data/sales.xlsx",
    "sheet": "Q1 Sales",
    "range": "A1:D10",
    "options": {
      "includeFormulas": true,
      "headerRow": 1
    }
  }
}
```

**Response:**
```json
{
  "headers": ["Product", "Q1 Sales", "Q2 Sales", "Total"],
  "data": [
    ["Widget A", 15000, 18000, { "formula": "=B2+C2", "value": 33000 }],
    ["Widget B", 12000, 14500, { "formula": "=B3+C3", "value": 26500 }]
  ],
  "rowCount": 9,
  "columnCount": 4
}
```

## Create Spreadsheet

```json
{
  "name": "create_spreadsheet",
  "arguments": {
    "path": "/output/report.xlsx",
    "format": "xlsx",
    "sheets": [
      {
        "name": "Summary",
        "data": [
          ["Category", "Amount"],
          ["Sales", 50000],
          ["Expenses", 30000]
        ]
      }
    ]
  }
}
```

## Write Cells

```json
{
  "name": "write_cells",
  "arguments": {
    "path": "/data/report.xlsx",
    "sheet": "Sheet1",
    "range": "A1:B2",
    "data": [
      ["Name", "Value"],
      ["Revenue", 100000]
    ]
  }
}
```

## Analyze Data

```json
{
  "name": "analyze_data",
  "arguments": {
    "path": "/data/sales.xlsx",
    "sheet": "Sales",
    "analysis": "stats",
    "options": {
      "columns": ["Amount", "Quantity"]
    }
  }
}
```

**Response:**
```json
{
  "stats": {
    "Amount": {
      "sum": 150000,
      "avg": 1500,
      "min": 100,
      "max": 5000,
      "count": 100
    },
    "Quantity": {
      "sum": 5000,
      "avg": 50,
      "min": 1,
      "max": 200,
      "count": 100
    }
  }
}
```

## Apply Formula

```json
{
  "name": "apply_formula",
  "arguments": {
    "path": "/data/report.xlsx",
    "sheet": "Sheet1",
    "cell": "C10",
    "formula": "=SUM(C2:C9)"
  }
}
```

## Convert Spreadsheet

```json
{
  "name": "convert_spreadsheet",
  "arguments": {
    "inputPath": "/data/report.xlsx",
    "outputPath": "/output/report.csv",
    "outputFormat": "csv"
  }
}
```
