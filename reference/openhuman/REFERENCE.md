# OpenHuman（参考项目）
> 🔗 [GitHub](https://github.com/tinyhumansai/openhuman) · [官网](https://tinyhumans.ai/openhuman) · [文档](https://tinyhumans.gitbook.io/openhuman/)
> ⭐ GitHub Trending #1 连续9天 · Product Hunt 热门

**你的个人 AI 超级智能** — 记住一切的脑子 + 编排 Agent 舰队 + 深度研究员。本地优先，简单，强大。

## 核心能力

| 能力 | 说明 | 与 gz-agent-kit 对应 |
|------|------|---------------------|
| 🧠 **Memory Tree + Obsidian Wiki** | 数据压缩为 Markdown 树存储在本地 SQLite，可开 Obsidian 编辑 | MEMORY.md + learning-records |
| 🔌 **100+ OAuth + 5000+ MCP** | 一键接入 Gmail/Notion/GitHub/Slack… | huawei_id_tool |
| 🌀 **Subconscious** | 后台循环：diff 你的世界，推进目标，写早晨简报 | cron heartbeat tasks |
| 🎯 **Goals & Todos** | 长期目标 + per-thread 目标 + Kanban | Goal Tracking |
| 🗜️ **TokenJuice** | 工具输出压缩→模型（跟 Headroom 同理念！） | Context Engineering + Headroom 参考 |
| 📁 **本地 LLM** | 处理摘要/工具等低层任务，不外泄 | — |
| 🔍 **Deep Research** | 在你的数据和全网搜索，答完前就完成 | literature-search + web-search |

## 设计理念对照

```
OpenHuman                          gz-agent-kit
─────────                         ───────────
Memory Tree (SQLite)         →    MEMORY.md + scene memory
Obsidian Wiki               →    learning-records/ (Zettelkasten)
Subconscious background     →    Heartbeat + periodic checks
Goals & Todos              →    Goal Tracking + update_goal
TokenJuice                 →    Context Engineering + Headroom
100+ OAuth                 →    huawei_id_tool
Local LLM for privacy      →    (sandbox 本地运行)
Agent Orchestration        →    sessions_spawn sub-agents
```

## 值得借鉴的点

1. **Memory Tree**：用 SQLite 存压缩 Markdown 树而非向量数据库 — 可解释、可编辑、可版本控制
2. **Subconscious 后台循环**：不只是定时任务，而是持续 diff 你的数据变化 + 推进目标
3. **Auto-fetch 每 20 分钟**：早晨就有今天的上下文，不需要手动同步
4. **TokenJuice 压缩**：跟 Headroom 一样的理念，工具输出进 LLM 前自动压缩
