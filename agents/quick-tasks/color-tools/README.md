# Color Tools Expert

> **Quick Task Agent - Instant Results**

## Overview
Convert between color formats, generate palettes, ensure accessibility. Essential for designers and developers.

## Capabilities
- Convert between HEX, RGB, HSL, CMYK, Pantone
- Generate color palettes (complementary, analogous, triadic)
- Check WCAG contrast ratios
- Suggest accessible alternatives
- Extract colors from images
- Generate gradients
- Color name lookup
- Random palette generation

## Input
```json
{
  "action": "convert|palette|contrast|gradient|extract",
  "color": "#FF5500 or rgb(255,85,0)",
  "format": "hex|rgb|hsl|cmyk",
  "palette_type": "complementary|analogous|triadic|split-complement"
}
```

## Output
```json
{
  "hex": "#FF5500",
  "rgb": {"r": 255, "g": 85, "b": 0},
  "hsl": {"h": 20, "s": 100, "l": 50},
  "name": "International Orange",
  "palette": ["#FF5500", "#0055FF", "#55FF00"],
  "wcag_aa": true,
  "wcag_aaa": false,
  "contrast_ratio": 4.5
}
```

## Pricing
- **Free**: 50 operations/day
- **Pro**: Unlimited ($3.99/mo)

## Revenue Potential
$100-400/month

---

*Quick Task Agent - 20 second average usage*
