# Skills.sh Platform Guide

## Overview

Skills.sh is Vercel's agent skills directory - a marketplace for discovering and installing reusable skills for AI agents. Skills are modular packages that enhance AI tools with specific capabilities.

## Platform Characteristics

| Aspect | Details |
|--------|---------|
| Type | Skill marketplace/directory |
| Maintainer | Vercel |
| Target | Claude Code, Cursor, Copilot, etc. |
| Best for | Reusable agent capabilities |
| Cost | Free to browse, varies by skill |

## Key Features

1. **Skill Discovery** - Browse 106,000+ skills
2. **One-Command Install** - Easy installation
3. **Versioning** - Versioned skills with rollback
4. **Categories** - Organized by function
5. **Quality Metrics** - Weekly install counts
6. **Multi-Tool Support** - Works with 20+ AI tools

## Supported Tools

- Claude Code
- Cursor
- GitHub Copilot
- Codex
- Windsurf
- Zed
- And 20+ more

## Skill Structure

```markdown
# skill-name

## Description
Brief description of what the skill does.

## Usage
How to use the skill.

## Examples
Example usage scenarios.

## Configuration
Any configuration options.

## Dependencies
Required tools or packages.
```

## Installation

```bash
# Install a skill
npx skills install skill-name

# Install with specific version
npx skills install skill-name@1.2.0

# Install from URL
npx skills install https://github.com/user/skill-repo
```

## Creating Skills

### Basic Skill Template
```markdown
# My Skill

> One-line description of the skill

## Purpose

Detailed explanation of what this skill does and when to use it.

## Instructions

Step-by-step instructions for the AI to follow:

1. First, analyze the input
2. Then, process the data
3. Finally, generate output

## Examples

### Example 1: Basic Usage
Input: "example input"
Output: "expected output"

### Example 2: Advanced Usage
Input: "complex input"
Output: "complex output"

## Notes

- Important considerations
- Edge cases to handle
- Best practices
```

### Advanced Skill with Functions
```javascript
// skill.js
export default {
  name: "data-analyzer",
  description: "Analyze data and generate insights",
  
  async execute(input, context) {
    // Process input
    const data = await this.parseInput(input);
    
    // Analyze
    const insights = await this.analyze(data);
    
    // Return results
    return {
      insights,
      recommendations: this.generateRecommendations(insights)
    };
  },
  
  async parseInput(input) {
    // Implementation
  },
  
  async analyze(data) {
    // Implementation
  }
};
```

## Skill Categories

### Development Skills
- Code generation
- Debugging
- Refactoring
- Testing

### Analysis Skills
- Data analysis
- Code review
- Performance profiling
- Security scanning

### Automation Skills
- Task automation
- File processing
- API integration
- Workflow orchestration

### Domain Skills
- Finance
- Healthcare
- Legal
- Education

## Publishing Skills

### To GitHub
1. Create repository with skill files
2. Add README with documentation
3. Tag releases with versions
4. Submit to Skills.sh directory

### Package.json
```json
{
  "name": "my-skill",
  "version": "1.0.0",
  "description": "What the skill does",
  "main": "skill.js",
  "keywords": ["ai", "skill", "agent"],
  "author": "your-name",
  "license": "MIT"
}
```

## Monetization Strategies

### Free Skills (Lead Generation)
- Build audience
- Demonstrate expertise
- Drive consulting inquiries

### Paid Skills
- Premium capabilities
- Advanced features
- Enterprise support

### Subscription
- Ongoing updates
- Priority support
- Custom modifications

## Popular Skill Metrics

| Skill Category | Avg Weekly Installs |
|---------------|---------------------|
| Code Generation | 5,000+ |
| Testing | 2,000+ |
| Documentation | 1,500+ |
| Security | 1,000+ |
| Deployment | 800+ |

## Quality Guidelines

1. **Clear Purpose** - What the skill does
2. **Good Examples** - Multiple use cases
3. **Error Handling** - Graceful failures
4. **Documentation** - Complete instructions
5. **Testing** - Verified functionality

## Security Considerations

- Skills can have security vulnerabilities
- Snyk found 36% of skills have issues
- Always vet skills before installing
- Check for prompt injection risks
- Review code before using

## Integration Examples

### With Claude Code
```bash
# Install skill for Claude Code
claude-code skill install skill-name

# Use in Claude Code
# Skill is automatically loaded and available
```

### With Cursor
```bash
# Install for Cursor
cursor skill install skill-name

# Skill appears in Cursor's skill panel
```

## Related Links

- Official Site: https://skills.sh
- Documentation: https://skills.sh/docs
- GitHub Integration: Automatic
- Community: Discord

## Agents We Recommend for Skills.sh

1. **React Reasoner** - `agents/reasoning-patterns/react-reasoner/`
2. **Plan Executor** - `agents/reasoning-patterns/plan-executor/`
3. **Quick Tasks** - `agents/quick-tasks/` (multiple)
4. **Code Reviewer** - `agents/validation/code-reviewer/`
