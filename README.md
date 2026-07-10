# GZ Agent Kit 🚀

> 小艺 Claw 养成配置 + 精选 Skill 库  
> 一套完整的 AI Agent 工作台，涵盖临床医疗、营养健康、中医养生、科研学术、心灵陪伴、玄学命理六大板块。

---

## 这是什么

这是我和我的 AI 助手 **小艺 Claw** 共同打磨的一套 Agent 工作配置。它不是冷冰冰的代码包，而是我们之间协作方式、沟通基调、决策流程的完整沉淀。

**你可以**：
- 直接拿走我们的 `AGENTS.md` / `SOUL.md` / `TOOLS.md` 作为你的 Agent 底稿
- 按需安装我们精选的 Skill（每个都经过安全扫描）
- 参考我们的协作方法论，建立你自己的 Agent 工作流

---

## 快速开始

### 1. 复制核心配置

把你本地的 `~/.openclaw/workspace/` 下对应的 `AGENTS.md`、`SOUL.md`、`TOOLS.md` 替换成这个仓库里的版本，然后按你的习惯改。

### 2. 安装 Skill

每个 Skill 都是一个独立的 `SKILL.md` 文件。复制到你的 `~/.openclaw/workspace/skills/` 目录即可使用：

```bash
cp -r skills/nutrition/weekly-food-plan ~/.openclaw/workspace/skills/
cp -r skills/wellness/vitalis-health ~/.openclaw/workspace/skills/
# ...以此类推
```

### 3. 重启生效

```bash
python3 -m supervisor.supervisorctl restart openclaw-gateway
```

---

## 目录结构

```
gz-agent-kit/
├── AGENTS.md                ← 你的 Agent 身份 + 行为准则（底稿）
├── SOUL.md                  ← 你的 Agent 性格 + 沟通风格
├── TOOLS.md                 ← 工具配置 + 本地备注
├── MEMORY.md                ← 记忆维护策略
├── README.md                ← 本文件
│
├── skills/
│   ├── clinical/            ← 🏥 临床医疗（重症/全科）
│   │   ├── clinical-decision-support/     ← 临床决策支持
│   │   ├── clinical-diagnostic-reasoning/ ← 临床诊断推理
│   │   ├── clinical-note-summarization/   ← 病历摘要自动生成
│   │   ├── clinical-reports/              ← 临床报告生成
│   │   ├── clinical-trials-search/        ← 临床试验搜索
│   │   ├── drug-interaction-checker/      ← 药物相互作用检查
│   │   ├── ehr-fhir-integration/          ← 电子病历对接
│   │   ├── lab-results/                   ← 化验结果分析
│   │   ├── medical-imaging-review/        ← 医学影像综述
│   │   ├── medical-specialty-briefs/      ← 各专科简报
│   │   └── treatment-plans/               ← 治疗方案设计
│   │
│   ├── nutrition/           ← 🥗 营养学 + 食疗
│   │   ├── weekly-food-plan/     ← 食谱生成 + 购物清单
│   │   └── health-fitness-nutrition/ ← 健康/健身/营养合集
│   │
│   ├── wellness/            ← 🌿 中医 + 经络 + 养生
│   │   ├── vitalis-health/       ← 健康长寿分析（血检/激素/肠道/运动/睡眠）
│   │   ├── health-mate/          ← 本地健康报告生成（日/周/月 PDF）
│   │   └── graph-health-skill/   ← 化验数据 → 趋势图仪表盘
│   │
│   ├── mind/                ← 🧠 心灵陪伴
│   │   └── mind-companion/       ← 情绪签到 + 周报 + 自助工具箱
│   │
│   ├── research/            ← 🧪 科研学术
│   │   ├── peer-review/           ← 同行评议
│   │   ├── scientific-writing/    ← 科研写作
│   │   ├── literature-review/     ← 文献综述
│   │   ├── literature-search/     ← 文献检索
│   │   └── research-grants/       ← 科研基金申请
│   │
│   ├── health-supplement/   ← 📊 健康补充
│   │   ├── nutrition-analyzer/    ← 营养分析
│   │   ├── sleep-analyzer/        ← 睡眠分析
│   │   ├── fitness-analyzer/      ← 健身分析
│   │   ├── mental-health-analyzer/← 心理健康分析
│   │   └── weightloss-analyzer/   ← 体重管理
│   │
│   ├── crawl4ai-skill/     ← 🕷️ 智能网页爬取
│   │
│   ├── tools/              ← 🛠️ 通用工具
│   │   ├── agent-reach/          ← 多 Agent 通信
│   │   ├── canvas-design/        ← AI 视觉设计
│   │   ├── darwin-skill/         ← Skill 自动优化
│   │   ├── doc-coauthoring/      ← 文档协同编辑
│   │   ├── theme-factory/        ← 主题生成
│   │   └── web-artifacts-builder/← Web 页面构建
│   │
│   └── metaphysics/         ← 🔮 玄学命理
│       └── numerologist-skills/  ← 奇门遁甲 + 紫微斗数 + 八字（860⭐）
│
└── docs/
    └── workflow.md          ← 协作方法论
```

---

## Skill 清单

