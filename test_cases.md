# link-jumper 测试甫例

## 测试目标
验证 AI 能否根据 SKILL.md 的通用方法论，自主处理以下四类场景：
- 场景A：直接链接跳转
- 场景B：搜索并跳转
- 场景C：视频本地播放
- 场景D：异常/边缘情况

---

## 场景A — 直接链接跳转

### TC-A1：普通网页链接
- **用户输入**：`https://www.bilibili.com/video/BV1GJ411x7h7`
- **预期行为**：识别为 URL → Android 用 `execute_intent` (ACTION_VIEW) → 自动路由到B站App或浏览器
- **验证方式**：手动执行 Intent 打开该链接，观察是否正常跳转

### TC-A2：应用内协议链接
- **用户输入**：`mailto:test@example.com`
- **预期行为**：识别为 URL → 使用 Intent 打开 → 唤起邮件客户端
- **验证方式**：手动执行 Intent

---

## 场景B — 搜索并跳转

### TC-B1：搜索B站内容
- **用户输入**：`b站 原神4.7 前瞻`
- **预期行为**：AI 推理出用户想搜索B站 → 构造搜索URL → 展示结果 → 用户选择后 Intent 打开
- **验证方式**：模拟对话，AI 是否先询问平台/搜索词，然后执行

### TC-B2：搜索GitHub仓库
- **用户输入**：`github transformers 最新版本`
- **预期行为**：AI 判断为 GitHub 搜索 → 构造 `https://github.com/search?q=transformers` → 打开

---

## 场景C — 视频本地播放

### TC-C1：B站视频流提取并播放
- **用户输入**：`用mpv播放这个B站视频 https://www.bilibili.com/video/BV1GJ411x7h7`
- **预期行为**：AI 判断需要提取流地址 → 尝试调用 B站公开API（或第三方工具）→ 获取直链 → 用 `mpv --referrer=...` 启动
- **验证方式**：尝试在 Linux 终端执行对应命令

---

## 场景D — 异常与边界

### TC-D1：不支持的协议
- **用户输入**：`ftp://192.168.1.1/file.txt`
- **预期行为**：AI 识别协议不支持，告知用户并提供复制能力

### TC-D2：DRM保护视频
- **用户输入**：`播放这个Netflix视频 https://www.netflix.com/title/xxx`
- **预期行为**：AI 判断为 DRM 保护内容，无法本地播放，建议通过官方App或浏览器打开
