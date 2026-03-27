# Token Vault - Usage Examples

## Store Secret

```json
{
  "name": "store_secret",
  "arguments": {
    "name": "openai_api_key",
    "value": "sk-your-api-key-here",
    "type": "api_key",
    "environment": "production",
    "rotationDays": 90
  }
}
```

**Response:**
```json
{
  "success": true,
  "name": "openai_api_key",
  "type": "api_key",
  "environment": "production",
  "storedAt": "2024-01-15T10:30:00Z",
  "nextRotation": "2024-04-15T10:30:00Z"
}
```

## Get Secret

```json
{
  "name": "get_secret",
  "arguments": {
    "name": "openai_api_key",
    "environment": "production",
    "reason": "API call for user request"
  }
}
```

**Response:**
```json
{
  "name": "openai_api_key",
  "value": "sk-your-api-key-here",
  "type": "api_key",
  "accessedAt": "2024-01-15T10:35:00Z"
}
```

## List Secrets

```json
{
  "name": "list_secrets",
  "arguments": {
    "environment": "production"
  }
}
```

**Response:**
```json
{
  "secrets": [
    { "name": "openai_api_key", "type": "api_key", "lastAccessed": "2024-01-15T10:35:00Z" },
    { "name": "database_password", "type": "password", "lastAccessed": "2024-01-14T08:00:00Z" }
  ],
  "total": 2
}
```

## Rotate Secret

```json
{
  "name": "rotate_secret",
  "arguments": {
    "name": "openai_api_key",
    "newValue": "sk-new-api-key",
    "keepHistory": true
  }
}
```

## Get Audit Log

```json
{
  "name": "get_audit_log",
  "arguments": {
    "secretName": "openai_api_key",
    "startDate": "2024-01-01",
    "endDate": "2024-01-15"
  }
}
```

**Response:**
```json
{
  "logs": [
    { "action": "get", "reason": "API call", "timestamp": "2024-01-15T10:35:00Z", "ip": "192.168.1.1" },
    { "action": "rotate", "reason": "Scheduled rotation", "timestamp": "2024-01-10T00:00:00Z" }
  ]
}
```

## Generate Token

```json
{
  "name": "generate_token",
  "arguments": {
    "type": "api_key",
    "length": 32
  }
}
```

**Response:**
```json
{
  "token": "sk_live_abc123def456ghi789jkl012mno345pq",
  "type": "api_key",
  "length": 32
}
```
