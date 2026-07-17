# Link Jumper — 通用智能链接跳转 & 内容消费

> 教会 AI 一套通用的链接跳转、搜索跳转和视频播放的思维方法，而非绑定任何具体平台或前端组件。

[![version](https://img.shields.io/badge/version-1.0.1-blue)](https://github.com/0Sakura721/link-jumper-skill)
[![License](https://img.shields.io/badge/license-MIT-green)](https://github.com/0Sakura721/link-jumper-skill)

> [🌐 English](README_EN.md) · [🇨🇳 中文](README.md)

---

## 设计理念

link-jumper 是一套通用方法论型的思维框架。核心设计原则：不预设任何平台，不锁死任何配置，AI依据上下文自主判断如何处理链接。

### 三种操作模式

| 模式 | 用户输入 | AI行为 |
|------|---------|--------|
| URL跳转 | http/https链接 | 调用系统Intent(Android)或xdg-open(Linux) |
| 搜索跳转 | 搜一下xxx上的yyy | AI搜索目标平台→解析结果→跳转 |
| 本地播放 | 播放xxx视频 | AI提取视频流→mpv或外部播放器播放 |

## 能力概览

| 场景 | 行为 |
|------|------|
| 链接跳转 | AI使用系统Intent或终端命令打开目标链接 |
| 搜索跳转 | AI分析用户意图→推理目标平台→构造搜索URL |
| 视频播放 | AI提取流地址→本地播放器+Referer防盗链处理 |

## 文件结构



## 许可证

[MIT](LICENSE) — 免费开源，欢迎Fork和PR。
