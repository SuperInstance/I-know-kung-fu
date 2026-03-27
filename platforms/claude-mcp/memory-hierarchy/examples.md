# Memory Hierarchy - Usage Examples

## Basic Usage

### Example 1: Storing a Memory

**Tool Call:**
```json
{
  "name": "store_memory",
  "arguments": {
    "content": "User prefers dark mode for all applications and finds light mode straining to eyes",
    "type": "preference",
    "importance": 0.8,
    "tags": ["ui", "preference", "dark-mode", "accessibility"]
  }
}
```

**Response:**
```json
{
  "success": true,
  "memory": {
    "id": "mem_abc123",
    "content": "User prefers dark mode for all applications and finds light mode straining to eyes",
    "type": "preference",
    "importance": 0.8,
    "tags": ["ui", "preference", "dark-mode", "accessibility"],
    "tier": 3,
    "createdAt": "2024-01-15T10:30:00Z",
    "embeddingGenerated": true
  },
  "message": "Memory stored in Tier 3 (Working Storage)"
}
```

---

### Example 2: Semantic Search

**Tool Call:**
```json
{
  "name": "search_memories",
  "arguments": {
    "query": "user interface preferences",
    "topK": 5,
    "includeScores": true
  }
}
```

**Response:**
```json
{
  "results": [
    {
      "id": "mem_abc123",
      "content": "User prefers dark mode for all applications...",
      "score": 0.92,
      "tier": 3,
      "type": "preference",
      "tags": ["ui", "preference", "dark-mode"]
    },
    {
      "id": "mem_def456",
      "content": "User prefers font size 16px for better readability",
      "score": 0.85,
      "tier": 3,
      "type": "preference"
    },
    {
      "id": "mem_ghi789",
      "content": "User dislikes animations and prefers reduced motion",
      "score": 0.78,
      "tier": 4,
      "type": "preference"
    }
  ],
  "total": 3,
  "queryTime": 45
}
```

---

### Example 3: Retrieving by ID

**Tool Call:**
```json
{
  "name": "retrieve_memory",
  "arguments": {
    "id": "mem_abc123",
    "includeMetadata": true
  }
}
```

**Response:**
```json
{
  "success": true,
  "memory": {
    "id": "mem_abc123",
    "content": "User prefers dark mode for all applications...",
    "type": "preference",
    "importance": 0.8,
    "tags": ["ui", "preference", "dark-mode", "accessibility"],
    "tier": 3,
    "accessCount": 5,
    "lastAccessed": "2024-01-15T11:00:00Z",
    "createdAt": "2024-01-15T10:30:00Z",
    "metadata": {
      "source": "user_feedback",
      "confidence": 0.95
    }
  }
}
```

---

## Memory Types

### Example 4: Storing Different Types

**Fact:**
```json
{
  "name": "store_memory",
  "arguments": {
    "content": "Company was founded in 2018 by Jane Smith",
    "type": "fact",
    "importance": 0.7,
    "tags": ["company", "history"]
  }
}
```

**Event:**
```json
{
  "name": "store_memory",
  "arguments": {
    "content": "Product launch scheduled for March 15th, 2024",
    "type": "event",
    "importance": 0.9,
    "tags": ["product", "launch", "schedule"],
    "metadata": {
      "date": "2024-03-15",
      "status": "scheduled"
    }
  }
}
```

**Instruction:**
```json
{
  "name": "store_memory",
  "arguments": {
    "content": "Always confirm with user before sending emails on their behalf",
    "type": "instruction",
    "importance": 1.0,
    "tags": ["behavior", "email", "confirmation"]
  }
}
```

---

## Temporal Queries

### Example 5: Time Range Search

**Tool Call:**
```json
{
  "name": "retrieve_memory",
  "arguments": {
    "timeRange": {
      "start": "2024-01-01T00:00:00Z",
      "end": "2024-01-15T23:59:59Z"
    },
    "type": "event",
    "topK": 10
  }
}
```

**Response:**
```json
{
  "results": [
    {
      "id": "mem_event1",
      "content": "Team meeting scheduled for January 5th",
      "createdAt": "2024-01-02T09:00:00Z",
      "type": "event"
    },
    {
      "id": "mem_event2",
      "content": "Product demo on January 10th",
      "createdAt": "2024-01-05T14:30:00Z",
      "type": "event"
    }
  ],
  "total": 2,
  "timeRange": {
    "start": "2024-01-01T00:00:00Z",
    "end": "2024-01-15T23:59:59Z"
  }
}
```

