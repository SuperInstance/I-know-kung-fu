# Redirect Tracer Agent

> **Quick Task Agent - URL Analysis**

## Overview
Trace URL redirect chains to see the full path from short URL to destination. Security and debugging utility.

## Capabilities
- Full redirect chain
- HTTP status codes
- Response times
- Header inspection
- Meta refresh detection
- JavaScript redirect detection

## Input
```json
{
  "url": "https://bit.ly/example",
  "follow_max": 10
}
```

## Output
```json
{
  "chain": [
    {"url": "https://bit.ly/example", "status": 301, "time_ms": 50},
    {"url": "https://example.com/page", "status": 200, "time_ms": 120}
  ],
  "final_url": "https://example.com/page",
  "total_redirects": 1,
  "total_time_ms": 170
}
```

## Pricing
- **Free**: 50 traces/day
- **Pro**: $4.99/mo

## Revenue Potential
$200-800/month

---

*Quick Task Agent - URL analysis*
