# Regex Helper & Builder

> **Quick Task Agent - Instant Results**

## Overview
Build, test, and explain regular expressions. From natural language to working regex.

## Capabilities
- Generate regex from natural language description
- Explain any regex in plain English
- Test regex against sample text
- Optimize regex for performance
- Convert between regex flavors (Python, JS, PCRE, etc.)
- Generate code snippets
- Common pattern library (emails, phones, URLs, etc.)

## Input
```json
{
  "action": "generate|explain|test|optimize|convert",
  "description": "match email addresses",
  "regex": "[a-z]+@[a-z]+\\.[a-z]+",
  "test_string": "optional sample text",
  "flavor": "python|javascript|pcre|go"
}
```

## Output
```json
{
  "regex": "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}",
  "explanation": "Matches email addresses with local part, @ symbol, and domain",
  "matches": ["test@example.com"],
  "code_snippets": {
    "python": "import re\nre.findall(pattern, text)",
    "javascript": "text.match(new RegExp(pattern))"
  }
}
```

## Pricing
- **Free**: 30 regex operations/day
- **Pro**: Unlimited ($5.99/mo)

## Revenue Potential
$300-1,000/month

---

*Quick Task Agent - 45 second average usage*
