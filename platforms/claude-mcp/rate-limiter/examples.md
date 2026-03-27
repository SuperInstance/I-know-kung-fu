# Rate Limiter - Usage Examples

## Check Rate Limit

```json
{
  "name": "check_rate_limit",
  "arguments": {
    "key": "user:123:api",
    "limit": 100,
    "window": 60
  }
}
```

**Response:**
```json
{
  "allowed": true,
  "remaining": 99,
  "resetAt": "2024-01-15T10:31:00Z",
  "retryAfter": null
}
```

## Create Quota

```json
{
  "name": "create_quota",
  "arguments": {
    "name": "api_tier_pro",
    "limits": [
      { "window": "minute", "maxRequests": 100 },
      { "window": "hour", "maxRequests": 5000 },
      { "window": "day", "maxRequests": 50000 }
    ]
  }
}
```

## Apply Quota

```json
{
  "name": "apply_quota",
  "arguments": {
    "quotaName": "api_tier_pro",
    "key": "user:456"
  }
}
```

## Get Usage

```json
{
  "name": "get_usage",
  "arguments": {
    "key": "user:123:api"
  }
}
```

**Response:**
```json
{
  "key": "user:123:api",
  "current": 45,
  "limit": 100,
  "remaining": 55,
  "percentUsed": 45,
  "resetAt": "2024-01-15T10:31:00Z"
}
```

## Rate Limited Response

```json
{
  "name": "check_rate_limit",
  "arguments": {
    "key": "user:123:api",
    "limit": 10,
    "window": 60
  }
}
```

**Response:**
```json
{
  "allowed": false,
  "remaining": 0,
  "resetAt": "2024-01-15T10:31:00Z",
  "retryAfter": 45
}
```
