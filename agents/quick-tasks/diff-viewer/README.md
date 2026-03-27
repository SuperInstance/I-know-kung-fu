# Diff Viewer Expert

> **Quick Task Agent - Instant Results**

## Overview
Compare texts, code, or JSON and generate beautiful diff outputs. Essential for code reviews and document comparison.

## Capabilities
- Side-by-side diff comparison
- Unified diff format
- Line-by-line highlighting
- Word-level diff
- Semantic diff for code
- Ignore whitespace options
- Diff statistics
- Merge conflict detection

## Input
```json
{
  "original": "string or code",
  "modified": "string or code",
  "format": "side-by-side|unified|html",
  "options": {
    "ignore_whitespace": true,
    "word_level": false,
    "language": "javascript|python|..."
  }
}
```

## Output
```json
{
  "diff": "formatted diff output",
  "stats": {
    "added": 12,
    "removed": 5,
    "unchanged": 100,
    "changed_files": 3
  },
  "html": "colorized HTML diff"
}
```

## Pricing
- **Free**: 30 diffs/day
- **Pro**: Unlimited ($4.99/mo)

## Revenue Potential
$150-500/month

---

*Quick Task Agent - 25 second average usage*
