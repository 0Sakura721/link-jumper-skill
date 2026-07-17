# Link Jumper - Universal Link Jumping and Content Consumption

> Teaches AI a universal methodology for link jumping, search jumping, and video playback.

[![version](https://img.shields.io/badge/version-1.0.1-blue)](https://github.com/0Sakura721/link-jumper-skill)
[![License](https://img.shields.io/badge/license-MIT-green)](https://github.com/0Sakura721/link-jumper-skill)

> [EN](README_EN.md) [CN](README.md)

---

## Design Philosophy

link-jumper is a methodology-based thinking framework. No platform assumptions, AI decides based on context.

### Three Modes

| Mode | Input | AI Behavior |
|------|-------|-------------|
| URL Jumping | http/https link | Invokes system Intent (Android) or xdg-open (Linux) |
| Search Jumping | search xxx on yyy | AI searches target, parses, jumps |
| Local Playback | play/watch video | AI extracts stream, plays locally |

---

## File Structure

```
link-jumper/
SKILL.md          Core Skill definition
README.md         Chinese
README_EN.md      This file (English)
LICENSE           MIT
```

## License

MIT