---

## Context Generation

### Example 6: Getting Context for LLM

**Tool Call:**
```json
{
  "name": "get_memory_context",
  "arguments": {
    "query": "What are the user's preferences for UI design?",
    "maxTokens": 2000,
    "strategy": "balanced"
  }
}
```

**Response:**
```json
{
  "context": "## User UI Preferences\n\n- Prefers dark mode for all applications (finds light mode straining)\n- Font size preference: 16px for better readability\n- Dislikes animations, prefers reduced motion\n- High contrast mode enabled for accessibility\n- Preferred color scheme: blue accents on dark background\n\n## Related Notes\n\n- Accessibility is important due to visual sensitivity\n- Works primarily in low-light environments",
  "tokensUsed": 187,
  "memoriesIncluded": 7,
  "strategy": "balanced",
  "sources": [
    {"id": "mem_abc123", "relevance": 0.92},
    {"id": "mem_def456", "relevance": 0.85},
    {"id": "mem_ghi789", "relevance": 0.78}
  ]
}
```

---

## Memory Updates

### Example 7: Updating Memory Content

**Tool Call:**
```json
{
  "name": "update_memory",
  "arguments": {
    "id": "mem_abc123",
    "content": "User prefers dark mode for all applications. Recently tried light mode for 1 week but reverted due to eye strain",
    "importance": 0.9
  }
}
```

**Response:**
```json
{
  "success": true,
  "memory": {
    "id": "mem_abc123",
    "content": "User prefers dark mode for all applications. Recently tried light mode for 1 week but reverted due to eye strain",
    "importance": 0.9,
    "previousImportance": 0.8,
    "updatedAt": "2024-01-15T12:00:00Z",
    "version": 2
  }
}
```

### Example 8: Appending to Memory

**Tool Call:**
```json
{
  "name": "update_memory",
  "arguments": {
    "id": "mem_abc123",
    "content": "\n\nNote: User specifically mentioned VS Code dark theme 'One Dark Pro' as favorite",
    "append": true
  }
}
```

---

## Memory Consolidation

### Example 9: Consolidating Related Memories

**Tool Call:**
```json
{
  "name": "consolidate_memories",
  "arguments": {
    "ids": ["mem_ui1", "mem_ui2", "mem_ui3", "mem_ui4"],
    "strategy": "summarize",
    "keepOriginals": false
  }
}
```

**Response:**
```json
{
  "success": true,
  "consolidatedMemory": {
    "id": "mem_consolidated_1",
    "content": "## UI Preferences Summary\n\n### Visual Settings\n- Dark mode preference (all applications)\n- Font size: 16px\n- Reduced motion enabled\n\n### Color Preferences\n- Blue accents on dark backgrounds\n- High contrast for text\n\n### Accessibility\n- Visual sensitivity considerations\n- Low-light work environment",
    "type": "insight",
    "importance": 0.85,
    "tier": 4,
    "consolidatedFrom": ["mem_ui1", "mem_ui2", "mem_ui3", "mem_ui4"],
    "createdAt": "2024-01-15T14:00:00Z"
  },
  "originalsDeleted": true
}
```

---

## Tier Management

### Example 10: Checking Tier Status

**Tool Call:**
```json
{
  "name": "get_memory_stats",
  "arguments": {
    "includeTierBreakdown": true,
    "includeTypeBreakdown": true
  }
}
```

**Response:**
```json
{
  "totalMemories": 1247,
  "totalSize": "45.2 MB",
  "averageImportance": 0.72,
  "tierBreakdown": {
    "tier0": { "count": 50, "usage": "12%" },
    "tier1": { "count": 200, "usage": "35%" },
    "tier2": { "count": 300, "usage": "60%" },
    "tier3": { "count": 400, "usage": "45%" },
    "tier4": { "count": 250, "usage": "15%" },
    "tier5": { "count": 47, "usage": "5%" }
  },
  "typeBreakdown": {
    "fact": 450,
    "preference": 320,
    "event": 200,
    "conversation": 150,
    "instruction": 80,
    "insight": 47
  },
  "retrievalStats": {
    "hitRate": 0.92,
    "averageLatency": 23
  }
}
```

