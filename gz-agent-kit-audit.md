# GZ Agent Kit — 代码审计报告

**项目：** gz-agent-kit
**审计日期：** 2026-07-14
**模式：** architecture + maintainability + security
**报告语言：** 中文

---

## 📊 评分面板

| 维度 | 评分 | 等级 |
|------|:----:|:----:|
| 架构 (Architecture) | 8.5 | S |
| 可维护性 (Maintainability) | 8.0 | S |
| 安全 (Security) | 9.5 | S |
| **总分** | **8.7** | **S** |

---

## 项目画像

| 属性 | 内容 |
|------|------|
| **项目类型** | AI Agent 工作台 + Skill 集合 |
| **核心语言** | Markdown（268 个 .md 文件，约 70K 行）+ Python（44 个 .py 文件） |
| **技能数量** | 19 个板块，7 个独立 Skill 文件 + 大量内嵌 Skill |
| **文件总量** | ~380 个文件 |
| **构建配置** | 无 package.json / requirements.txt / 依赖锁文件 |
| **许可协议** | MIT |

---

## 一、架构审计

### ✅ 优点

1. **清晰的分层结构** — 根目录只有 5 个核心文件（AGENTS.md / README.md / MEMORY.md / SOUL.md / TOOLS.md），skills/ 和 reference/ 分开放，职责分明。
2. **可扩展设计** — 每个 skill 独立目录，互不依赖。新增一个 skill = 建个目录塞文件，零耦合。
3. **README 索引完整** — 47 个 skill 按 12 大板块分门别类，用户一目了然。

### ⚠️ 关注点（不严重，但值得注意）

| # | 问题 | 严重程度 | 建议 |
|---|------|---------|------|
| 1 | **无 package.json / requirements.txt / pyproject.toml** | Low | 如果技能中包含 Python 脚本（44 个 .py），建议在根目录加一个 `requirements.txt` 说明运行依赖 |
| 2 | **skills/metaphysics/ 空目录** | Low | 清掉或放占位 README |
| 3 | **无测试文件** | Low | 作为 OpenClaw skill 集合，测试不是强需求，但如果有 Python 脚本的测试会更完整 |

---

## 二、可维护性审计

### ✅ 优点

1. **命名规范** — 目录和文件名一致使用 kebab-case，可读性好
2. **文档完整** — 每个 skill 基本都有 SKILL.md，README 和 reference 文件齐全
3. **文件体积健康** — 绝大部分 skill 的正文在 500-1500 行，可控
4. **无深层嵌套代码** — 整个项目以 markdown prompt 为主，没有复杂的逻辑嵌套

### ⚠️ 关注点

| # | 问题 | 严重程度 | 建议 |
|---|------|---------|------|
| 1 | **最大的单个文件 5,970 行** | Medium | `skills/crawl4ai-skill/references/complete-sdk-reference.md` 接近 6000 行。如果这是完整 SDK 文档，建议分拆或只引用官方文档链接 |
| 2 | **4 个 .sh 脚本没有执行权限标记** | Low | `chmod +x` 一下即可 |
| 3 | **AGENTS.md 与根目录 AGENTS.md 内容重复** | Medium | gz-agent-kit 根目录有一份 AGENTS.md 是 OpenClaw 配置，skills 内有自己的参考格式，注意不要混淆。README 建议补充说明这份 AGENTS.md 的用途 |

---

## 三、安全审计

### ✅ 优点

1. **无硬编码密钥** — 搜索全项目代码，未发现 token / API key / password 等凭证硬编码
2. **无敏感文件** — .env、credentials、key 文件均不在版本控制中
3. **Python 脚本无 OS command injection** — `subprocess` 调用均使用列表形式而非 shell string

### ⚠️ 关注点

| # | 问题 | 严重程度 | 建议 |
|---|------|---------|------|
| 1 | **README 无安全性说明** | Low | 建议加一段小提示，提醒用户不要往 Skill 文件里写 API Key |
| 2 | **无依赖锁定** | Low | `.gitignore` 中未排除 node_modules / .env 等模式——从文件列表看它们不在 repo 中是好的，但建议明确加到 `.gitignore` |

---

## 覆盖矩阵

| 维度 | 覆盖置信度 | 已检内容 | 未检范围 |
|------|:---------:|---------|---------|
| 架构 | High | 目录结构、模块边界、依赖方向 | — |
| 可维护性 | High | 文件大小、命名规范、文档完整性 | 单个 skill 内部的代码风格一致性（样本检查） |
| 安全 | High | 硬编码密钥扫描、敏感文件检查、injeciton 扫描 | Python 脚本的完整运行时测试 |

---

## 总结

**GZ Agent Kit 是一个非常健康的 AI Agent Skill 集合。** 不需要"修山"——它没有明显的屎山问题。

评分 S（8.7/10）的理由：
- 架构干净、扩展友好
- 文档覆盖率高
- 安全无隐患
- 项目风格统一、易于维护

**最值得优化的 3 件事（优先级排序）：**
1. 拆一下那个 6000 行的 SDK reference 文件
2. 加上 requirements.txt 和 .gitignore
3. README 中补充安全性提示
