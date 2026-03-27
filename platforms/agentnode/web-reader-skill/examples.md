# Web Reader Skill API Examples

This document provides comprehensive examples for using the Web Reader Skill API.

## Authentication

All API requests require authentication via API key:

```bash
curl -X POST "https://api.agentnode.io/v1/skills/web-reader/extract" \
  -H "X-API-Key: your_api_key_here" \
  -H "Content-Type: application/json"
```

## Content Extraction

### Basic Content Extraction

Extract content from a web page:

```bash
POST /v1/skills/web-reader/extract
```

**Request:**
```json
{
  "url": "https://example.com/article/how-ai-is-transforming-business",
  "options": {
    "output_format": "markdown",
    "include_images": true,
    "include_metadata": true
  }
}
```

**Response:**
```json
{
  "success": true,
  "url": "https://example.com/article/how-ai-is-transforming-business",
  "final_url": "https://example.com/article/how-ai-is-transforming-business",
  "title": "How AI is Transforming Business Operations in 2024",
  "content": "# How AI is Transforming Business Operations in 2024\n\nArtificial intelligence has moved beyond the experimental phase...",
  "author": "Sarah Johnson",
  "published_date": "2024-12-10T09:00:00Z",
  "modified_date": "2024-12-12T14:30:00Z",
  "metadata": {
    "description": "Discover how AI is revolutionizing business operations across industries...",
    "keywords": ["AI", "business", "automation", "digital transformation"],
    "og_title": "How AI is Transforming Business Operations",
    "og_description": "Discover how AI is revolutionizing business operations...",
    "og_image": "https://example.com/images/ai-business.jpg",
    "og_type": "article"
  },
  "images": [
    {
      "url": "https://example.com/images/ai-dashboard.png",
      "alt_text": "AI Dashboard showing analytics",
      "caption": "AI-powered analytics dashboard",
      "width": 1200,
      "height": 630
    }
  ],
  "links": [
    {
      "url": "https://example.com/related/machine-learning",
      "text": "Machine Learning Guide",
      "is_internal": true
    }
  ],
  "language": "en",
  "word_count": 1850,
  "reading_time_minutes": 8,
  "quality_score": 0.94,
  "billing": {
    "operation": "extract",
    "amount_charged": 0.005
  }
}
```

### JavaScript Rendering

Extract content from JavaScript-heavy pages:

```bash
POST /v1/skills/web-reader/extract
```

**Request:**
```json
{
  "url": "https://spa-website.com/products",
  "options": {
    "render_javascript": true,
    "timeout_ms": 20000,
    "output_format": "text"
  }
}
```

**Response:**
```json
{
  "success": true,
  "url": "https://spa-website.com/products",
  "title": "Products - Modern E-commerce",
  "content": "Product Catalog\n\nFeatured Products:\n\n1. Smart Home Hub - $149.99\n2. Wireless Earbuds - $79.99...",
  "javascript_rendered": true,
  "render_time_ms": 3500,
  "billing": {
    "operation": "extract_js",
    "amount_charged": 0.02
  }
}
```

### Extract Structured Data

Extract Schema.org and JSON-LD data:

```bash
POST /v1/skills/web-reader/extract-structured
```

**Request:**
```json
{
  "url": "https://ecommerce-site.com/product/smart-watch-pro",
  "schema_types": ["Product", "Offer", "AggregateRating"]
}
```

**Response:**
```json
{
  "success": true,
  "url": "https://ecommerce-site.com/product/smart-watch-pro",
  "structured_data": [
    {
      "@context": "https://schema.org",
      "@type": "Product",
      "name": "Smart Watch Pro",
      "description": "Advanced smartwatch with health monitoring",
      "image": "https://cdn.example.com/watch-pro.jpg",
      "brand": {
        "@type": "Brand",
        "name": "TechWear"
      },
      "offers": {
        "@type": "Offer",
        "price": "299.99",
        "priceCurrency": "USD",
        "availability": "https://schema.org/InStock",
        "seller": {
          "@type": "Organization",
          "name": "TechStore"
        }
      },
      "aggregateRating": {
        "@type": "AggregateRating",
        "ratingValue": "4.7",
        "reviewCount": "1523"
      }
    }
  ],
  "billing": {
    "operation": "extract_structured",
    "amount_charged": 0.01
  }
}
```

