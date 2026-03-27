# Tool Guardian - Usage Examples

## Basic Usage

### Example 1: Registering a Simple Tool

**Tool Call:**
```json
{
  "name": "register_tool",
  "arguments": {
    "name": "weather_api",
    "description": "Get current weather for a location",
    "inputSchema": {
      "type": "object",
      "properties": {
        "location": {
          "type": "string",
          "description": "City name or coordinates"
        },
        "units": {
          "type": "string",
          "enum": ["celsius", "fahrenheit"],
          "default": "celsius"
        }
      },
      "required": ["location"]
    },
    "endpoint": "https://api.weather.com/v1/current",
    "method": "GET",
    "retry": {
      "maxAttempts": 3,
      "backoff": "exponential",
      "baseDelay": 1000
    }
  }
}
```

**Response:**
```json
{
  "success": true,
  "tool": {
    "name": "weather_api",
    "registered": true,
    "schemaValidated": true
  },
  "message": "Tool 'weather_api' registered successfully"
}
```

---

### Example 2: Executing a Tool

**Tool Call:**
```json
{
  "name": "execute_tool",
  "arguments": {
    "name": "weather_api",
    "parameters": {
      "location": "San Francisco"
    }
  }
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "location": "San Francisco",
    "temperature": 18,
    "units": "celsius",
    "conditions": "Partly cloudy",
    "humidity": 72
  },
  "execution": {
    "attempts": 1,
    "latency": 234,
    "validated": true,
    "coerced": {
      "units": "celsius"
    }
  }
}
```

---

### Example 3: Validation with Type Coercion

**Tool Call:**
```json
{
  "name": "execute_tool",
  "arguments": {
    "name": "weather_api",
    "parameters": {
      "location": "Tokyo",
      "units": "CELSIUS"
    }
  }
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "location": "Tokyo",
    "temperature": 25,
    "units": "celsius",
    "conditions": "Sunny"
  },
  "execution": {
    "attempts": 1,
    "latency": 189,
    "validated": true,
    "coerced": {
      "units": "celsius"
    },
    "coercionDetails": {
      "units": {
        "from": "CELSIUS",
        "to": "celsius",
        "reason": "Enum case mismatch"
      }
    }
  }
}
```

---

## Retry Examples

### Example 4: Automatic Retry on Failure

**Tool Call:**
```json
{
  "name": "execute_tool",
  "arguments": {
    "name": "unreliable_api",
    "parameters": {
      "query": "test"
    }
  }
}
```

**Response (with retries):**
```json
{
  "success": true,
  "data": {
    "result": "success"
  },
  "execution": {
    "attempts": 3,
    "latency": 3456,
    "validated": true,
    "retryDetails": {
      "attempt1": {
        "status": "failed",
        "error": "ECONNRESET",
        "delay": 1000
      },
      "attempt2": {
        "status": "failed",
        "error": 503,
        "delay": 2000
      },
      "attempt3": {
        "status": "success",
        "latency": 456
      }
    }
  }
}
```

---

### Example 5: Retry Exhausted

**Tool Call:**
```json
{
  "name": "execute_tool",
  "arguments": {
    "name": "failing_api",
    "parameters": {
      "id": "test"
    }
  }
}
```

**Response:**
```json
{
  "success": false,
  "error": {
    "code": "RETRY_EXHAUSTED",
    "message": "All retry attempts failed",
    "attempts": 3,
    "lastError": {
      "status": 503,
      "message": "Service Unavailable"
    },
    "retryHistory": [
      {"attempt": 1, "error": "503", "delay": 1000},
      {"attempt": 2, "error": "503", "delay": 2000},
      {"attempt": 3, "error": "503", "delay": 4000}
    ]
  },
  "deadLetterQueue": {
    "queued": true,
    "id": "dlq_abc123",
    "scheduledRetry": "2024-01-15T12:00:00Z"
  }
}
```

---

## Circuit Breaker Examples

### Example 6: Circuit Breaker Opening

**Tool Call:**
```json
{
  "name": "execute_tool",
  "arguments": {
    "name": "flaky_service",
    "parameters": {}
  }
}
```

