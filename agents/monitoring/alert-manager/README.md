# Alert Manager Agent

## Overview

Intelligent alert management system that reduces alert fatigue through smart deduplication, correlation, and prioritization.

## Core Capabilities

| Capability | Description |
|------------|-------------|
| Alert Deduplication | Eliminate duplicate alerts |
| Alert Correlation | Find related alerts |
| Priority Scoring | Score alert importance |
| Noise Reduction | Reduce false positives |
| Routing | Route to correct responders |

## Skills

### Primary Skills
1. **Alert Deduplication** - Identify and suppress duplicates
2. **Root Cause Analysis** - Find underlying causes
3. **Severity Assessment** - Assess true severity
4. **Correlation Engine** - Connect related alerts
5. **Escalation Management** - Manage escalation paths

### Secondary Skills
- Alert grouping
- Trend analysis
- Maintenance window awareness
- Team routing
- Runbook linking

## Use Cases

1. **IT Operations** - Manage infrastructure alerts
2. **Security Operations** - Security alert triage
3. **Application Monitoring** - Application alert management
4. **DevOps** - CI/CD alert management
5. **Business Operations** - Business metric alerts

## Example Alert Processing

### Alert Correlation
```
Input Alerts (5 minutes):
1. [CRITICAL] Database connection timeout - db-prod-01
2. [HIGH] API latency > 5s - api-gateway
3. [MEDIUM] High CPU usage - web-server-03
4. [CRITICAL] Database connection timeout - db-prod-01
5. [HIGH] API error rate > 10% - api-gateway

Processing:
- Deduplicate: Alert 4 is duplicate of Alert 1
- Correlate: Alerts 1, 2, 5 are related (database → API)
- Root Cause: Database connection issues causing API problems
- Severity: CRITICAL (higher than individual alerts)

Output Incident:
{
  "incident_id": "INC-2026-0328-001",
  "severity": "CRITICAL",
  "summary": "Database connection issues affecting API",
  "related_alerts": [1, 2, 5],
  "root_cause": "Database connection pool exhausted",
  "affected_services": ["api-gateway", "web-app"],
  "recommended_actions": [
    "Check database connection pool settings",
    "Review recent deployment changes",
    "Scale database connections if needed"
  ],
  "runbook": "https://wiki/incidents/db-connection-issues",
  "assigned_team": "database-oncall"
}
```

## Alert Priority Matrix

| Likelihood | Impact | Priority |
|------------|--------|----------|
| High | High | P1 - Critical |
| High | Medium | P2 - High |
| Medium | High | P2 - High |
| Medium | Medium | P3 - Medium |
| Low | High | P3 - Medium |
| Low | Medium | P4 - Low |

## Configuration

```json
{
  "agent_type": "alert-manager",
  "deduplication_window": 300,
  "correlation_window": 600,
  "noise_threshold": 0.3,
  "auto_suppress": true,
  "escalation_policies": {
    "P1": {"response_time": "5m", "team": "oncall-primary"},
    "P2": {"response_time": "30m", "team": "oncall-secondary"},
    "P3": {"response_time": "4h", "team": "team-lead"},
    "P4": {"response_time": "24h", "team": "business-hours"}
  }
}
```

## Performance Characteristics

| Metric | Value |
|--------|-------|
| Noise reduction | 70-80% |
| Correlation accuracy | 90%+ |
| Processing latency | <100ms |
| MTTR improvement | 30% |

## Monetization

- **Basic**: $0.05/alert processed
- **Pro**: $0.15/alert (with correlation)
- **Enterprise**: $1,000+/month unlimited

## Related Agents

- `incident-responder/` - Incident handling
- `threat-hunter/` - Security threats
- `escalation-engine/` - Intelligent routing