## Batch Extraction

### Process Multiple URLs

Extract content from multiple URLs at once:

```bash
POST /v1/skills/web-reader/extract-batch
```

**Request:**
```json
{
  "urls": [
    "https://news-site.com/article/1",
    "https://news-site.com/article/2",
    "https://news-site.com/article/3",
    "https://news-site.com/article/4",
    "https://news-site.com/article/5"
  ],
  "options": {
    "output_format": "markdown",
    "include_metadata": true
  },
  "webhook_url": "https://your-app.com/webhook/extract-complete"
}
```

**Response:**
```json
{
  "success": true,
  "batch_id": "batch_xyz789",
  "status": "processing",
  "total_urls": 5,
  "webhook_url": "https://your-app.com/webhook/extract-complete",
  "estimated_completion": "2024-12-15T10:35:00Z"
}
```

**Webhook Payload (when complete):**
```json
{
  "batch_id": "batch_xyz789",
  "status": "completed",
  "completed_at": "2024-12-15T10:34:45Z",
  "results": [
    {
      "url": "https://news-site.com/article/1",
      "success": true,
      "title": "Article 1 Title",
      "content": "Content..."
    },
    {
      "url": "https://news-site.com/article/2",
      "success": true,
      "title": "Article 2 Title",
      "content": "Content..."
    }
  ],
  "summary": {
    "total": 5,
    "successful": 5,
    "failed": 0
  }
}
```

## Sitemap Parsing

### Extract URLs from Sitemap

Get all URLs from a website's sitemap:

```bash
POST /v1/skills/web-reader/sitemap
```

**Request:**
```json
{
  "site_url": "https://example.com",
  "max_urls": 500,
  "filter_pattern": "/blog/.*"
}
```

**Response:**
```json
{
  "success": true,
  "site_url": "https://example.com",
  "urls_found": 125,
  "urls": [
    "https://example.com/blog/post-1",
    "https://example.com/blog/post-2",
    "https://example.com/blog/post-3"
  ],
  "sitemaps_parsed": [
    "https://example.com/sitemap.xml",
    "https://example.com/blog-sitemap.xml"
  ],
  "filter_applied": "/blog/.*",
  "billing": {
    "operation": "sitemap",
    "amount_charged": 0.02
  }
}
```

## RSS Feed Parsing

### Parse RSS/Atom Feed

Extract content from RSS feeds:

```bash
POST /v1/skills/web-reader/rss
```

**Request:**
```json
{
  "feed_url": "https://tech-news.com/feed",
  "max_items": 20,
  "include_content": true
}
```

**Response:**
```json
{
  "success": true,
  "feed_title": "Tech News Daily",
  "feed_url": "https://tech-news.com/feed",
  "feed_description": "Latest technology news and updates",
  "last_updated": "2024-12-15T08:00:00Z",
  "items": [
    {
      "title": "New AI Model Breaks Records",
      "link": "https://tech-news.com/ai-model-record",
      "published": "2024-12-15T07:30:00Z",
      "author": "John Smith",
      "categories": ["AI", "Machine Learning"],
      "content": "Full article content here...",
      "description": "Brief summary of the article..."
    },
    {
      "title": "Cloud Computing Trends for 2025",
      "link": "https://tech-news.com/cloud-trends-2025",
      "published": "2024-12-14T15:00:00Z",
      "author": "Jane Doe",
      "categories": ["Cloud", "Enterprise"],
      "content": "Full article content here..."
    }
  ],
  "total_items": 20,
  "billing": {
    "operation": "rss",
    "amount_charged": 0.01
  }
}
```

## Metadata Extraction

### Extract Page Metadata Only

Get metadata without full content:

```bash
POST /v1/skills/web-reader/metadata
```

**Request:**
```json
{
  "url": "https://example.com/landing-page"
}
```