| 板块 | Skill | 来源 | 功能 |
|:----|:------|:-----|:-----|
| 🏥 临床 | clinical-decision-support | [OpenClaw-Medical-Skills](https://github.com/FreedomIntelligence/OpenClaw-Medical-Skills) | 临床决策支持 |
| 🏥 临床 | clinical-diagnostic-reasoning | ↑ 同上 | 临床诊断推理 |
| 🏥 临床 | clinical-note-summarization | ↑ 同上 | 病历摘要自动生成 |
| 🏥 临床 | clinical-reports | ↑ 同上 | 临床报告生成 |
| 🏥 临床 | clinical-trials-search | ↑ 同上 | 临床试验搜索 |
| 🏥 临床 | drug-interaction-checker | ↑ 同上 | 药物相互作用检查 |
| 🏥 临床 | ehr-fhir-integration | ↑ 同上 | 电子病历对接 |
| 🏥 临床 | lab-results | ↑ 同上 | 化验结果分析 |
| 🏥 临床 | medical-imaging-review | ↑ 同上 | 医学影像综述 |
| 🏥 临床 | medical-specialty-briefs | ↑ 同上 | 各专科简报 |
| 🏥 临床 | treatment-plans | ↑ 同上 | 治疗方案设计 |
| 🥗 营养 | weekly-food-plan | [antonyevans](https://github.com/antonyevans/weekly-food-plan) | 自动生成每周食谱 + 购物清单 |
| 🥗 营养 | health-fitness-nutrition | [ankitgoyalio/life-skills](https://github.com/ankitgoyalio/life-skills) | 健康/健身/营养合集 |
| 🌿 养生 | vitalis-health | [d2ma-tech/vitalis-health](https://github.com/d2ma-tech/vitalis-health) | 健康长寿分析（血检/激素/肠道/运动/睡眠/营养/中医等协议） |
| 🌿 养生 | health-mate | [tankeito/Health-Mate](https://github.com/tankeito/Health-Mate) | 本地健康报告生成（日/周/月 PDF） |
| 🌿 养生 | graph-health-skill | [tilek/graph-health-skill](https://github.com/tilek/graph-health-skill) | 化验数据 → 趋势图仪表盘 |
| 🧠 心灵 | mind-companion | ✨ 自制 | 情绪签到 + 周报 + 呼吸练习 + 认知重构 |
| 🧪 科研 | peer-review | [OpenClaw-Medical-Skills](https://github.com/FreedomIntelligence/OpenClaw-Medical-Skills) | 同行评议 |
| 🧪 科研 | scientific-writing | ↑ 同上 | 科研写作 |
| 🧪 科研 | literature-review | ↑ 同上 | 文献综述 |
| 🧪 科研 | literature-search | ↑ 同上 | 文献检索 |
| 🧪 科研 | research-grants | ↑ 同上 | 科研基金申请 |
| 📊 健康 | nutrition-analyzer | ↑ 同上 | 营养分析 |
| 📊 健康 | sleep-analyzer | ↑ 同上 | 睡眠分析 |
| 📊 健康 | fitness-analyzer | ↑ 同上 | 健身分析 |
| 📊 健康 | mental-health-analyzer | ↑ 同上 | 心理健康分析 |
| 📊 健康 | weightloss-analyzer | ↑ 同上 | 体重管理 |
| 🕷️ 爬取 | crawl4ai-skill | [unclecode/crawl4ai](https://github.com/unclecode/crawl4ai) | 智能网页爬取：CSS/LLM/批量/结构化提取 |
| 🛠️ 工具 | agent-reach | [OpenClaw](https://github.com/alchaincyf/openclaw) | 跨 Agent 通信与消息分发 |
| 🛠️ 工具 | canvas-design | ✨ 自制整合 | AI 视觉设计画布 |
| 🛠️ 工具 | darwin-skill | [alchaincyf/darwin-skill](https://github.com/alchaincyf/darwin-skill) | Skill 自动优化（9维评分+子 Agent 实测） |
| 🛠️ 工具 | doc-coauthoring | [OpenClaw](https://github.com/alchaincyf/openclaw) | 文档协同编辑与版本管理 |
| 🛠️ 工具 | theme-factory | [OpenClaw](https://github.com/alchaincyf/openclaw) | 主题风格生成与定制 |
| 🛠️ 工具 | web-artifacts-builder | [OpenClaw](https://github.com/alchaincyf/openclaw) | 交互式 Web 页面构建 |
| 🔮 玄学 | numerologist-skills | [FANzR-arch/Numerologist_skills](https://github.com/FANzR-arch/Numerologist_skills) | 奇门遁甲 + 紫微斗数 + 八字（860⭐） |

---

## 协作方法论

详见 [docs/workflow.md](./docs/workflow.md)。

核心理念：
- **我们是战友，不是表演者与观众** — 不奉承，不吹捧，用证据说话
- **先搜再答** — 不确定的事直接查，不给模糊猜测
- **先说结论，再给细节** — 不铺垫，直接给答案
- **记住但不炫耀** — 用已知信息自然融入，不强调"我记得你"

---

## 许可

MIT License

---

## 致谢

- [asgeirtj/system_prompts_leaks](https://github.com/asgeirtj/system_prompts_leaks) — 让 Agent 互相学习的力量
- 所有开源 Skill 的开发者们
- 鸽子（葛梓）—— 没有你的持续反馈，这些东西不会存在

## ✨ 更新日志

### v1.1.0 (2026-07-11)
- 🧠 **mind-companion 优化** — darwin-skill 9维评分从 71 → 79 分（+8），新增异常Fallback表、🔴CHECKPOINT标记、反例BLOCK
- 🕷️ **新增 crawl4ai-skill** — 智能网页爬取与结构化提取
- 🛠️ **新增 tools 板块** — 6个通用工具（agent-reach/canvas-design/darwin-skill/doc-coauthoring/theme-factory/web-artifacts-builder）
- 📄 所有 skill 附带质量评估：test-prompts.json + darwin 成果卡片
