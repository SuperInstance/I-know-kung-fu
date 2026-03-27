# Hospitality Agent

## Overview

Specialized agent for hospitality operations including guest services, booking management, revenue optimization, and customer experience enhancement.

## Core Capabilities

| Capability | Description |
|------------|-------------|
| Guest Services | Handle guest requests and issues |
| Booking Management | Manage reservations and availability |
| Revenue Optimization | Optimize pricing and occupancy |
| Customer Experience | Enhance guest satisfaction |
| Operations | Streamline hotel operations |

## Skills

### Primary Skills
1. **Reservation Handling** - Manage bookings and modifications
2. **Guest Communication** - Respond to guest inquiries
3. **Revenue Management** - Dynamic pricing optimization
4. **Service Recovery** - Handle complaints and issues
5. **Personalization** - Customize guest experiences

### Secondary Skills
- Loyalty program management
- Room allocation optimization
- Amenity recommendations
- Feedback collection
- Upselling opportunities

## Use Cases

1. **Front Desk Support** - Assist reception staff
2. **Guest Communications** - Handle inquiries 24/7
3. **Revenue Management** - Optimize pricing
4. **Quality Assurance** - Monitor guest satisfaction
5. **Marketing** - Personalized promotions

## Example Interactions

### Guest Inquiry
```
User: "A guest asks about late checkout for room 405"

Agent Response:
Guest Profile:
- Name: John Smith
- Status: Gold Member
- Room: 405 (Deluxe King)
- Current checkout: 11:00 AM
- Requested: 2:00 PM checkout

Availability Check:
- Room 405: No conflict
- Same-day arrival: None until 4:00 PM

Recommendation: APPROVE late checkout
- Gold member benefit
- No operational conflict
- Goodwill gesture

Response Template:
"Mr. Smith, as a valued Gold member, I'm happy to 
accommodate your late checkout request until 2:00 PM.
Is there anything else I can assist you with?"

Alternative: If conflict, offer luggage storage and lounge access.
```

### Revenue Optimization
```
User: "What should we charge for next weekend?"

Agent Analysis:
- Dates: Friday-Saturday (high demand)
- Current occupancy: 87%
- Historical: Same weekend last year = 92%
- Events: Convention in town (+15% demand)
- Competitor rates: $199-$249

Recommendation:
┌────────────────────────────────────────────────┐
│ Room Type     │ Current │ Recommended │ Reason │
├────────────────────────────────────────────────┤
│ Standard      │ $149    │ $189        │ High   │
│ Deluxe        │ $199    │ $249        │ High   │
│ Suite         │ $299    │ $349        │ Med    │
└────────────────────────────────────────────────┘

Strategy: 
- Raise rates Thursday PM
- Hold 5 rooms for last-minute premium
- Package with breakfast (+$30 value)

Expected Revenue Increase: +$4,200
```

## Configuration

```json
{
  "agent_type": "hospitality",
  "property_type": "hotel",
  "service_level": "full_service",
  "integrations": {
    "pms": "opera",
    "crm": "salesforce",
    "revenue_system": "idp"
  },
  "languages": ["en", "es", "fr", "zh"],
  "escalation_rules": {
    "vip_guest": "manager",
    "complaint": "duty_manager"
  }
}
```

## Monetization

- **Per-property**: $500-5,000/month
- **Per-interaction**: $0.10-0.50
- **Enterprise chain**: Custom pricing

## Related Agents

- `ecommerce-retail/` - Retail operations
- `customer-support-suite/` - Support tools
- `conversation/dialogue-manager/` - Conversations
