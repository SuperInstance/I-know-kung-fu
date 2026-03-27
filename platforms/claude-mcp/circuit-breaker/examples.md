# Circuit Breaker - Usage Examples

## Create Circuit

```json
{
  "name": "create_circuit",
  "arguments": {
    "name": "api_service",
    "config": {
      "failureThreshold": 5,
      "successThreshold": 2,
      "timeout": 30000,
      "resetTimeout": 60000
    }
  }
}
```

**Response:**
```json
{
  "success": true,
  "circuit": {
    "name": "api_service",
    "state": "closed",
    "config": {
      "failureThreshold": 5,
      "successThreshold": 2,
      "timeout": 30000,
      "resetTimeout": 60000
    }
  }
}
```

## Execute Through Circuit

```json
{
  "name": "execute",
  "arguments": {
    "circuitName": "api_service",
    "operation": "fetch_user",
    "params": { "userId": 123 }
  }
}
```

**Response (success):**
```json
{
  "success": true,
  "result": { "id": 123, "name": "John" },
  "circuitState": "closed",
  "latency": 45
}
```

**Response (circuit open):**
```json
{
  "success": false,
  "error": {
    "code": "CIRCUIT_OPEN",
    "message": "Circuit is open - requests are failing fast"
  },
  "fallbackUsed": true,
  "fallbackResult": { "cached": true, "data": {...} }
}
```

## Get Circuit Status

```json
{
  "name": "get_circuit_status",
  "arguments": {
    "name": "api_service"
  }
}
```

**Response:**
```json
{
  "name": "api_service",
  "state": "closed",
  "stats": {
    "totalRequests": 1000,
    "successfulRequests": 985,
    "failedRequests": 15,
    "failureRate": 0.015
  },
  "lastStateChange": "2024-01-15T10:00:00Z"
}
```

## Reset Circuit

```json
{
  "name": "reset_circuit",
  "arguments": {
    "name": "api_service"
  }
}
```

**Response:**
```json
{
  "success": true,
  "previousState": "open",
  "currentState": "closed",
  "resetAt": "2024-01-15T10:30:00Z"
}
```

## Get Metrics

```json
{
  "name": "get_metrics",
  "arguments": {
    "circuitName": "api_service",
    "period": "24h"
  }
}
```

**Response:**
```json
{
  "circuit": "api_service",
  "period": "24h",
  "metrics": {
    "totalRequests": 5000,
    "successRate": 0.985,
    "avgLatency": 45,
    "stateChanges": [
      { "from": "closed", "to": "open", "at": "2024-01-14T15:00:00Z" },
      { "from": "open", "to": "half-open", "at": "2024-01-14T16:00:00Z" },
      { "from": "half-open", "to": "closed", "at": "2024-01-14T16:05:00Z" }
    ]
  }
}
```
