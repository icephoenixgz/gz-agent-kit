# Headroom（参考项目）
> 🔗 [GitHub](https://github.com/headroomlabs-ai/headroom) · [官网](https://headroomlabs-ai.github.io/headroom) · [文档](https://headroom-docs.vercel.app/docs)
> ⭐ 近期热项目 · 压缩模型: [kompress-v2-base](https://huggingface.co/chopratejas/kompress-v2-base)

**AI Agent 上下文压缩层** — 工具输出/日志/文件/RAG 进入 LLM 前自动压缩，答案不变但 token 减少 60-95%。

## 核心能力

| 能力 | 说明 |
|------|------|
| 🔄 **Proxy 模式** | `headroom proxy` — 零代码改，透明代理 |
| 🧩 **Library 模式** | `compress(messages)` — Python/TS SDK 内联 |
| 🤖 **Agent 包装** | `headroom wrap claude/cursor/copilot/aider/openclaw` — 一行命令 |
| 🧠 **learn 模式** | 分析失败 session → 自动写 CLAUDE.md 修正行为 |
| 🗜️ **压缩算法** | SmartCrusher(JSON) + CodeCompressor(AST) + Kompress-v2(文本) |
| 🔙 **可逆压缩 (CCR)** | 原始内容本地缓存，LLM 需要时调用 `headroom_retrieve` |
| 🧲 **跨 Agent 记忆** | Claude/Codex/Gemini 共享，自动去重 |

## 在 gz-agent-kit 中的定位

### 与 AGENTS.md Context Engineering 的关系

AGENTS.md 中已有的 Context Engineering 是**手动策略**（Context Budget Awareness / 2-Action Rule / Hard Compaction），Headroom 做的是**自动执行层**：

```
AGENTS.md 策略  →  告诉我什么时候该压缩
Headroom        →  自动帮我把需要压缩的东西压缩掉
```

### 安装方式（需要时）

```bash
# uv 安装（推荐，最快）
uv tool install "headroom-ai[all]"

# pip
pip install "headroom-ai[all]"

# npm（仅 TypeScript SDK）
npm install headroom-ai

# 包装 OpenClaw
headroom wrap openclaw
```

### 适用场景
- token 预算吃紧时 → 自动降低 60-95% 消耗
- 需要跨 Agent 共享记忆 → 去重 + 压缩
- 工具输出过长（如 web_fetch 大量结果）→ 自动压缩
- 日志/文件/JSON 密集任务 → SmartCrusher / CodeCompressor
