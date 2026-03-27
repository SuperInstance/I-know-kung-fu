# Data Quality Agent

## Overview

Monitors, measures, and improves data quality across datasets with automated profiling, validation, and cleansing recommendations.

## Core Capabilities

| Capability | Description |
|------------|-------------|
| Data Profiling | Profile data distributions and patterns |
| Quality Scoring | Calculate data quality scores |
| Anomaly Detection | Find data anomalies and outliers |
| Validation Rules | Apply validation rules |
| Cleansing Recommendations | Recommend data fixes |

## Skills

### Primary Skills
1. **Completeness Check** - Check for missing values
2. **Accuracy Validation** - Validate data accuracy
3. **Consistency Check** - Check data consistency
4. **Timeliness Analysis** - Analyze data freshness
5. **Uniqueness Validation** - Check for duplicates

### Secondary Skills
- Schema validation
- Format validation
- Range checking
- Referential integrity
- Business rule validation

## Use Cases

1. **Data Pipeline Quality** - Monitor pipeline data quality
2. **Database Health** - Maintain database quality
3. **ML Data Prep** - Prepare quality training data
4. **Regulatory Compliance** - Ensure data compliance
5. **Customer Data** - Maintain customer data quality

## Example Quality Report

### Dataset Analysis
```json
{
  "dataset": "customer_records",
  "overall_score": 78,
  "dimensions": {
    "completeness": {
      "score": 85,
      "issues": [
        {"field": "email", "missing": "12%"},
        {"field": "phone", "missing": "8%"}
      ]
    },
    "accuracy": {
      "score": 72,
      "issues": [
        {"field": "email", "invalid_format": "5%"},
        {"field": "zip_code", "invalid": "3%"}
      ]
    },
    "consistency": {
      "score": 90,
      "issues": [
        {"field": "country", "format_variance": "multiple formats detected"}
      ]
    },
    "timeliness": {
      "score": 65,
      "issues": [
        {"field": "last_updated", "stale_over_1yr": "23%"}
      ]
    },
    "uniqueness": {
      "score": 88,
      "issues": [
        {"field": "customer_id", "duplicates": "0.5%"}
      ]
    }
  },
  "recommendations": [
    {"priority": "high", "action": "Implement email validation at entry"},
    {"priority": "high", "action": "Run deduplication on customer_id"},
    {"priority": "medium", "action": "Standardize country codes"},
    {"priority": "low", "action": "Implement update reminders"}
  ]
}
```

## Quality Dimensions

| Dimension | Description | Key Metrics |
|-----------|-------------|-------------|
| Completeness | Missing values | % null, % empty |
| Accuracy | Correct values | % valid, error rate |
| Consistency | Same format/values | % matching patterns |
| Timeliness | Data freshness | Age, update frequency |
| Uniqueness | No duplicates | Duplicate count |
| Validity | Conforms to rules | % passing rules |

## Configuration

```json
{
  "agent_type": "data-quality",
  "profiling_depth": "comprehensive",
  "validation_rules": ["schema", "business", "statistical"],
  "scoring_method": "weighted",
  "dimension_weights": {
    "completeness": 0.25,
    "accuracy": 0.25,
    "consistency": 0.20,
    "timeliness": 0.15,
    "uniqueness": 0.15
  },
  "alert_threshold": 70
}
```

## Performance Characteristics

| Metric | Value |
|--------|-------|
| Processing speed | 1M records/min |
| Accuracy of detection | 95%+ |
| Supported formats | CSV, JSON, SQL, Parquet |

## Monetization

- **Basic**: $0.10/dataset analysis
- **Pro**: $1.00/dataset (with cleansing recommendations)
- **Enterprise**: $500/month unlimited

## Related Agents

- `data-anonymizer/` - Privacy protection
- `data-transformer/` - Data transformation
- `pii-scanner/` - PII detection
