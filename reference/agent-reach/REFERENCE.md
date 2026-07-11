# Agent Reach（参考项目 / v2 升级版）
> 🔗 [GitHub](https://github.com/Panniantong/agent-reach) · ⭐ 54,700+
> 国内镜像：[AtomGit](https://atomgit.com/qq_51337814/Agent-Reach)  
> 安装文档：`docs/install.md` · 更新文档：`docs/update.md`

**给你的 AI Agent 一键装上互联网能力** — 读推特/搜 Reddit/看 YouTube/B站/小红书/全网搜索，一句话搞定。

## 与 tools/agent-reach 的关系

当前 tools/agent-reach（SKILL.md 4.5KB）是旧版 OpenClaw 内置的搜索包装器。
原项目 Panniantong/Agent-Reach（⭐54.7k）是更完整的**联网能力工具箱**，通过 agent-reach 命令提供：

- 30+ 平台支持，统一接口
- `agent-reach doctor` 诊断
- 持续迭代：平台封了它修，有新渠道它加
- 多后端路由 + 备选方案（平台变化用户无感）

## 核心能力

| 平台 | 装好即用 | 需配置（自动引导） |
|------|---------|-----------------|
| 🌐 网页 | ✅ 阅读任意网页 | — |
| 📺 YouTube | ✅ 字幕+搜索 | — |
| 📡 RSS | ✅ 任意 RSS/Atom | — |
| 🔍 全网搜索 | — | ✅ 免费自动配置 |
| 📦 GitHub | ✅ 公开仓库 | ✅ 私有/Issue/PR |
| 🐦 Twitter/X | ✅ 单条推文 | ✅ 搜索/时间线 |
| 📺 B站 | ✅ 搜索+详情 | ✅ 字幕 |
| 📕 小红书 | — | ✅ OpenCLI |
| 📖 Reddit | — | ✅ Cookie |
| 📈 雪球 | ✅ 行情/热帖 | — |

## 安装方式

```bash
# 自动安装（把你的 Agent 复制过去即可）
agent-reach install

# 或手动克隆
pip install agent-reach  # pip 方式
# 或 uv 安装
uv tool install agent-reach
```

## 在 gz-agent-kit 中的定位

- **tools/agent-reach**：保持当前 OpenClaw 内置 SKILL.md 不变（小艺搜索的轻量入口）
- **reference/agent-reach**：完整版的安装 + 能力文档存档
- 如需更全面的联网能力，运行 `agent-reach install` 升级到 v2
