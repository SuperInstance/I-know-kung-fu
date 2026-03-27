# Token Vault - Installation Guide

## Prerequisites

- Node.js v18+

## Quick Start

```bash
git clone https://github.com/your-org/token-vault-mcp.git
cd token-vault-mcp
npm install && npm run build

# Generate master key
npm run generate-key

npm start
```

## Claude Desktop Configuration

```json
{
  "mcpServers": {
    "token-vault": {
      "command": "node",
      "args": ["/path/to/token-vault/dist/index.js"],
      "env": {
        "VAULT_MASTER_KEY": "your-master-key",
        "VAULT_STORAGE_PATH": "/secure/vault"
      }
    }
  }
}
```

## Security Best Practices

1. Store master key in a secure location (not in code)
2. Use environment variables for configuration
3. Enable audit logging in production
4. Set up regular secret rotation
5. Use the principle of least privilege
