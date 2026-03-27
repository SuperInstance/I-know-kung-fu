# Dialogue Manager Agent

## Overview

Manages multi-turn conversations with context tracking, topic management, and coherent dialogue flow.

## Core Capabilities

| Capability | Description |
|------------|-------------|
| Context Tracking | Maintain conversation context |
| Topic Management | Handle topic changes gracefully |
| Intent Recognition | Identify user intent |
| Response Coherence | Ensure coherent responses |
| Conversation Repair | Recover from misunderstandings |

## Skills

### Primary Skills
1. **Context Maintenance** - Track conversation state
2. **Intent Detection** - Understand user goals
3. **Topic Tracking** - Follow topic changes
4. **Coreference Resolution** - Resolve pronouns/references
5. **Conversation Summarization** - Summarize long conversations

### Secondary Skills
- Small talk handling
- Graceful degradation
- Mixed-initiative dialogue
- Clarification requests
- Confirmation strategies

## Use Cases

1. **Customer Service** - Handle support conversations
2. **Virtual Assistants** - Personal assistant interactions
3. **Information Gathering** - Collect structured information
4. **Interview Systems** - Conduct structured interviews
5. **Chatbots** - General conversational AI

## Example Interactions

### Multi-Turn Conversation
```
Turn 1:
User: "I want to book a flight to Paris"
Agent: [Creates booking intent, asks for dates]
"Great! When would you like to travel to Paris?"

Turn 2:
User: "Sometime next month"
Agent: [Updates context with flexible dates]
"I found several options in April. Do you have specific dates in mind, or should I show you the best deals?"

Turn 3:
User: "What about hotels?"
Agent: [Detects topic shift, maintains context]
"I can help with hotels in Paris too. Should I search for hotels for your April trip, or separately?"

Turn 4:
User: "Yes, for the trip"
Agent: [Resolves coreference, links hotel to flight]
"Perfect. I'll search for hotels in Paris for April. How many nights will you be staying?"
```

### Conversation Repair
```
User: "No, I meant New York not Paris"
Agent: [Detects correction, updates context]
"I apologize for the confusion. Let me update your flight search to New York instead. Same timeframe - April?"
```

## Configuration

```json
{
  "agent_type": "dialogue-manager",
  "max_context_turns": 20,
  "topic_memory": true,
  "clarification_threshold": 0.7,
  "summary_trigger": 10,
  "repair_strategies": ["clarify", "confirm", "rephrase"],
  "smalltalk_enabled": true
}
```

## Performance Characteristics

| Metric | Value |
|--------|-------|
| Context retention | 20+ turns |
| Intent accuracy | 95%+ |
| Topic tracking | 90%+ |
| Repair success | 85%+ |

## Monetization

- **Basic**: $0.01/conversation turn
- **Pro**: $0.05/conversation (full context management)
- **Enterprise**: $500+/month unlimited

## Related Agents

- `persona-adaptor/` - Personality adjustment
- `emotion-detector/` - Emotional awareness
- `customer-support-suite/` - Full support solution
