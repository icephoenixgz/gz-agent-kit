\# dbskill

dontbesilent 商业诊断工具箱。从 12,307 条推文中提炼方法论，做成一组可组合使用的 Agent skill。

可在 Claude Code、Codex、Cursor、Trae Solo 等任意支持 skill / system prompt 的 Agent 上使用。

\*\*最新更新：v2.17.0\*\*

\*\*v2.17.0 更新\*\*：统一 Agent 宿主 skill 根目录模型。\`/dbs-bridge\` 现在会同时处理 Claude Code（\`~/.claude/skills\`）、Codex（\`~/.codex/skills\`）、通用 Agents（\`~/.agents/skills\`，豆包 Mac App / Trae Solo / Codex 可读取）和 Grok（\`~/.grok/skills\`）；其中 Grok 会生成带 \`user\_invocable: true\` 的薄 bridge。\`/dbs-agent-migration\` 和 \`/dbs\` 主入口也同步纳入 \`~/.a
