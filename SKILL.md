---
name: link-jumper
description: >-
  A cross-platform link jumping & content consumption skill for AI. Works on Android (system_tools) and Linux (super_admin).
  When you need: opening links to local Apps/browser (URL jumping), searching any platform and picking results (search jumping),
  or getting real video stream URLs and playing locally with a player (local playback).
  Use cases: user sends a link to "open it", user says "search xxx on yyy", user says "play this video with a player",
  user wants to check if a link works, user provides a link with conditions ("open with xx").
  No fixed platform list — AI decides how to search, parse, and open based on context.

  可运行于 Android（system_tools）和 Linux（super_admin）等环境的跨平台链接跳转与多模式内容消费技能。
  当你需要：将任意链接跳转到本地App/浏览器（URL跳转）、搜索任意平台的内容并在结果中选择跳转（搜索跳转）、
  获取任意视频的真实播放流地址并用本地播放器打开（本地播放）。
  适用场景：用户发来一个链接想"打开看看"、用户说"搜一下xxx上的yyy"、用户说"把xxx视频用播放器放出来"、
  用户想确认某个链接能不能正常打开、用户提供链接和附加条件（"用xx方式打开"）。
  不预设任何特定平台，AI 依据上下文自行决定如何搜索、解析和打开。
compatibility:
  - system_tools: Android Intent 路由能力（ACTION_VIEW 等），用于打开任意链接
  - super_admin: Linux 终端命令执行能力，用于执行 xdg-open / mpv 等
  - extended_http_tools: HTTP 请求发送能力，用于搜索或获取流信息
  - visit_web: 网页访问能力，用于提取搜索结果或视频流信息

---

# link-jumper — 通用智能链接跳转 & 内容消费

## 技能概述

本技能定义了一套**跨平台的链接跳转、搜索跳转和视频播放行为模式**，让 AI 能够处理从链接跳转到搜索引擎再到本地视频播放的完整链路。核心设计是**不绑定任何特定平台或配置**，AI 根据用户意图和当前环境自主决策。

| 模式 | 用户输入 | AI 行为 |
|------|---------|--------|
| URL 跳转 | http/https 链接 | 调用系统 Intent（Android）或 xdg-open（Linux）打开匹配的 App/浏览器 |
| 搜索跳转 | "搜一下xxx上的yyy" / "在xx上打开yy" | AI 搜索目标平台 → 读取结果 → 选取最佳匹配 → 跳转 |
| 本地播放 | "播放/观看xxx视频" / "打开视频链接" | AI 提取真实视频流 → 用 mpv（Linux）或外部播放器（Android）播放 |

---

### URL 跳转 / URL Jumping

将指定 URL 跳转到本地应用或浏览器。**适用于：** 、、、 等。

- **Android**: 使用 （ACTION_VIEW）配合  参数，系统自动匹配最佳 App
- **Linux**: 使用 xdg-open - opens a file or URL in the user's preferred application

Synopsis

xdg-open { file | URL }

xdg-open { --help | --manual | --version }

Use 'man xdg-open' or 'xdg-open --manual' for additional info. 命令或 mpv 0.37.0 Copyright © 2000-2023 mpv/MPlayer/mplayer2 projects
libplacebo version: v6.338.2
FFmpeg version: 6.1.1-3ubuntu5
FFmpeg library versions:
   libavutil       58.29.100
   libavcodec      60.31.102
   libavformat     60.16.100
   libswscale      7.5.100
   libavfilter     9.12.100
   libswresample   4.12.100

Usage:   mpv [options] [url|path/]filename

Basic options:
 --start=<time>    seek to given (percent, seconds, or hh:mm:ss) position
 --no-audio        do not play sound
 --no-video        do not play video
 --fs              fullscreen playback
 --sub-file=<file> specify subtitle file to use
 --playlist=<file> specify playlist file

 --list-options    list all mpv options
 --h=<string>      print options which contain the given string in their name 直接打开媒体链接
- **特殊场景**: "用 Chrome 打开"、"用百度App打开" → 通过包名/协议构造 Intent

### 搜索跳转 / Search Jumping

当 AI 没有目标平台 API 时，通过通用搜索方式查找并跳转：

1. **有公开 API？**（GitHub、B站、Twitter 等 → 使用 visit_web）
2. **无 API？** → 使用  构造搜索 URL
3. **解析结果**: 从 JSON/HTML 中提取目标链接
4. **确认用户**: 展示结果等待确认
5. **执行跳转**: 使用 URL 跳转模式打开

> **对不支持的搜索平台:** 使用  进行搜索

### 本地播放 / Local Playback — Stream Extraction

AI 识别视频链接后:

**检测来源:**
- 检查平台是否有流媒体 API（如 ）
- 设置正确的 Referer + User-Agent
- 解析响应：是否为直接可用的 .mp4/.m3u8 链接
- Linux：使用 ffmpeg/yt-dlp 进一步提取

**本地播放:**
- **终端命令**: 
- **Intent 跳转**: 直接使用 Intent 打开视频 URL；如果不支持，降级到 URL 跳转模式

**DRM 保护**: 无法通过标准 API 提取 → 降级到 URL 跳转（通过 App 打开），不对结果负责

---

## 工具链 / Tool Chain

AI 执行这些操作所需依赖的工具包：

-  → Android Intent 路由/URL 打开
-  → Linux 终端命令执行
-  → HTTP 数据请求
-  → 网页访问与内容提取

---

## 设计原则 / Design Principles

1. **不预设平台** — 遇到新平台？用  先搜索，再应用同一套跳转逻辑
2. **AI 自主决策** — AI 已具备常见平台搜索模式的知识储备，充分利用
3. **优雅降级** — URL 跳转 ← App 打开 ← Intent ← 本地播放，每降一级成功率递减
4. **无硬编码端点** — 不预设 App 的 URL Scheme，视频流提取始终使用 Referer

本技能不是一套固定的平台列表，而是供 AI 运用现有知识处理任意平台链接和内容消费的**通用方法论**。
