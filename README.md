# Link Jumper — 通用跨平台链接跳转方法论

> 教会 AI **一套通用的链接跳转、搜索跳转和视频内容消费的思维方式**，不受限于特定平台或设备。

[![version](https://img.shields.io/badge/version-1.0.1-blue)](https://github.com/0Sakura721/link-jumper-skill)
[![License](https://img.shields.io/badge/license-MIT-green)](https://github.com/0Sakura721/link-jumper-skill)

> [**🌐 English**](README_EN.md) · [**🇨🇳 中文**](README.md)

---

## 目录

- [核心概念](#核心概念)
- [能力矩阵](#能力矩阵)
- [架构设计](#架构设计)
- [工具链对照](#工具链对照)
- [文件结构](#文件结构)
- [文件说明](#文件说明)
- [快速上手](#快速上手)
- [最低环境要求](#最低环境要求)
- [依赖准备](#依赖准备)
- [更新日志](#更新日志)
- [许可证](#许可证)

---

## 核心概念

 是一套 **通用跨平台消费方法论**。其核心理念是：

> **不预设具体平台或设备**，AI 理解的是**方法论**而非"平台清单"，面对任何新平台都能自行应对。

与传统硬编码平台列表不同， 定义的是一套 **思维框架**——教会 AI **"遇到链接怎么处理、遇到搜索怎么做、遇到视频怎么播放"** 这三个层面的通用解决方案。

### 三种场景

| 你遇到的问题 | link-jumper 的做法 |
|------------|-------------------|
|  链接 → 希望打开 App | **AI 分析协议 + 判断能力** → 调用系统 Intent 或命令行，以最匹配方式打开 |
| 想搜索平台内容（如查找某个 B 站视频，但没 API） | **AI 使用通用搜索 + 解析方式** → 找到内容后跳转 |
| 想播放视频/音频链接 | **AI 解析流媒体资源** → 提取真实播放地址 → 使用本地播放器播放 |

---

## 能力矩阵

| 能力 | 说明 |
|------|------|
| **🔗 URL 跳转** | AI 使用系统 Intent 或命令行（如 xdg-open - opens a file or URL in the user's preferred application

Synopsis

xdg-open { file | URL }

xdg-open { --help | --manual | --version }

Use 'man xdg-open' or 'xdg-open --manual' for additional info.）打开内容型链接 |
| **🔍 搜索跳转** | AI 引导用户 → 搜索目标平台 → 解析结果 → 找到目标 URL → 跳转打开 |
| **🎬 媒体播放** | AI 获取流地址 → 使用 mpv（Linux）/ 外部播放器（Android）+ Referer 处理 |
| **📧 通用链接** | 、 等协议直接跳转到对应 App |

---

## 架构设计

### 三层操作模式（取自 SKILL.md）



### 核心设计原则

1. **不锁定平台** — 遇到新平台时，AI 使用  先去搜索，再应用同一套跳转逻辑
2. **AI 自主决策** — AI 已有对常见平台搜索模式的知识储备，直接用起来
3. **优雅降级** — URL 跳转 ← App 打开 ← Intent 调用 ← 本地播放，每降一级成功率递减
4. **无硬编码端点** — 不预设特定应用的 URL Scheme，视频流提取始终使用 Referer

---

## 工具链对照

| 工具 | 环境 | 说明 |
|------|------|------|
| **Android** | 系统 Intent 调用（如 ） | 最高优先级的链接跳转方式 |
| **Linux** | 命令行（xdg-open - opens a file or URL in the user's preferred application

Synopsis

xdg-open { file | URL }

xdg-open { --help | --manual | --version }

Use 'man xdg-open' or 'xdg-open --manual' for additional info./mpv 0.37.0 Copyright © 2000-2023 mpv/MPlayer/mplayer2 projects
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
 --h=<string>      print options which contain the given string in their name） | 终端环境下的链接跳转/媒体播放 |
| **通用工具** | AI 自主调用多种能力 | 不限于特定工具，AI 可根据上下文灵活选择 |

---

## 文件结构



### 文件说明

| 文件 | 用途 | 维护状态 |
|------|------|---------|
|  | 核心 Skill 定义，含触发词、操作模式、设计原则 | ✅ 已就绪 |
|  | 中文说明文档，包含概念、架构、使用指南 | ✅ 已就绪 |
|  | English documentation | ✅ 已就绪 |
|  | 测试用例定义，覆盖正常/边界/异常场景 | ✅ 已就绪 |
|  | MIT 开源协议 | — |

---

## 快速上手

### 最低环境要求

| 环境 | 最低能力 | 说明 |
|------|---------|------|
| **Android** | 系统 Intent 调用能力 | 用于  等 Intent 跳转链接 |
| **Linux** | 命令行执行能力 | 用于 xdg-open - opens a file or URL in the user's preferred application

Synopsis

xdg-open { file | URL }

xdg-open { --help | --manual | --version }

Use 'man xdg-open' or 'xdg-open --manual' for additional info./mpv 0.37.0 Copyright © 2000-2023 mpv/MPlayer/mplayer2 projects
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
 --h=<string>      print options which contain the given string in their name 命令 |

### 依赖准备

- **mpv 0.37.0 Copyright © 2000-2023 mpv/MPlayer/mplayer2 projects
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
 --h=<string>      print options which contain the given string in their name**（Linux）— 用于媒体播放能力。安装：
- ****（Linux）— 常用于 xdg-open - opens a file or URL in the user's preferred application

Synopsis

xdg-open { file | URL }

xdg-open { --help | --manual | --version }

Use 'man xdg-open' or 'xdg-open --manual' for additional info. 打开链接

---

## 更新日志

> 以下为逐步积累的变更记录，后续将自动归档至 CHANGELOG。

| 版本 | 日期 | 变更内容 |
|------|------|---------|
| 1.0.1 | 2026-07-16 | 🔄 重构：通用多模态阅读框架，赋能 AI Agent 通用阅读能力 |
| 1.0.0 | 2026-07-16 | 📍 初始发布：3 种操作模式 + 4 个设计原则 |

---

## 许可证

[MIT](LICENSE) — 免费开源，欢迎 Fork 和 PR。
