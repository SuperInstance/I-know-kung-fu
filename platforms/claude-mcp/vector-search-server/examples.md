# Vector Search Server - Usage Examples

## Create Index

```json
{
  "name": "create_index",
  "arguments": {
    "name": "documents",
    "dimension": 1536,
    "metric": "cosine",
    "indexType": "hnsw"
  }
}
```

**Response:**
```json
{
  "success": true,
  "index": {
    "name": "documents",
    "dimension": 1536,
    "metric": "cosine",
    "indexType": "hnsw",
    "vectorsCount": 0
  }
}
```

## Add Vectors

```json
{
  "name": "add_vectors",
  "arguments": {
    "index": "documents",
    "documents": [
      { "id": "doc1", "text": "Machine learning is transforming industries", "metadata": { "category": "tech" } },
      { "id": "doc2", "text": "Natural language processing enables chatbots", "metadata": { "category": "tech" } }
    ]
  }
}
```

**Response:**
```json
{
  "success": true,
  "added": 2,
  "indexSize": 2,
  "embeddingTime": 45
}
```

## Search

```json
{
  "name": "search",
  "arguments": {
    "index": "documents",
    "query": "AI technology applications",
    "topK": 5
  }
}
```

**Response:**
```json
{
  "results": [
    {
      "id": "doc1",
      "text": "Machine learning is transforming industries",
      "score": 0.89,
      "metadata": { "category": "tech" }
    },
    {
      "id": "doc2",
      "text": "Natural language processing enables chatbots",
      "score": 0.85,
      "metadata": { "category": "tech" }
    }
  ],
  "queryTime": 5
}
```

## Hybrid Search

```json
{
  "name": "hybrid_search",
  "arguments": {
    "index": "documents",
    "query": "machine learning chatbots",
    "topK": 10,
    "vectorWeight": 0.7,
    "keywordWeight": 0.3
  }
}
```

## Batch Search

```json
{
  "name": "batch_search",
  "arguments": {
    "index": "documents",
    "queries": ["AI technology", "programming languages", "data science"],
    "topK": 5
  }
}
```

## Get Stats

```json
{
  "name": "get_index_stats",
  "arguments": {
    "name": "documents"
  }
}
```

**Response:**
```json
{
  "name": "documents",
  "vectors": 10000,
  "dimension": 1536,
  "indexSizeMB": 45.2,
  "avgSearchTime": 4.5
}
```
