# Broken Link Checker

> **Quick Task Agent - SEO Quality**

## Overview
Scan websites for broken links (404s). Essential for SEO and user experience.

## Capabilities
- Single page scan
- Full site crawl
- Internal/external link distinction
- Redirect tracking
- Response time measurement
- Export to CSV

## Input
```json
{
  "url": "https://example.com",
  "depth": 2,
  "check_external": true
}
```

## Output
```json
{
  "total_links": 150,
  "broken": [
    {"url": "https://example.com/old-page", "status": 404}
  ],
  "redirects": [
    {"from": "/old", "to": "/new", "code": 301}
  ]
}
```

## Pricing
- **Free**: 50 links/month
- **Pro**: $9.99/mo

## Revenue Potential
$400-1,500/month

---

*Quick Task Agent - SEO quality*