### Example 11: Manual Promotion

**Tool Call:**
```json
{
  "name": "promote_memory",
  "arguments": {
    "id": "mem_important_1",
    "targetTier": 1
  }
}
```

**Response:**
```json
{
  "success": true,
  "memory": {
    "id": "mem_important_1",
    "previousTier": 3,
    "newTier": 1
  },
  "message": "Memory promoted from Tier 3 to Tier 1 for faster access"
}
```

---

## Forgetting Memories

### Example 12: Soft Delete

**Tool Call:**
```json
{
  "name": "forget_memory",
  "arguments": {
    "id": "mem_outdated_1",
    "soft": true
  }
}
```

**Response:**
```json
{
  "success": true,
  "memory": {
    "id": "mem_outdated_1",
    "status": "deleted",
    "recoverable": true,
    "recoverableUntil": "2024-01-22T10:30:00Z"
  },
  "message": "Memory soft-deleted. Can be recovered within 7 days."
}
```

### Example 13: Hard Delete

**Tool Call:**
```json
{
  "name": "forget_memory",
  "arguments": {
    "id": "mem_sensitive_1",
    "soft": false,
    "cascade": true
  }
}
```

**Response:**
```json
{
  "success": true,
  "deleted": {
    "primary": "mem_sensitive_1",
    "associated": ["mem_assoc1", "mem_assoc2"]
  },
  "recoverable": false,
  "message": "Memory and 2 associated memories permanently deleted"
}
```

---

## Summarization

### Example 14: Creating Memory Summary

**Tool Call:**
```json
{
  "name": "summarize_memories",
  "arguments": {
    "query": "project requirements",
    "tags": ["project-x", "requirements"],
    "maxLength": 300
  }
}
```

**Response:**
```json
{
  "summary": {
    "content": "## Project X Requirements Summary\n\n### Core Features\n- User authentication with SSO\n- Dashboard with real-time analytics\n- Export functionality (PDF, Excel)\n\n### Technical Requirements\n- React frontend with TypeScript\n- Node.js backend\n- PostgreSQL database\n\n### Timeline\n- MVP: Q2 2024\n- Full release: Q4 2024",
    "wordCount": 45,
    "sourceMemories": 8
  },
  "summaryMemory": {
    "id": "mem_summary_1",
    "type": "insight",
    "tier": 4,
    "importance": 0.7
  }
}
```

---

## Advanced Filtering

### Example 15: Complex Search

**Tool Call:**
```json
{
  "name": "search_memories",
  "arguments": {
    "query": "security requirements",
    "filters": {
      "types": ["instruction", "fact"],
      "minImportance": 0.7,
      "timeRange": {
        "start": "2024-01-01T00:00:00Z",
        "end": "2024-01-31T23:59:59Z"
      }
    },
    "topK": 10
  }
}
```

**Response:**
```json
{
  "results": [
    {
      "id": "mem_sec1",
      "content": "All API endpoints must use HTTPS with TLS 1.3",
      "score": 0.94,
      "type": "instruction",
      "importance": 1.0
    },
    {
      "id": "mem_sec2",
      "content": "JWT tokens expire after 1 hour, refresh tokens after 7 days",
      "score": 0.89,
      "type": "fact",
      "importance": 0.9
    }
  ],
  "filtersApplied": {
    "types": ["instruction", "fact"],
    "minImportance": 0.7,
    "timeRange": true
  }
}
```

---

## Memory Associations

### Example 16: Creating Associated Memories

**Tool Call:**
```json
{
  "name": "store_memory",
  "arguments": {
    "content": "User's favorite code editor is VS Code",
    "type": "preference",
    "tags": ["development", "editor"],
    "associations": ["mem_abc123"]
  }
}
```

**Response:**
```json
{
  "success": true,
  "memory": {
    "id": "mem_new_1",
    "content": "User's favorite code editor is VS Code",
    "associations": ["mem_abc123"],
    "associatedMemoryPreview": {
      "mem_abc123": "User prefers dark mode for all applications..."
    }
  }
}
```
