# Cache Layer - Usage Examples

## Get Cached Value

```json
{
  "name": "get",
  "arguments": {
    "key": "user:123:profile"
  }
}
```

**Response:**
```json
{
  "found": true,
  "value": "{\"name\":\"John\",\"email\":\"john@example.com\"}",
  "tier": "L2",
  "age": 45,
  "remainingTTL": 255
}
```

## Set Cached Value

```json
{
  "name": "set",
  "arguments": {
    "key": "llm:response:abc123",
    "value": "The capital of France is Paris.",
    "ttl": 3600,
    "tags": ["llm", "geography"]
  }
}
```

## Semantic Matching

```json
{
  "name": "get",
  "arguments": {
    "key": "What is the capital city of France?",
    "semanticMatch": true,
    "similarityThreshold": 0.9
  }
}
```

**Response:**
```json
{
  "found": true,
  "value": "The capital of France is Paris.",
  "matchedKey": "llm:response:abc123",
  "similarity": 0.94,
  "note": "Semantically matched to similar cached query"
}
```

## Invalidate by Tag

```json
{
  "name": "invalidate_by_tag",
  "arguments": {
    "tag": "user:123"
  }
}
```

**Response:**
```json
{
  "success": true,
  "invalidated": 15,
  "keys": ["user:123:profile", "user:123:settings", "..."]
}
```

## Get Statistics

```json
{
  "name": "get_stats",
  "arguments": {}
}
```

**Response:**
```json
{
  "overall": {
    "hitRate": 0.65,
    "totalHits": 15000,
    "totalMisses": 8000
  },
  "byTier": {
    "L1": { "entries": 500, "hitRate": 0.8, "avgLatency": 0.5 },
    "L2": { "entries": 5000, "hitRate": 0.6, "avgLatency": 2.5 },
    "L3": { "entries": 20000, "hitRate": 0.4, "avgLatency": 15 }
  }
}
```
