# Web Reader Skill - Web Content Extraction

## Overview

The Web Reader Skill provides specialized web page content extraction capabilities, enabling AI agents to programmatically retrieve, parse, and extract structured content from web pages. This skill is essential for research automation, content aggregation, competitive analysis, and data collection workflows.

## Key Features

### Content Extraction
- **Full Article Extraction**: Extract main article content, removing ads and navigation
- **Structured Data**: Extract titles, authors, publication dates, and metadata
- **Clean Text Output**: Get clean, readable text without HTML markup
- **HTML Preservation**: Option to preserve HTML structure when needed

### Advanced Extraction
- **Smart Content Detection**: Automatically identify main content areas
- **Multi-page Articles**: Handle pagination and multi-page content
- **Paywall Bypass**: Handle sites with soft paywalls (where legally permitted)
- **JavaScript Rendering**: Extract content from JavaScript-heavy pages

### Metadata Extraction
- **Open Graph Tags**: Extract social media metadata
- **Schema.org Data**: Parse structured data markup
- **Meta Tags**: Retrieve all page metadata
- **Author Information**: Identify and extract author details

### Media Handling
- **Image Extraction**: Extract images with alt text and captions
- **Video Detection**: Identify embedded videos
- **Audio Extraction**: Find audio content and podcasts
- **Document Links**: Find linked documents (PDF, DOC)

## Use Cases

### Research & Analysis
- **Academic Research**: Extract papers, articles, and citations
- **Market Research**: Collect competitor content and pricing
- **News Monitoring**: Aggregate news from multiple sources
- **Trend Analysis**: Track content trends across websites

### Content Operations
- **Content Aggregation**: Build content feeds and directories
- **SEO Analysis**: Extract and analyze page content for SEO
- **Archive Creation**: Create archives of web content
- **Translation Pipelines**: Extract content for translation workflows

### Business Intelligence
- **Competitive Intelligence**: Monitor competitor websites
- **Price Monitoring**: Extract pricing information
- **Review Collection**: Aggregate reviews from multiple sources
- **Job Posting Aggregation**: Collect job listings

### Data Enrichment
- **Lead Enrichment**: Extract company information from websites
- **Contact Extraction**: Find contact information on pages
- **Social Profiles**: Extract social media links
- **API Discovery**: Find and document API endpoints

## Technical Specifications

### Supported Content Types
- HTML/XHTML pages
- JavaScript-rendered content (SPA support)
- RSS/Atom feeds
- Sitemaps
- JSON-LD structured data

### Extraction Capabilities
- Maximum page size: 50 MB
- JavaScript rendering timeout: 30 seconds
- Concurrent requests: 100
- Rate limiting: Configurable per domain

### Output Formats
- Plain text
- Markdown
- JSON (structured)
- HTML (cleaned)
- CSV (tabular data)

### Anti-Blocking Features
- Rotating user agents
- Proxy support
- Request throttling
- Cookie handling
- CAPTCHA detection notification

## Integration Capabilities

### Native Integrations
- Direct URL input
- Bulk URL processing
- Webhook callbacks
- Queue-based processing

### Output Integrations
- Cloud storage (S3, GCS, Azure)
- Webhook delivery
- Real-time streaming
- Database direct write

## Security and Compliance

- **Robots.txt Compliance**: Automatic robots.txt checking
- **Rate Limiting**: Respect server resources
- **Terms of Service**: Configurable ToS checking
- **Data Privacy**: GDPR-compliant data handling
- **IP Rotation**: Distributed extraction infrastructure

## Content Quality Features

- **Readability Scoring**: Quality score for extracted content
- **Language Detection**: Automatic language identification
- **Spam Detection**: Filter low-quality content
- **Duplicate Detection**: Identify duplicate content
- **Content Validation**: Verify extraction completeness

## Getting Started

1. **Install the Skill**: Add the Web Reader skill to your AgentNode workspace
2. **Configure Authentication**: Set up your API credentials
3. **Provide URLs**: Submit URLs for content extraction
4. **Receive Extracted Content**: Get clean, structured content

## Pricing

See [monetization.md](./monetization.md) for detailed pricing information.

## Examples

See [examples.md](./examples.md) for API usage examples and code snippets.

## Support

- Documentation: [docs.agentnode.io/skills/web-reader](https://docs.agentnode.io/skills/web-reader)
- Community: [community.agentnode.io](https://community.agentnode.io)
- Enterprise Support: enterprise@agentnode.io
