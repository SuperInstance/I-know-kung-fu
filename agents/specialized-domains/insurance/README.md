# Insurance Agent

## Overview

Specialized agent for insurance operations including underwriting support, claims processing, risk assessment, and policy management.

## Core Capabilities

| Capability | Description |
|------------|-------------|
| Underwriting Support | Assist risk assessment and pricing |
| Claims Processing | Streamline claims handling |
| Risk Assessment | Evaluate and score risks |
| Policy Management | Manage policy lifecycle |
| Fraud Detection | Identify suspicious claims |

## Skills

### Primary Skills
1. **Risk Scoring** - Calculate risk scores
2. **Claims Triage** - Prioritize and route claims
3. **Document Analysis** - Analyze policy documents
4. **Fraud Detection** - Identify fraud indicators
5. **Premium Calculation** - Calculate appropriate premiums

### Secondary Skills
- Compliance checking
- Customer communication
- Renewal management
- Coverage comparison
- Loss prediction

## Use Cases

1. **Underwriting** - Support risk assessment
2. **Claims Handling** - Process claims efficiently
3. **Customer Service** - Answer policy questions
4. **Fraud Prevention** - Detect suspicious activity
5. **Actuarial Support** - Data analysis

## Example Interactions

### Claims Triage
```
User: "Process this auto claim: $12,500 rear-end collision"

Agent Analysis:
Claim Details:
- Type: Auto collision
- Amount: $12,500
- Coverage: Comprehensive + Collision
- Deductible: $500
- Policy standing: Active, 3 years

Risk Assessment:
┌─────────────────────────────────────────────────┐
│ Factor          │ Status   │ Weight │ Score    │
├─────────────────────────────────────────────────┤
│ Police report   │ ✓ Filed  │ High   │ +20      │
│ Photos provided │ ✓ 6 imgs │ High   │ +15      │
│ Witness         │ ✗ None   │ Medium │ -10      │
│ Prior claims    │ 0 in 3yr │ Low    │ +10      │
│ At-fault        │ Other    │ High   │ +25      │
│ Fraud flags     │ None     │ High   │ +20      │
└─────────────────────────────────────────────────┘

Total Score: 80/100 (Low Risk)

Recommendation: FAST-TRACK
- Approve within 24 hours
- Payout estimate: $12,000 (after deductible)
- Assign to: Standard claims team
- No SIU referral needed

Next Steps:
1. Verify repair estimate
2. Confirm other party insurance
3. Issue payment within 3 business days
```

### Underwriting Support
```
User: "Assess risk for commercial property: warehouse, $2M value"

Agent Analysis:
Property Details:
- Type: Warehouse
- Value: $2,000,000
- Location: Industrial park, Suburban
- Year built: 1995
- Square footage: 45,000

Risk Assessment:
┌─────────────────────────────────────────────────┐
│ Category       │ Factor         │ Risk Level   │
├─────────────────────────────────────────────────┤
│ Fire           │ Sprinklers ✓   │ Low          │
│                │ Fire station 2mi│ Low          │
│ Theft          │ Security sys ✓ │ Low          │
│                │ Gated access ✓ │ Low          │
│ Natural        │ Flood zone X   │ None         │
│                │ Earthquake low │ Low          │
│ Liability      │ Low foot traffic│ Low         │
└─────────────────────────────────────────────────┘

Overall Risk Score: 72/100 (Below Average Risk)

Premium Recommendation:
- Base rate: $4,800/year
- Risk adjustment: -15%
- Final premium: $4,080/year

Coverage Terms:
- Deductible: $2,500
- Co-insurance: 80%
- Exclusions: Standard

Recommendation: APPROVE with standard terms
```

## Configuration

```json
{
  "agent_type": "insurance",
  "line_of_business": ["auto", "property", "commercial"],
  "risk_models": {
    "auto": "version_3.2",
    "property": "version_2.8",
    "commercial": "version_2.1"
  },
  "fraud_detection": {
    "enabled": true,
    "threshold": 0.7,
    "auto_refer": true
  },
  "compliance": {
    "regulations": ["state_insurance_law", "naic"],
    "audit_trail": true
  }
}
```

## Monetization

- **Per-assessment**: $1-10
- **Per-claim processed**: $5-25
- **SaaS subscription**: $1,000-10,000/month
- **Enterprise carrier**: Custom pricing

## Related Agents

- `legal-document-suite/` - Document handling
- `financial-analysis-suite/` - Financial analysis
- `compliance-checker/` - Compliance verification
