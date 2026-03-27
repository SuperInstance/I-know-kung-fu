# Timestamp Converter

> **Quick Task Agent - Instant Results**

## Overview
Convert between timestamp formats instantly. Unix, ISO, natural language, timezone conversions.

## Capabilities
- Unix timestamp to human-readable
- Human-readable to Unix
- ISO 8601 parsing
- Timezone conversions (all timezones)
- Relative time ("2 hours ago")
- Business hours calculations
- Date arithmetic
- Cron expression parsing

## Input
```json
{
  "value": "1709251200 or '2024-03-01' or '2 hours ago'",
  "from_format": "unix|iso|natural|relative",
  "to_format": "unix|iso|natural|relative",
  "timezone": "UTC|America/New_York|...",
  "operation": "convert|add|subtract|diff"
}
```

## Output
```json
{
  "result": "2024-03-01T00:00:00Z",
  "unix": 1709251200,
  "human": "March 1, 2024 12:00 AM UTC",
  "relative": "2 months ago"
}
```

## Pricing
- **Free**: 100 conversions/day
- **Pro**: Unlimited ($2.99/mo)

## Revenue Potential
$100-400/month

---

*Quick Task Agent - 10 second average usage*
