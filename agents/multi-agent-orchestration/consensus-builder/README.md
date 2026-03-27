# Consensus Builder Agent

## Overview

The Consensus Builder specializes in finding agreement among multiple agents or perspectives. It identifies common ground, resolves conflicts, and produces unified outputs that represent collective intelligence.

## Core Concept

Consensus building process:
1. **Gather Perspectives** - Collect all viewpoints
2. **Identify Overlap** - Find common elements
3. **Resolve Conflicts** - Address disagreements
4. **Build Agreement** - Create unified position
5. **Validate Consensus** - Ensure all parties satisfied

## Skills

### Primary Skills
1. **Agreement Detection** - Find shared positions
2. **Conflict Resolution** - Mediate disagreements
3. **Compromise Generation** - Create middle-ground solutions
4. **Priority Alignment** - Align on what matters most
5. **Commitment Securing** - Get buy-in from participants

### Secondary Skills
- Stakeholder analysis
- Trade-off identification
- Negotiation tactics
- Facilitation techniques
- Documentation

## Use Cases

1. **Team Decisions** - Align team on direction
2. **Requirement Gathering** - Unify stakeholder needs
3. **Document Review** - Agree on final content
4. **Architecture Decisions** - Consensus on design
5. **Policy Creation** - Build agreed-upon policies

## Example Consensus Sessions

### Feature Priority Consensus
```json
{
  "consensus_session": {
    "topic": "Q2 Feature Priorities",
    "participants": [
      {"role": "Product", "priorities": ["Analytics", "Export", "API"]},
      {"role": "Engineering", "priorities": ["Performance", "API", "Testing"]},
      {"role": "Sales", "priorities": ["Analytics", "Integrations", "Export"]},
      {"role": "Support", "priorities": ["Documentation", "Testing", "API"]}
    ],
    "analysis": {
      "unanimous": ["API"],
      "majority": ["Analytics", "Export", "Testing"],
      "minority": ["Performance", "Integrations", "Documentation"]
    },
    "consensus": {
      "rank_1": "API (unanimous support)",
      "rank_2": "Analytics (3/4 support, high business value)",
      "rank_3": "Testing (2/4 support, enables other work)",
      "rank_4": "Export (2/4 support, customer requests)",
      "deferred": ["Performance", "Integrations", "Documentation"]
    },
    "rationale": "Prioritized based on unanimous agreement first, then business impact"
  }
}
```

### Architecture Decision Record
```json
{
  "adr_consensus": {
    "decision": "Use PostgreSQL for primary database",
    "stakeholders": {
      "backend_lead": "Support - Familiarity, reliability",
      "devops": "Support - Easy to manage, good tooling",
      "security": "Support - Mature security features",
      "data_team": "Neutral - Would prefer columnar for analytics"
    },
    "concerns_addressed": [
      "Analytics needs: Add read replica for analytics queries",
      "Scaling: Start with PostgreSQL, migrate if needed"
    ],
    "consensus_level": "Full agreement with accommodations",
    "commitments": [
      "Backend: Own schema design",
      "DevOps: Set up replication",
      "Data: Access to read replica"
    ]
  }
}
```

## Configuration

```json
{
  "agent_type": "consensus-builder",
  "consensus_threshold": 0.7,
  "max_rounds": 5,
  "require_unanimous": false,
  "document_concerns": true,
  "facilitation_style": "collaborative",
  "conflict_resolution": "compromise",
  "output_format": "decision_record"
}
```

## Performance Characteristics

| Metric | Value |
|--------|-------|
| Consensus rate | 85% |
| Time to agreement | 3-5 rounds |
| Satisfaction score | 4.2/5 |
| Best for | Team decisions |
| Conflict resolution | 78% success |

## Consensus Strategies

### Unanimous Consensus
All participants must agree. Best for critical decisions.

### Majority Consensus
More than 50% agreement required. Faster decisions.

### Supermajority Consensus
67% or 75% agreement. Balances speed and buy-in.

### Weighted Consensus
Stakeholders have different voting weights based on expertise.

### Delphi Method
Iterative anonymous voting to reduce groupthink.

## Integration Points

- **AutoGen**: Multi-agent decision making
- **CrewAI**: Team-based workflows
- **Organizations**: Meeting facilitation

## Monetization Strategy

### Pricing Tiers
- **Basic**: $0.10/consensus (up to 5 participants)
- **Pro**: $0.30/consensus (up to 20 participants, detailed report)
- **Enterprise**: $1.00/consensus (unlimited, ADR integration)

### Target Markets
1. Product teams
2. Architecture teams
3. Executive teams
4. Cross-functional initiatives

## Technical Implementation

```python
class ConsensusBuilder:
    def __init__(self, threshold=0.7, max_rounds=5):
        self.threshold = threshold
        self.max_rounds = max_rounds
        self.positions = []
        self.concerns = []

    def gather_positions(self, participants, topic):
        self.positions = [
            participant.get_position(topic)
            for participant in participants
        ]
        return self.positions

    def find_overlap(self):
        # Find common elements across all positions
        common = set(self.positions[0].key_points)
        for position in self.positions[1:]:
            common &= set(position.key_points)
        return common

    def resolve_conflicts(self, conflicts):
        resolutions = []
        for conflict in conflicts:
            resolution = self.generate_compromise(conflict)
            resolutions.append(resolution)
        return resolutions

    def build_consensus(self, topic, participants):
        self.gather_positions(participants, topic)

        for round_num in range(self.max_rounds):
            overlap = self.find_overlap()
            conflicts = self.identify_conflicts()

            if self.consensus_level() >= self.threshold:
                return self.create_consensus_document()

            # Address concerns
            for concern in self.collect_concerns():
                self.address_concern(concern)

        return self.create_partial_consensus()

    def consensus_level(self):
        # Calculate agreement percentage
        total_points = sum(len(p.key_points) for p in self.positions)
        agreed_points = len(self.find_overlap())
        return agreed_points / max(total_points, 1)
```

## Consensus Document Template

```markdown
# Consensus Decision Record

## Topic
[Decision being made]

## Participants
- [Name] (Role): Position summary
- [Name] (Role): Position summary

## Areas of Agreement
1. [Agreed point 1]
2. [Agreed point 2]

## Resolved Concerns
| Concern | Resolution |
|---------|------------|
| [Issue] | [How it was addressed] |

## Unresolved Items
- [Items tabled for future discussion]

## Final Consensus
[Unified position agreed upon]

## Commitments
- [Name]: [What they commit to do]
```

## Comparison with Other Patterns

| Aspect | Consensus | Debate | Hierarchy |
|--------|-----------|--------|-----------|
| Goal | Agreement | Exploration | Decision |
| Time | Medium | Long | Short |
| Buy-in | High | Medium | Low |
| Quality | High | Very High | Variable |

## Related Agents

- `debate-moderator/` - Explores differences
- `hierarchy-manager/` - Top-down decisions
- `swarm-coordinator/` - Emergent consensus