**Response:**
```json
{
  "success": true,
  "url": "https://example.com/landing-page",
  "final_url": "https://example.com/landing-page",
  "title": "Welcome to Example - Transform Your Business",
  "description": "Example helps businesses transform their operations with innovative solutions...",
  "keywords": ["business", "transformation", "innovation"],
  "og_title": "Transform Your Business Today",
  "og_description": "Join thousands of companies using Example",
  "og_image": "https://example.com/og-image.jpg",
  "og_type": "website",
  "twitter_card": "summary_large_image",
  "twitter_site": "@example",
  "canonical_url": "https://example.com/landing-page",
  "favicon": "https://example.com/favicon.ico",
  "robots": "index, follow",
  "language": "en",
  "billing": {
    "operation": "metadata",
    "amount_charged": 0.002
  }
}
```

## Screenshot Capture

### Capture Page Screenshot

Take a screenshot of a web page:

```bash
POST /v1/skills/web-reader/screenshot
```

**Request:**
```json
{
  "url": "https://example.com/dashboard",
  "viewport_width": 1920,
  "viewport_height": 1080,
  "full_page": true,
  "format": "png"
}
```

**Response:**
```json
{
  "success": true,
  "url": "https://example.com/dashboard",
  "screenshot_url": "https://storage.agentnode.io/screenshots/screenshot_abc123.png",
  "width": 1920,
  "height": 4500,
  "format": "png",
  "file_size_kb": 850,
  "billing": {
    "operation": "screenshot",
    "amount_charged": 0.02
  }
}
```

## Error Handling

### Common Error Responses

**URL Not Accessible:**
```json
{
  "success": false,
  "error": {
    "code": "URL_NOT_ACCESSIBLE",
    "message": "The URL is not accessible",
    "details": {
      "url": "https://private-site.com/page",
      "status_code": 403,
      "reason": "Access denied by server"
    }
  }
}
```

**Timeout:**
```json
{
  "success": false,
  "error": {
    "code": "TIMEOUT",
    "message": "Request timed out",
    "details": {
      "url": "https://slow-site.com/page",
      "timeout_ms": 15000,
      "elapsed_ms": 15045
    }
  }
}
```

**Blocked by Website:**
```json
{
  "success": false,
  "error": {
    "code": "BLOCKED",
    "message": "Access blocked by website",
    "details": {
      "url": "https://protected-site.com/page",
      "block_type": "captcha",
      "suggestion": "Try with JavaScript rendering enabled"
    }
  }
}
```

## SDK Examples

### Python SDK

```python
from agentnode import WebReaderSkill

reader = WebReaderSkill(api_key="your_api_key")

# Basic extraction
result = reader.extract(
    url="https://example.com/article",
    options={
        "output_format": "markdown",
        "include_metadata": True
    }
)

print(f"Title: {result['title']}")
print(f"Content: {result['content'][:200]}...")

# Batch extraction
batch = reader.extract_batch(
    urls=["https://site1.com", "https://site2.com"],
    webhook_url="https://your-app.com/webhook"
)

print(f"Batch ID: {batch['batch_id']}")

# RSS feed
feed = reader.parse_rss(
    feed_url="https://news.com/feed",
    max_items=10
)

for item in feed['items']:
    print(f"- {item['title']}")
```

### JavaScript SDK

```javascript
const { WebReaderSkill } = require('@agentnode/skills');

const reader = new WebReaderSkill({ apiKey: 'your_api_key' });

// Extract with JavaScript rendering
const result = await reader.extract({
  url: 'https://spa-site.com/products',
  options: {
    render_javascript: true,
    output_format: 'text'
  }
});

console.log(`Extracted: ${result.content}`);

// Get sitemap
const sitemap = await reader.sitemap({
  site_url: 'https://example.com',
  max_urls: 100
});

console.log(`Found ${sitemap.urls_found} URLs`);

// Parse RSS feed
const feed = await reader.rss({
  feed_url: 'https://blog.com/feed',
  include_content: true
});

console.log(`Feed: ${feed.feed_title}`);
```