**Response (circuit opens):**
```json
{
  "success": false,
  "error": {
    "code": "CIRCUIT_OPEN",
    "message": "Circuit breaker is open due to consecutive failures",
    "circuitBreaker": {
      "state": "open",
      "failureCount": 5,
      "lastFailure": "2024-01-15T10:30:00Z",
      "resetScheduled": "2024-01-15T10:31:00Z"
    }
  },
  "fallback": {
    "available": true,
    "message": "Using cached response"
  }
}
```

---

### Example 7: Resetting Circuit Breaker

**Tool Call:**
```json
{
  "name": "reset_circuit_breaker",
  "arguments": {
    "toolName": "flaky_service",
    "force": false
  }
}
```

**Response:**
```json
{
  "success": true,
  "circuitBreaker": {
    "toolName": "flaky_service",
    "previousState": "open",
    "currentState": "closed",
    "resetAt": "2024-01-15T10:35:00Z"
  },
  "message": "Circuit breaker reset successfully"
}
```

---

## Validation Examples

### Example 8: Pre-Validation

**Tool Call:**
```json
{
  "name": "validate_parameters",
  "arguments": {
    "toolName": "user_api",
    "parameters": {
      "email": "user@example.com",
      "age": "25"
    },
    "coerce": true
  }
}
```

**Response:**
```json
{
  "valid": true,
  "original": {
    "email": "user@example.com",
    "age": "25"
  },
  "coerced": {
    "email": "user@example.com",
    "age": 25
  },
  "coercions": [
    {
      "field": "age",
      "from": "string",
      "to": "integer",
      "reason": "Type mismatch - string to integer"
    }
  ]
}
```

---

### Example 9: Validation Failure

**Tool Call:**
```json
{
  "name": "validate_parameters",
  "arguments": {
    "toolName": "payment_api",
    "parameters": {
      "amount": -50,
      "currency": "bitcoin"
    }
  }
}
```

**Response:**
```json
{
  "valid": false,
  "errors": [
    {
      "field": "amount",
      "error": "must be greater than 0",
      "value": -50,
      "suggestion": "Amount must be a positive number"
    },
    {
      "field": "currency",
      "error": "must be equal to one of the allowed values",
      "allowedValues": ["USD", "EUR", "GBP"],
      "value": "bitcoin",
      "suggestion": "Use one of: USD, EUR, GBP"
    }
  ]
}
```

---

## Rate Limiting Examples

### Example 10: Rate Limit Hit

**Tool Call:**
```json
{
  "name": "execute_tool",
  "arguments": {
    "name": "rate_limited_api",
    "parameters": {
      "query": "data"
    }
  }
}
```

**Response:**
```json
{
  "success": true,
  "data": {...},
  "execution": {
    "attempts": 1,
    "latency": 450,
    "rateLimited": true,
    "rateLimit": {
      "limit": 100,
      "remaining": 0,
      "resetAt": "2024-01-15T11:00:00Z",
      "waitTime": 234
    }
  }
}
```

---

## Statistics Examples

### Example 11: Tool Status

**Tool Call:**
```json
{
  "name": "get_tool_status",
  "arguments": {
    "name": "weather_api",
    "includeMetrics": true
  }
}
```

**Response:**
```json
{
  "tool": {
    "name": "weather_api",
    "status": "healthy",
    "registered": true
  },
  "circuitBreaker": {
    "state": "closed",
    "failureCount": 0,
    "successCount": 150
  },
  "rateLimit": {
    "currentUsage": 45,
    "limit": 100,
    "resetIn": 1800
  },
  "metrics": {
    "totalExecutions": 1250,
    "successfulExecutions": 1230,
    "failedExecutions": 20,
    "successRate": 0.984,
    "averageLatency": 234,
    "p95Latency": 567,
    "totalRetries": 35,
    "retrySuccessRate": 0.857
  }
}
```

---

### Example 12: Retry Statistics

**Tool Call:**
```json
{
  "name": "get_retry_stats",
  "arguments": {
    "period": "7d"
  }
}
```

