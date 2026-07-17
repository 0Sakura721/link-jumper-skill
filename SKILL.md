---
name: link-jumper
description: >-
  A cross-platform link jumping and content consumption methodology for AI. 
  When you need: opening links to local Apps/browser (URL jumping), searching any platform and picking results (search jumping), 
  or getting real video stream URLs and playing locally with a player (local playback).
  No fixed platform list - teaches AI a **mindset** for handling links and content consumption across any new platform.
  
  通用跨平台链接跳转与多模式内容消费方法论。当你需要：将任意链接跳转到本地App/浏览器（URL跳转）、搜索任意平台的内容并在结果中选择跳转（搜索跳转）、
  获取任意视频的真实播放流地址并用本地播放器打开（本地播放）。不预设任何特定平台，AI 依据上下文自行决定如何搜索、解析和打开。
compatibility:
  - intent_routing: System Intent routing capability, used for ACTION_VIEW Intent to jump to links
  - command_line: Terminal/CLI capability, used for xdg-open / mpv on Linux
  - http_request: HTTP request capability, for searching or fetching streaming info
  - web_access: Web page access capability, for extracting search results or streaming info

---

# link-jumper - Universal Link Jumping & Content Consumption

## What It Solves

A cross-platform approach that transcends specific platforms and devices. AI understands a **methodology**, not a platform checklist - with the flexibility to handle links and content consumption beyond hardcoded platforms.

**Three operational modes:**

| Mode | Input to AI | Outcome |
|------|------------|---------|
| URL Jumping | http/https link -> AI parses protocol & decides | Invokes system Intent (Android) or xdg-open (Linux) to open in matching App/Browser |
| Search Jumping | "search on Y for X" or "open X on Y" | AI searches target platform -> reads results -> picks best match -> jumps |
| Local Playback | "play/watch X" or "open video/audio link" | AI extracts real video stream -> plays locally with mpv (Linux) or external player (Android) |

---

### Mode A: URL Jumping

Jump a URL to local app/browser.
- **Android**: `ACTION_VIEW` Intent with `uri=<url>` -> routes to best matching App
- **Linux**: `xdg-open <url>` or terminal-based opener
- **Special cases**: "open X in Chrome", "open X with Baidu App" -> use Intent with package name / app scheme

### Mode B: Search Jumping

When AI doesn't have direct API access:
1. **Is there a public/searchable API?** (GitHub, Bilibili, Twitter, etc. -> use visit_web)
2. **No API?** -> use web search `site:platform-name search-keyword`
3. **Search + parse**: extract from JSON/HTML, locate the target link
4. **Present to user**: summarize and confirm
5. **Jump**: execute the chosen jump method

> **For unsupported search targets:** use `visit_web <site>.com/search?q=<keyword>`

### Mode C: Local Playback - Stream Extraction

**Detect source:**
- Check if platform has streaming API (e.g. `api.bilibili.com/x/player/playurl`)
- Set proper Referer + User-Agent
- Parse response: is it a direct .mp4/.m3u8 link?
- Linux: use ffmpeg/yt-dlp for further extraction

**Play locally:**
- **Terminal command**: `mpv --http-header-fields="Referer: xxx" <stream_url>`
- **Intent jump**: directly invoke Intent with the video URL; fall back to Mode A

**DRM**: cannot extract DRM-protected content via Standard API -> fall back to Mode A.

---

## Tool Chain

- `intent_routing` -> Android Intent execution/URL routing
- `command_line` -> Linux shell execution
- `http_request` -> HTTP data fetching
- `web_access` -> Web page access for search/local parsing

---

## Design Principles

1. **Not platform-locked** -> new platform? Use `visit_web` to search, then apply same jumping logic.
2. **AI-driven decision making** -> AI already knows common platforms' search patterns. Use it.
3. **Graceful fallback** -> URL Jumping <- App <- Intent <- Local Playback. Each step = lower success rate.
4. **No hardcoded endpoints** -> no app-specific URL schemas; always use Referer for video extraction.

This skill is a **universal methodology** that AI applies with existing knowledge to handle links on any platform.
