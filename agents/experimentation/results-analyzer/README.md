# Results Analyzer Agent

## Overview

The Results Analyzer agent provides deep analysis of experiment results, generating insights, visualizations, and actionable recommendations.

## Core Concept

Analysis workflow:
1. **Data Collection** - Gather experiment data
2. **Statistical Analysis** - Apply statistical methods
3. **Visualization** - Create charts and graphs
4. **Insight Generation** - Extract key insights
5. **Recommendations** - Suggest actions

## Skills

### Primary Skills
1. **Statistical Analysis** - Apply appropriate tests
2. **Data Visualization** - Create clear visualizations
3. **Trend Detection** - Identify trends and patterns
4. **Anomaly Detection** - Find unusual results
5. **Report Generation** - Create comprehensive reports

### Secondary Skills
- Segmentation analysis
- Cohort analysis
- Funnel analysis
- Correlation analysis
- Predictive insights

## Use Cases

1. **A/B Test Analysis** - Analyze experiment results
2. **Performance Monitoring** - Track key metrics
3. **User Behavior Analysis** - Understand user actions
4. **Business Intelligence** - Generate insights
5. **Research Analysis** - Analyze research data

## Example Analysis Output

### Experiment Results
```json
{
  "experiment": "Homepage CTA Test",
  "duration": "14 days",
  "sample_size": 10000,
  "variants": {
    "control": {"n": 5000, "conversion": 0.12},
    "treatment": {"n": 5000, "conversion": 0.15}
  },
  "analysis": {
    "statistical_test": "two_proportion_z_test",
    "z_score": 3.45,
    "p_value": 0.00056,
    "confidence_interval": {
      "lift": [0.018, 0.042],
      "level": 0.95
    },
    "effect_size": "medium",
    "power": 0.92
  },
  "segments": [
    {
      "segment": "mobile_users",
      "lift": 0.35,
      "significance": true
    },
    {
      "segment": "desktop_users",
      "lift": 0.15,
      "significance": false
    }
  ],
  "recommendation": {
    "action": "implement_treatment",
    "confidence": "high",
    "expected_impact": "+25% conversions",
    "caveats": ["Desktop lift not significant - consider separate test"]
  }
}
```

## Configuration

```json
{
  "agent_type": "results-analyzer",
  "significance_level": 0.05,
  "confidence_level": 0.95,
  "segment_analysis": true,
  "visualization_enabled": true,
  "report_format": "markdown",
  "include_raw_data": false,
  "anomaly_detection": true
}
```

## Analysis Types

### Statistical Tests
- t-test
- Chi-square
- Mann-Whitney U
- ANOVA
- Regression

### Visualization Types
- Conversion funnels
- Time series
- Segment comparisons
- Distribution plots
- Heatmaps

## Performance Characteristics

| Metric | Value |
|--------|-------|
| Analysis time | <30s |
| Report quality | High |
| Insight accuracy | 90%+ |
| Best for | Experiment analysis |

## Monetization Strategy

### Pricing Tiers
- **Basic**: $0.10/analysis
- **Pro**: $0.50/analysis (segmented)
- **Enterprise**: $2.00/analysis (custom visualizations)

### Target Markets
1. Growth teams
2. Product teams
3. Data science teams
4. Marketing teams

## Related Agents

- `ab-tester/` - Run experiments
- `variant-generator/` - Create variants
- `market-analyst/` - Market analysis
