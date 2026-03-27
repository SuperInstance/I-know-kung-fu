# ClawHub Platform Guide

## Overview

ClawHub is a skill marketplace for AI agents, allowing developers to upload, version, and distribute AgentSkills bundles. It's designed for the emerging AI agent ecosystem with versioning similar to npm.

## Platform Characteristics

| Aspect | Details |
|--------|---------|
| Type | Skill marketplace |
| Versioning | npm-like |
| Search | Vector-based |
| Best for | Skill distribution |
| Cost | Free to publish |

## Key Features

1. **Skill Upload** - Upload AgentSkills bundles
2. **Versioning** - Semantic versioning with rollback
3. **Vector Search** - AI-powered skill discovery
4. **Curation** - Highlighted quality skills
5. **No Gatekeeping** - Open access

## Skill Package Structure

```
my-skill/
├── skill.md          # Main skill definition
├── README.md         # Documentation
├── package.json      # Metadata
├── examples/         # Usage examples
│   ├── example1.md
│   └── example2.md
└── tests/            # Test cases
    └── test.md
```

## Skill Definition Format

```markdown
# Skill Name

## Metadata
- Author: Your Name
- Version: 1.0.0
- Tags: category, functionality, use-case

## Description
What this skill does and when to use it.

## Capabilities
- Capability 1
- Capability 2
- Capability 3

## Usage

### Basic Usage
```prompt
Example prompt that triggers the skill
```

### Advanced Usage
```prompt
More complex usage example
```

## Requirements
- Required tools or access
- Dependencies

## Configuration
Any configuration options needed.

## Examples
Real-world examples with inputs and outputs.
```

## Publishing Skills

### CLI Upload
```bash
# Install ClawHub CLI
npm install -g clawhub

# Login
clawhub login

# Publish skill
clawhub publish ./my-skill

# Update version
clawhub version patch
clawhub publish
```

### Web Upload
1. Create account on ClawHub
2. Create new skill
3. Upload files
4. Add metadata
5. Publish

## Version Management

```bash
# List versions
clawhub versions my-skill

# Rollback to previous version
clawhub rollback my-skill@1.0.0

# Deprecate version
clawhub deprecate my-skill@1.0.1
```

## Skill Categories

### Development
- Code generation
- Debugging
- Refactoring
- Documentation

### Analysis
- Data analysis
- Security scanning
- Performance profiling
- Log analysis

### Automation
- Task automation
- Workflow orchestration
- Integration
- Batch processing

### Communication
- Email drafting
- Report generation
- Translation
- Summarization

## Discovery Features

### Vector Search
AI-powered semantic search:
```
Query: "analyze code for security issues"
Results: Skills related to security analysis, code review, vulnerability scanning
```

### Tag Filtering
Filter by tags:
```
tags: ["security", "code-review", "static-analysis"]
```

### Curated Lists
Highlighted quality skills:
- Editor's picks
- Trending skills
- New releases
- Category leaders

## Security Considerations

**Important**: Snyk found security issues in 36% of skills:
- Prompt injection vulnerabilities
- Data exfiltration risks
- Malicious code execution

### Vetting Skills
```bash
# Scan skill for vulnerabilities
clawhub scan my-skill

# View security report
clawhub security-report my-skill
```

## Monetization Strategies

### Free Skills (Marketing)
- Build reputation
- Drive consulting
- Attract users to paid offerings

### Premium Skills
- Advanced capabilities
- Enterprise features
- Support included

### Custom Skills
- Build-to-order skills
- Private deployments
- Enterprise licensing

## Integration Examples

### With Claude Code
```bash
# Install skill from ClawHub
claude-code skill install clawhub:my-skill

# Install specific version
claude-code skill install clawhub:my-skill@1.2.0
```

### With Custom Agents
```python
import requests

# Fetch skill from ClawHub
response = requests.get(
    "https://clawhub.ai/api/skills/my-skill/latest"
)
skill = response.json()

# Apply to agent
agent.add_skill(skill)
```

## Package.json Format

```json
{
  "name": "my-skill",
  "version": "1.0.0",
  "description": "Skill for doing X, Y, Z",
  "author": "Your Name",
  "license": "MIT",
  "keywords": [
    "ai",
    "skill",
    "agent",
    "category"
  ],
  "dependencies": {
    "other-skill": "^2.0.0"
  },
  "clawhub": {
    "category": "development",
    "tools": ["code-editor", "terminal"],
    "models": ["gpt-4", "claude-3"]
  }
}
```

## Statistics

| Metric | Value |
|--------|-------|
| Total Skills | 100,000+ |
| Active Developers | 10,000+ |
| Weekly Downloads | 500,000+ |
| Categories | 50+ |

## Related Links

- Official Site: https://clawhub.ai
- Documentation: https://clawhub.ai/docs
- CLI: npm install -g clawhub
- Security Scanner: Built-in

## Agents We Recommend for ClawHub

1. **Quick Tasks** - All quick-task agents are ideal
2. **Code Reviewer** - `agents/validation/code-reviewer/`
3. **Security Analyst** - `agents/role-based/security-analyst/`
4. **Document Processor** - `platforms/minimax-experts/document-processor/`
