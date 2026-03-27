# Emotion Detector Agent

## Overview

Detects and responds to user emotions in real-time, enabling empathetic and contextually appropriate AI responses.

## Core Capabilities

| Capability | Description |
|------------|-------------|
| Emotion Detection | Identify user emotional state |
| Sentiment Analysis | Analyze positive/negative sentiment |
| Intensity Measurement | Measure emotion intensity |
| Trend Tracking | Track emotional trends over time |
| Response Adaptation | Adapt responses to emotions |

## Skills

### Primary Skills
1. **Emotion Classification** - Classify emotions (joy, anger, sadness, etc.)
2. **Sentiment Scoring** - Score sentiment intensity
3. **Context Awareness** - Consider conversation context
4. **Empathetic Response** - Generate appropriate responses
5. **Escalation Detection** - Detect need for human intervention

### Secondary Skills
- Sarcasm detection
- Frustration indicators
- Mixed emotion handling
- Cultural emotion norms
- Privacy considerations

## Use Cases

1. **Customer Support** - Detect frustrated customers
2. **Mental Health** - Support emotional wellness
3. **Education** - Adapt to student engagement
4. **Sales** - Read buyer signals
5. **HR** - Employee sentiment monitoring

## Example Detection

### Frustration Detection
```
Input: "I've been trying to do this for an hour and it keeps crashing!"
Analysis:
- Emotion: Frustration (primary), Anger (secondary)
- Intensity: High (0.82)
- Sentiment: Negative (-0.75)
- Duration: Extended (indicated by "an hour")
- Risk: Escalation likely

Response Strategy:
1. Acknowledge frustration
2. Apologize sincerely
3. Provide immediate solution
4. Offer human escalation option

Generated Response:
"I completely understand your frustration - an hour of crashes is unacceptable. I'm escalating this immediately. In the meantime, let me offer a quick workaround..."
```

### Joy Detection
```
Input: "I just got the promotion! This is amazing!"
Analysis:
- Emotion: Joy (primary), Pride (secondary)
- Intensity: High (0.91)
- Sentiment: Positive (0.95)
- Social signal: Celebratory

Response Strategy:
1. Celebrate with user
2. Match excitement level
3. Ask about next steps (optional)

Generated Response:
"Congratulations! 🎉 That's fantastic news! All your hard work paid off. How are you feeling about the new role?"
```

## Emotion Categories

| Category | Sub-emotions | Indicators |
|----------|--------------|------------|
| **Joy** | Happy, Excited, Proud | Exclamation marks, positive words |
| **Sadness** | Disappointed, Grief, Lonely | Downward language, withdrawal |
| **Anger** | Frustrated, Furious, Annoyed | Strong negative words, ALL CAPS |
| **Fear** | Anxious, Worried, Scared | Uncertainty language, questions |
| **Surprise** | Shocked, Amazed, Confused | Unexpected reactions, questions |
| **Disgust** | Revolted, Disappointed | Negative evaluation language |
| **Neutral** | Calm, Professional | Factual, balanced language |

## Configuration

```json
{
  "agent_type": "emotion-detector",
  "model": "fine-tuned-roberta",
  "emotions": ["joy", "sadness", "anger", "fear", "surprise", "disgust", "neutral"],
  "intensity_scale": "0-1",
  "history_window": 5,
  "escalation_threshold": 0.8,
  "response_adaptation": true
}
```

## Performance Characteristics

| Metric | Value |
|--------|-------|
| Detection accuracy | 87% |
| Real-time latency | <50ms |
| Language support | 12 languages |
| False positive rate | <5% |

## Monetization

- **Basic**: $0.01/detection
- **Pro**: $0.03/detection (with response adaptation)
- **Enterprise**: $200/month unlimited

## Related Agents

- `dialogue-manager/` - Conversation flow
- `persona-adaptor/` - Response styling
- `escalation-engine/` - Routing decisions
