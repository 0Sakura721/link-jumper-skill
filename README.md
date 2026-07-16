# link-jumper — 通用跨平台链接跳转 Skill

> 教会 AI **一套通用的链接跳转、搜索跳转和视频播放的思维方法**，而非绑定任何具体平台。

## 概述

`link-jumper` 是面向 Operit AI Agent 的一个**通用方法论型 Skill**。它的核心思想是：

> **不预设任何平台，不锁死任何配置，AI 依据上下文自主判断如何处理链接。**

无论是普通网页链接、搜索关键词、视频流地址，还是 `mailto:`、`tel:` 等特殊协议，AI 都能自行推理出合适的处理方式并执行。

## 能力

| 场景 | 行为 |
|------|------|
| **链接跳转** | 直接使用 `system_tools:execute_intent`（Android）/ `xdg-open`（Linux）打开 |
| **搜索跳转** | AI 自行分析用户意图 → 推理目标平台 → 构造搜索 URL 并打开 |
| **视频播放** | AI 自行提取流地址 → 使用本地播放器（如 `mpv`）+ Referer 防盗链头处理 |
| **特殊协议** | `mailto:`、`tel:` 等直接路由到系统对应 App |

## 环境支持

- **Android** — 使用 `system_tools:execute_intent` 实现 Intent 跳转
- **Linux** — 使用 `super_admin:terminal` 执行 `xdg-open` 或 `mpv`

## 文件结构

```
link-jumper/
├── SKILL.md          ← 核心技能定义（通用方法论）
├── README.md         ← 本文件
├── LICENSE           ← MIT 许可证
├── test_cases.md     → 测试用例
├── references/       → 参考文档（可选）
└── scripts/          → 辅助脚本（可选）
```

## 使用前提

需要激活以下工具包：

| 环境 | 所需工具包 |
|------|-----------|
| Android | `system_tools`（用于 `execute_intent`） |
| Linux | `super_admin`（用于 `terminal`） |

## 测试

参考 `test_cases.md` 中的测试场景，涵盖：
- TC-A1～A3：普通网页链接、mailto 协议、自定义协议
- TC-B1～B2：B站搜索、GitHub 搜索
- TC-C1：视频流提取与本地播放
- TC-D1～D2：无效链接、短链接重定向

## 许可证

[MIT](LICENSE)
