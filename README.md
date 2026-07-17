# Link Jumper — Universal Cross-Platform Link Jumping Methodology

> Teaches AI a universal methodology for link jumping, search jumping, and video content consumption — not bound to any specific platform or device.

[![version](https://img.shields.io/badge/version-1.0.1-blue)](https://github.com/0Sakura721/link-jumper-skill)
[![License](https://img.shields.io/badge/license-MIT-green)](https://github.com/0Sakura721/link-jumper-skill)

> [**🌐 English**](README.md) · [**🇨🇳 中文**](README_CN.md)

---

## Core Concept

link-jumper is a universal cross-platform content consumption methodology. Core philosophy: **Not bound to specific platforms or devices** — AI understands a methodology, not a platform checklist.

### Three Scenarios

| Your Problem | AI Solution |
|-------------|------------|
| Open a link | AI analyzes protocol + capabilities → invokes system Intent or command line |
| Search on a platform (no API) | AI uses generic search + parsing → finds content → jumps |
| Play a video/audio link | AI extracts streaming resource → plays locally |

## Architecture

**Three Operational Modes:**

- Mode A: URL Jumping — link → AI parses protocol → invokes system Intent / command line
- Mode B: Search Jumping — search intent → AI searches platform → parses results → jumps
- Mode C: Media Playback — video link → AI extracts stream → plays locally

**Design Principles:**

1. Not platform-locked — new platform? AI uses visit_web to search first
2. AI-driven decision making — AI knows common platforms search patterns
3. Graceful fallback — URL Jumping <- App <- Intent <- Local Playback
4. No hardcoded endpoints — always use Referer for video extraction

## File Structure



## Min Requirements

| Environment | Capability Needed |
|-------------|-------------------|
| Android | System Intent (ACTION_VIEW) |
| Linux | Command line (xdg-open/mpv) |

## License

[MIT](LICENSE) — Free and open-source, welcome to Fork and PR.
