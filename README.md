# 🚀 DesignArena-2Api: 边缘计算时代的视觉创作黑盒解构 🎨

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Cloudflare Workers](https://img.shields.io/badge/Platform-Cloudflare%20Workers-orange.svg)](https://workers.cloudflare.com/)
[![OpenAI Compatible](https://img.shields.io/badge/API-OpenAI%20Compatible-green.svg)](https://platform.openai.com/docs/api-reference)

> **「技术不应是高墙，而应是通往无限可能的阶梯。」** —— 本项目秉持 F1 赛车级极致响应理念，将复杂的 Web 逆向工程转化为优雅的生产力工具。

---

### 🌐 快速导航
- **在线体验 (Live Demo):** [立即进入驾驶舱 ⚡](https://designarena-2api.to2ai.workers.dev/)
- **GitHub 仓库:** [lza6/designarena-2api-cfwork](https://github.com/lza6/designarena-2api-cfwork)
- **一键部署:** [![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/lza6/designarena-2api-cfwork)

---

## 💎 项目愿景与哲学 (Project Vision)

在 AI 浪潮汹涌的今天，我们不仅是代码的搬运工，更是数字世界的解构者。`DesignArena-2Api` 的诞生，不仅仅是为了将一个网站变成一个接口，它是对 **「开发者体验 (DX)」** 的一次深耕。

我们采用了 **F1-Cockpit (驾驶舱)** 的设计理念：
- **信息密集 (Data-Rich):** 每一毫秒的延迟、每一个 Trace ID、每一次心跳都在掌握之中。
- **响应迅捷 (Reactive):** 边缘计算带来的近乎零的物理延迟。
- **绝对可靠 (Rock-Solid):** 即使面对上游的波动，也有健壮的 SSE 心跳层保驾护航。

这不仅是一个工具，更是一种开源精神的传递：**「如果你觉得世界不够完美，那就动手去重塑它。」** 🛠️

---

## ✨ 核心特性与技术亮点 (Features)

### 1. 动态凭证穿透 (JWT Passthrough) 🔑
**【原创黑科技】** 突破了传统 API 代理必须在服务器端配置 Token 的局限。你只需在客户端（如 LobeChat）的 API Key 中填入官网抓取的 `ey...` 开头长效 JWT，系统会自动识别并实现无感透传。

### 2. 原生 SSE 心跳保活 (Heartbeat Keep-Alive) 💓
针对生成图片长达 10-20 秒的等待期，内置了 1秒频率的 SSE 注释流心跳。有效绕过 Cloudflare/Vercel 的 `524 Timeout` 限制，确保连接永不断连。

### 3. 全链路图生图解析 (Full Image-to-Image Flow) 📸
完美复刻官方多步上传逻辑：
`请求上传链接` -> `直接 PUT 投递到云存储` -> `提交存储路径到竞技场` -> `触发渲染`。

### 4. F1-Cockpit 开发者面板 V2 🏎️
内置基于 **Web Components & Shadow DOM** 的交互式 UI。支持本地 `localStorage` 历史记录自动持久化，重启浏览器，灵感依旧在。

---

## 🛠️ 懒人一键安装教程 (Lazy-Person Deployment)

### 方案 A：云端一键发射 (推荐) 🚀
1. 点击上方的 **[Deploy to Cloudflare Workers]** 蓝色按钮。
2. 登录你的 Cloudflare 账号。
3. 点击部署，你将获得一个属于自己的 API 终端。

### 方案 B：手动硬核部署 (Manual) 🛠️
1. 复制本项目中的 `cfwork.js` 代码。
2. 在 Cloudflare Workers 控制台创建一个新 Worker。
3. 粘贴代码并部署。
4. **关键步骤：** 在【设置】->【变量】中添加 `API_MASTER_KEY`。
    - *值：* 填入抓包获得的 `ey...` Token。

---

## 🔬 技术原理与逻辑解构 (Technical Mechanics)

### 1. 文件结构蓝图 (File Structure)
为了方便 AI 爬虫及后续开发者快速上手，本项目保持了极简的结构：
```text
/
├── cfwork.js             # 🚀 核心逻辑：包含路由、代理、UI、SSE 等所有功能（单文件战神）
├── README.md             # 🗺️ 导航地图（你正在看的文件）
├── LICENSE               # ⚖️ 阿帕奇 2.0 开源协议
├── DesignArena-2ApiF12抓包记录/    # 🧪 研究实验室：记录了所有原始请求包格式
└── DesignArena-2Api网站源代码/      # 📚 参考文献：官网前端逻辑的反汇编参考
```

### 2. 核心算法与方法说明
- **`executeDesignArenaFlow`**: 任务执行核心。采用 **异步串行模式** 控制三阶段任务（上传、加会话、生成）。
- **`uploadImageToDesignArena`**: 素材同步算法。支持 Base64 和 URL 互转，自动处理 MIME 类型。
- **`handleWebUI`**: 采用 **Shadow DOM** 技术实现的 UI 隔离，确保 CSS 不会污染外部环境，性能极高。
- **`createJsonResponse`**: 封装了 Brotli 压缩响应头，提升边缘传输效率。

---

## 🌈 使用场景 (Scenarios)

- **AI 绘画爱好者**: 配合 LobeChat 或 Cherry Studio，享受官方级生图体验。
- **自动化集成**: 在 ComfyUI 或 Midjourney Bot 中作为 DALL-E 3 的平替接口。
- **学术研究**: 学习 Cloudflare Workers 如何处理复杂的 Web 异步逆向流。

---

## 🚧 现状与未来扩展 (Roadmap)

### 现阶段成果：
- [x] 兼容 OpenAI Chat/Image 协议。
- [x] 图生图 (I2I) 链路全打通。
- [x] 开发者驾驶舱 UI 完备。

### 待优化/不足点：
- [ ] **多账号轮询**: 目前单实例主要针对单 Key 或透传，未来可增加本地 KV 存储实现多 Key 自动调度。
- [ ] **模型增强**: 官方支持更多模型（如 GPT-4V），目前代理层已预留接口，但需更精细的消息映射。
- [ ] **指纹库动态化**: 目前 User-Agent 固定，未来可引入动态指纹生成。

---

## ⚖️ 开源协议与价值观

本项目基于 **Apache License 2.0** 协议开源。

我们相信：**「代码是自由的，而分享是文明进步的燃料。」**
在使用本项目时，请遵守当地法律法规，尊重版权。如果你从中受益，请给作者一个 **Star** ⭐，这不仅是认可，更是开源精神的火种传递。

---

## 🤝 开发者共建、AI 友好提示

如果你是一位开发者，或者你正在指导一位 AI 助手改进此项目，请关注 `cfwork.js` 中的 `CONFIG` 字典。所有的逻辑扩展点都预留在 `handleApi` 函数中。

> **「星辰大海，始于足下。来吧，亲自动手写下一行代码，你会发现，你也能行！」** ✨

---
*Created with ❤️ by lza6 & Antigravity AI*