**Response:**
```json
{
  "period": "7d",
  "summary": {
    "totalRetries": 1523,
    "successfulRetries": 1342,
    "retrySuccessRate": 0.881,
    "avgRetriesPerExecution": 0.12
  },
  "byErrorType": [
    {
      "error": "ECONNRESET",
      "count": 456,
      "retrySuccessRate": 0.95
    },
    {
      "error": 503,
      "count": 321,
      "retrySuccessRate": 0.82
    },
    {
      "error": 429,
      "count": 234,
      "retrySuccessRate": 0.91
    }
  ],
  "byTool": [
    {
      "tool": "weather_api",
      "retries": 234,
      "successRate": 0.92
    },
    {
      "tool": "payment_api",
      "retries": 156,
      "successRate": 0.88
    }
  ]
}
```

---

## List Tools Example

### Example 13: List All Registered Tools

**Tool Call:**
```json
{
  "name": "list_tools",
  "arguments": {
    "includeSchemas": false
  }
}
```

**Response:**
```json
{
  "tools": [
    {
      "name": "weather_api",
      "description": "Get current weather for a location",
      "status": "healthy",
      "circuitBreakerState": "closed",
      "endpoint": "https://api.weather.com/v1/current"
    },
    {
      "name": "payment_api",
      "description": "Process payment transactions",
      "status": "healthy",
      "circuitBreakerState": "closed",
      "endpoint": "https://api.payments.com/v2/process"
    },
    {
      "name": "user_api",
      "description": "User management operations",
      "status": "degraded",
      "circuitBreakerState": "half-open",
      "endpoint": "https://api.users.com/v1"
    }
  ],
  "total": 3,
  "healthy": 2,
  "degraded": 1
}
```

---

## Authentication Examples

### Example 14: Tool with API Key

**Tool Call:**
```json
{
  "name": "register_tool",
  "arguments": {
    "name": "secure_api",
    "description": "Secure API with authentication",
    "inputSchema": {
      "type": "object",
      "properties": {
        "data": { "type": "string" }
      }
    },
    "endpoint": "https://api.secure.com/data",
    "authentication": {
      "type": "api_key",
      "header": "X-API-Key",
      "key": "your-secret-key"
    }
  }
}
```

**Response:**
```json
{
  "success": true,
  "tool": {
    "name": "secure_api",
    "registered": true,
    "authenticationType": "api_key",
    "keyPreview": "you****key"
  }
}
```

---

## Timeout Example

### Example 15: Handling Timeouts

**Tool Call:**
```json
{
  "name": "execute_tool",
  "arguments": {
    "name": "slow_api",
    "parameters": {},
    "options": {
      "timeout": 5000
    }
  }
}
```

**Response:**
```json
{
  "success": false,
  "error": {
    "code": "TIMEOUT_EXCEEDED",
    "message": "Request timed out after 5000ms",
    "timeout": 5000,
    "elapsed": 5002
  },
  "retry": {
    "suggested": true,
    "suggestedTimeout": 10000
  }
}
```

---

## Configuration Examples

### Example 16: Update Retry Configuration

**Tool Call:**
```json
{
  "name": "configure_retry",
  "arguments": {
    "toolName": "unreliable_api",
    "config": {
      "maxAttempts": 5,
      "backoff": "exponential",
      "baseDelay": 500,
      "maxDelay": 60000,
      "jitter": true
    }
  }
}
```

**Response:**
```json
{
  "success": true,
  "tool": "unreliable_api",
  "previousConfig": {
    "maxAttempts": 3,
    "backoff": "exponential",
    "baseDelay": 1000
  },
  "newConfig": {
    "maxAttempts": 5,
    "backoff": "exponential",
    "baseDelay": 500,
    "maxDelay": 60000,
    "jitter": true
  },
  "message": "Retry configuration updated successfully"
}
```

---

### Example 17: Update Rate Limit Configuration

**Tool Call:**
```json
{
  "name": "configure_rate_limit",
  "arguments": {
    "toolName": "rate_limited_api",
    "config": {
      "requestsPerSecond": 10,
      "burstSize": 20
    }
  }
}
```

**Response:**
```json
{
  "success": true,
  "tool": "rate_limited_api",
  "rateLimitConfig": {
    "requestsPerSecond": 10,
    "burstSize": 20
  },
  "message": "Rate limit configuration updated"
}
```
