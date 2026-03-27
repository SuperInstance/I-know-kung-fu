# Circuit Breaker MCP Server

## Overview

The Circuit Breaker is an MCP (Model Context Protocol) server implementing the circuit breaker pattern for fault tolerance. It prevents cascading failures in distributed systems by detecting failures and stopping requests to failing services.

## Problem Statement

Distributed systems face reliability challenges:

- **Cascading Failures**: One service failure brings down others
- **Resource Exhaustion**: Continuing to call failing services
- **Slow Recovery**: Services don't recover under load
- **Timeout Management**: Knowing when to give up
- **Partial Degradation**: Maintaining service despite failures

## Solution

Circuit Breaker implements proven fault tolerance patterns:

```
┌─────────────────────────────────────────────────────────────┐
│                    CIRCUIT BREAKER                           │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│    CLOSED ─────────→ OPEN ─────────→ HALF-OPEN              │
│      ↑                │                   │                  │
│      │                │                   │                  │
│      └────────────────┴───────────────────┘                  │
│                                                              │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Failure   │  │   Timeout   │  │   Fallback  │         │
│  │  Detection  │  │   Manager   │  │   Handler   │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
└─────────────────────────────────────────────────────────────┘
```

## Key Features

### Circuit States
- **CLOSED**: Normal operation, requests pass through
- **OPEN**: Requests fail fast, no calls to failing service
- **HALF-OPEN**: Testing if service recovered

### Configuration Options
- **Failure Threshold**: Number of failures to open circuit
- **Timeout**: How long to wait for responses
- **Reset Timeout**: How long before trying again
- **Success Threshold**: Successes needed to close circuit

### Monitoring
- **State Transitions**: Track open/close events
- **Metrics**: Success/failure rates, latency
- **Alerts**: Notifications on state changes
- **Integration**: Prometheus, Datadog support

## Installation

```bash
git clone https://github.com/your-org/circuit-breaker-mcp.git
cd circuit-breaker-mcp
npm install && npm run build
npm start
```

## Configuration

```json
{
  "mcpServers": {
    "circuit-breaker": {
      "command": "node",
      "args": ["/path/to/circuit-breaker/dist/index.js"]
    }
  }
}
```

## Pricing

See [monetization.md](./monetization.md) for details.
