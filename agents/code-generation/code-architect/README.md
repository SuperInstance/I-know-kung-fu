# Code Architect Agent

## Overview

The Code Architect agent designs software architectures, makes technical decisions, and creates implementation plans for complex software systems.

## Core Concept

Architecture workflow:
1. **Requirements Analysis** - Understand functional and non-functional requirements
2. **Technology Selection** - Choose appropriate technologies
3. **Architecture Design** - Design system structure
4. **Documentation** - Create architecture documentation
5. **Review & Iterate** - Refine based on feedback

## Skills

### Primary Skills
1. **System Design** - Design scalable system architectures
2. **Technology Evaluation** - Evaluate and select technologies
3. **Trade-off Analysis** - Analyze architectural trade-offs
4. **Documentation** - Create clear architecture documents
5. **Pattern Recognition** - Apply appropriate design patterns

### Secondary Skills
- Cost estimation
- Performance modeling
- Security architecture
- Migration planning
- Technical debt assessment

## Use Cases

1. **New System Design** - Design new software systems
2. **Architecture Review** - Review existing architectures
3. **Technology Migration** - Plan technology migrations
4. **Scalability Planning** - Design for scale
5. **Documentation** - Create architecture documentation

## Example Architecture Output

### Microservices Architecture
```yaml
architecture:
  name: "E-commerce Platform"
  style: "Microservices"
  
  services:
    - name: "User Service"
      technology: "Node.js, PostgreSQL"
      responsibilities: ["Authentication", "User management"]
      scaling: "Horizontal"
      
    - name: "Product Service"
      technology: "Python, MongoDB"
      responsibilities: ["Product catalog", "Inventory"]
      scaling: "Horizontal"
      
    - name: "Order Service"
      technology: "Java, PostgreSQL"
      responsibilities: ["Order processing", "Payment"]
      scaling: "Horizontal"
      
  infrastructure:
    orchestration: "Kubernetes"
    message_queue: "RabbitMQ"
    cache: "Redis"
    api_gateway: "Kong"
    
  patterns:
    - "CQRS for Order Service"
    - "Event Sourcing for Audit"
    - "Circuit Breaker for resilience"
    
  decisions:
    - decision: "Use event-driven architecture"
      rationale: "Enables loose coupling and scalability"
      tradeoffs: "Added complexity, eventual consistency"
```

## Configuration

```json
{
  "agent_type": "code-architect",
  "design_depth": "comprehensive",
  "documentation_format": "markdown",
  "include_code_examples": true,
  "consider_costs": true,
  "security_by_default": true,
  "scalability_focus": true
}
```

## Performance Characteristics

| Metric | Value |
|--------|-------|
| Design quality | High |
| Pattern accuracy | 95% |
| Documentation clarity | Excellent |
| Best for | New projects |

## Monetization Strategy

### Pricing Tiers
- **Basic**: $5.00/architecture (simple systems)
- **Pro**: $25.00/architecture (complex systems)
- **Enterprise**: $100.00/architecture (full documentation)

### Target Markets
1. Software development teams
2. Startups
3. Enterprise architecture teams
4. Consulting firms

## Related Agents

- `refactoring-engine/` - Refactor existing code
- `api-designer/` - API design focus
- `codebase-onboarder/` - Understand existing code
