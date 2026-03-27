# Token Vault MCP Server

## Overview

The Token Vault is a secure MCP (Model Context Protocol) server for managing API keys, tokens, and sensitive credentials. It provides encrypted storage, access control, and audit logging for all your AI agent secrets.

## Problem Statement

Managing API keys and tokens is risky:

- **Exposure Risk**: Keys in code, configs, or environment variables
- **Rotation Challenges**: Manually rotating keys is error-prone
- **Access Control**: Who accessed what, when?
- **Compliance**: Audit trails required for security
- **Multi-Environment**: Different keys for dev/staging/prod

## Solution

Token Vault provides secure credential management:

```
┌─────────────────────────────────────────────────────────────┐
│                      TOKEN VAULT                             │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │  Encryption │  │   Access    │  │   Audit     │         │
│  │   Engine    │  │   Control   │  │   Logging   │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│         ↓                ↓                ↓                  │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Keys &    │  │   Secret    │  │   Rotation  │         │
│  │   Tokens    │  │   Sharing   │  │   Manager   │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
└─────────────────────────────────────────────────────────────┘
```

## Key Features

### Secure Storage
- **AES-256 Encryption**: Military-grade encryption at rest
- **Key Derivation**: PBKDF2 with unique salts
- **Memory Security**: Keys never stored in plain text
- **Secure Deletion**: Crypto-shredding for deleted secrets

### Access Control
- **Role-Based Access**: Define who can access what
- **Time-Limited Tokens**: Temporary access grants
- **IP Restrictions**: Limit access by IP range
- **MFA Support**: Require additional authentication

### Audit & Compliance
- **Complete Audit Trail**: Every access logged
- **Alert System**: Notify on suspicious activity
- **Export Reports**: Compliance-ready documentation
- **Retention Policies**: Configurable log retention

### Secret Management
- **Multiple Secret Types**: API keys, OAuth tokens, certificates
- **Environment Segregation**: Separate dev/staging/prod
- **Automatic Rotation**: Scheduled key rotation
- **Version History**: Track secret changes

## Installation

```bash
git clone https://github.com/your-org/token-vault-mcp.git
cd token-vault-mcp
npm install && npm run build
npm start
```

## Configuration

```json
{
  "mcpServers": {
    "token-vault": {
      "command": "node",
      "args": ["/path/to/token-vault/dist/index.js"],
      "env": {
        "VAULT_MASTER_KEY": "your-master-encryption-key"
      }
    }
  }
}
```

## Pricing

See [monetization.md](./monetization.md) for details.
