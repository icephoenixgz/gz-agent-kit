<div align="center">
  <h1>🛸 GZ Agent Kit</h1>
  <p><strong>你的 AI 工作台 · 53 个精选 Skill · 12 大板块</strong></p>
  <p><em>小艺 Claw 养成配置 + 精选 Skill 库 — 一套陪你成长的 Agent 工作台</em></p>
  <p>
    <a href="#-skill-清单"><img src="https://img.shields.io/badge/Skills-53-blue" alt="Skills"></a>
    <a href="#-板块"><img src="https://img.shields.io/badge/Categories-12-brightgreen" alt="Categories"></a>
    <a href="https://github.com/icephoenixgz/gz-agent-kit/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-MIT-green" alt="License"></a>
    <a href="#"><img src="https://img.shields.io/badge/Maintained-Yes-ff69b4" alt="Maintained"></a>
  </p>
  <p>
    <sub>作者 <a href="https://github.com/icephoenixgz">@icephoenixgz</a>（鸽子 / 白大褂鸽子） · ✨ 小艺 Claw</sub>
  </p>
  <br>
</div>

---

## 🎯 这是什么

这是鸽子（葛梓）和他的 AI 助手 **小艺 Claw** 共同打磨的一套 Agent 工作配置。不是冷冰冰的代码包，而是我们之间协作方式、沟通基调、决策流程的完整沉淀。

**你可以**：
- 📋 拿走 `AGENTS.md` / `SOUL.md` / `TOOLS.md` 作为底稿，快速搭建你自己的 Agent
- 🧩 按需安装 47 个精选 Skill（每个都经过质量评估）
- 💡 参考我们的协作方法论，建立你自己的 Agent 工作流

---

## 🚀 快速开始

```bash
# 1. 复制核心配置
cp -r skills/* ~/.openclaw/workspace/skills/

# 2. 重启生效
python3 -m supervisor.supervisorctl restart openclaw-gateway

# 3. 开箱即用
# 试试："帮我做临床决策"、"写一篇小红书笔记"、"教我营养学"...
```

---

## 📐 十二大板块

```
🏥 临床     🥗 营养     🌿 养生     🧠 心灵
🧪 科研     📊 健康     📝 内容     🧠 人物视角
🎬 视频     🏢 运营     🔮 玄学     🛠️ 工具
🎓 学习                              📋 参考项目
```

从临床到玄学，从学习到运营——**围绕你（ICU医生·专利撰写者·终身学习者）的真实需求精筛**，不堆数量。

---

## 📦 目录结构

```
gz-agent-kit/
├── AGENTS.md          ← Agent 身份 + 行为准则
├── SOUL.md            ← Agent 性格 + 沟通风格
├── TOOLS.md           ← 工具配置 + 本地备注
├── MEMORY.md          ← 记忆维护策略
├── README.md          ← ← 你正在看这个
│
├── skills/            ← 🧩 Skill 仓库（53 个）
│   ├── clinical/      ← 🏥 临床医疗 ICU/全科（11 个）
│   ├── nutrition/     ← 🥗 营养学 + 食疗（2 个）
│   ├── wellness/      ← 🌿 中医 + 养生（3 个）
│   ├── mind/          ← 🧠 心灵陪伴（1 个）
│   ├── research/      ← 🧪 科研学术（7 个）
│   ├── health-supplement/ ← 📊 健康分析补充（5 个）
│   ├── content/       ← 📝 内容创作（4 个）
│   ├── oracles/       ← 🧠 人物视角（2 个）
│   ├── video/         ← 🎬 视频创作（6 个）
│   ├── operations/    ← 🏢 商业运营（1 个）
│   ├── learning-system/ ← 🎓 学习引擎
│   ├── metaphysics/   ← 🔮 玄学命理
│   ├── tools/         ← 🛠️ 通用工具（11 个）
│   └── crawl4ai-skill/← 🕷️ 爬取
│
└── reference/         ← 📋 参考项目
    ├── patent-disclosure-skill/  ← 专利交底书生成
    ├── money-printer-turbo/      ← 短视频自动成片
    └── mattpocock-teach/         ← Matt Pocock 教学理念源文件
```

---

## 🧩 Skill 清单

### 🏥 临床医疗（ICU / 全科）

| Skill | 说明 | ⭐ 来源 |
|:------|:-----|:-------|
| **clinical-decision-support** | 临床决策支持 | [FreedomIntelligence](https://github.com/FreedomIntelligence/OpenClaw-Medical-Skills) |
| **clinical-diagnostic-reasoning** | 临床诊断推理 | ↑ |
| **clinical-note-summarization** | 病历摘要自动生成 | ↑ |
| **clinical-reports** | 临床报告生成 | ↑ |
| **clinical-trials-search** | 临床试验搜索 | ↑ |
| **drug-interaction-checker** | 药物相互作用检查 | ↑ |
| **ehr-fhir-integration** | 电子病历对接 | ↑ |
| **lab-results** | 化验结果分析 | ↑ |
| **medical-imaging-review** | 医学影像综述 | ↑ |
| **medical-specialty-briefs** | 各专科简报 | ↑ |
| **treatment-plans** | 治疗方案设计 | ↑ |

### 🥗 营养 + 🌿 养生

| Skill | 说明 | ⭐ 来源 |
|:------|:-----|:-------|
| **weekly-food-plan** | 每周食谱 + 购物清单 | [antonyevans](https://github.com/antonyevans/weekly-food-plan) |
| **health-fitness-nutrition** | 健康/健身/营养合集 | [ankitgoyalio/life-skills](https://github.com/ankitgoyalio/life-skills) |
| **vitalis-health** | 健康长寿分析（血检/激素/肠道/运动） | [d2ma-tech/vitalis-health](https://github.com/d2ma-tech/vitalis-health) |
| **health-mate** | 本地健康报告（日/周/月 PDF） | [tankeito/Health-Mate](https://github.com/tankeito/Health-Mate) |
| **graph-health-skill** | 化验数据 → 趋势图仪表盘 | [tilek/graph-health-skill](https://github.com/tilek/graph-health-skill) |

### 🧠 心灵 + 🧪 科研 + 📊 健康分析

| Skill | 说明 | ⭐ 来源 |
|:------|:-----|:-------|
| **mind-companion** ✨自制 | 情绪签到 + 周报 + 呼吸练习 | 9维darwin评分79 |
| **peer-review** | 同行评议 | [FreedomIntelligence](https://github.com/FreedomIntelligence/OpenClaw-Medical-Skills) |
| **scientific-writing** | 科研写作 | ↑ |
| **literature-review** | 文献综述 | ↑ |
| **literature-search** | 文献检索 | ↑ |
| **research-grants** | 科研基金申请 | ↑ |
| **paper-lookup** ✨增强 | 12库学术检索（含中文知网/万方/维普 + Zenodo） | [alfonso0512](https://github.com/alfonso0512/academic-search-skill) 吸收整合 |
| **hv-analysis** | 竞品深度分析，万字报告（纵向历史+横向对比） | [KKKKhazix](https://github.com/KKKKhazix/khazix-skills) |
| **nutrition-analyzer** | 营养分析 | ↑ |
| **sleep-analyzer** | 睡眠分析 | ↑ |
| **fitness-analyzer** | 健身分析 | ↑ |
| **mental-health-analyzer** | 心理健康分析 | ↑ |
| **weightloss-analyzer** | 体重管理 | ↑ |

### 📝 内容创作

| Skill | 说明 | ⭐ 来源 |
|:------|:-----|:-------|
| **guizang-social-card-skill** | 社交卡片 / 小红书轮播 / 公众号封面 | [op7418](https://github.com/op7418/guizang-social-card-skill) |
| **ian-xiaohei-illustrations** | 小黑手绘风正文配图 🏆7.5k⭐ | [helloianneo](https://github.com/helloianneo/ian-xiaohei-illustrations) |
| **humanizer-zh** | 去 AI 机味（16种AI模式识别） | [op7418/humanizer-zh](https://github.com/op7418/humanizer-zh) |
| **remove-ai-flavor-skill** | 模板句改造 + 措辞自然化 | [B1lli/remove-ai-flavor-skill](https://github.com/B1lli/remove-ai-flavor-skill) |

### 🧠 人物视角（Oracles）

| Skill | 说明 | ⭐ 来源 |
|:------|:-----|:-------|
| **god-skill** | 输入人名 → 7层蒸馏 → 可运行人物Skill | [fattly/god-skill](https://github.com/fattly/god-skill) |
| **zeng-guofan-perspective** | 曾国藩 · 知行操作系统 | ✨ 自制（364行，7层输出） |

### 🎬 视频创作

| Skill | 说明 | ⭐ 来源 |
|:------|:-----|:-------|
| **chengfeng-videocut-skill** | 口播剪辑全自动 | [chengfeng2023](https://github.com/chengfeng2023/videocut-skill) |
| **bibigpt-skill** | 30+平台视频结构化拆解 | [bibigpt/bibigpt-skill](https://github.com/BibiGPT-team/bibigpt-skill) |
| **good-broll** | B-roll 画面方案 + AI提示词 | [goodbroll/good-broll](https://github.com/goodbroll/good-broll) |
| **narrator-ai-cli-skill** | 电影解说8步全自动 | [narrator-ai](https://github.com/narrator-ai/narrator-ai-cli) |
| **remotion-video-skill** | React代码写视频（动画/字幕/3D） | [remotion-dev/remotion](https://github.com/remotion-dev/remotion) |
| **OpenMontage-video-factory** | 开源Agent视频工厂 | [ProjectOpenMontage](https://github.com/ProjectOpenMontage/OpenMontage-video-factory) |

### 🏢 商业运营 + 🎓 学习 + 🛠️ 工具

| Skill | 说明 | ⭐ 来源 |
|:------|:-----|:-------|
| **dbskill** (24个子skill) | 一人公司商业诊断工具箱 🏆7.6k⭐ | [dontbesilent2025/dbskill](https://github.com/dontbesilent2025/dbskill) |
| **learning-system** ✨自制 | 小艺双向学习引擎（Teach+Zettelkasten+Open Notebook） | Teach理念整合 |
| **crawl4ai-skill** | 智能网页爬取（CSS/LLM/批量） | [unclecode/crawl4ai](https://github.com/unclecode/crawl4ai) |
| **agent-reach** | 跨Agent通信 | [OpenClaw](https://github.com/alchaincyf/openclaw) |
| **darwin-skill** | Skill自动优化（9维评分+实测） | [alchaincyf/darwin-skill](https://github.com/alchaincyf/darwin-skill) |
| **theme-factory** | 主题风格生成 | [OpenClaw](https://github.com/alchaincyf/openclaw) |
| **web-artifacts-builder** | Web页面构建 | [OpenClaw](https://github.com/alchaincyf/openclaw) |
| **aihot** 🆕 | 一句话查AI圈最新动态（免费，无需Key） | [KKKKhazix](https://github.com/KKKKhazix/khazix-skills) |
| **pua-skill** 🆕 | 专治Agent摆烂 — 高压推进，强制换思路 | [tanweai/pua](https://github.com/tanweai/pua) |
| **ashan-skill-creator** 🆕 | 用嘴描述需求自动生成Skill | [ashans](https://github.com/ashans/ashan-skill-creator) |
| **naiyue-thinking** 🆕 ✨自制 | 12条思考纪律：先标证据、再给结论、最小可用路径 | 吸收 naiyue-skills 思路自制 |

### 📋 参考项目

| 项目 | 说明 | 板块 |
|:-----|:-----|:----|
| **patent-disclosure-skill** 🏆3.7k⭐ | 专利挖掘→查新→交底书→自检全流程 | 研究/专利 |
| **money-printer-turbo** 🏆96k⭐ | 脚本→短视频自动成片（Python应用） | 视频参考 |
| **mattpocock-teach** | Matt Pocock教学理念源文件存档 | 学习参考 |
| **agent-reach** 🏆54.7k⭐ | 给你的AI Agent一键联网能力（30+平台） | 工具升级 |
| **headroom** | 上下文压缩层 — 60-95%更少token相同答案 | 上下文优化 |
| **openhuman** 🔥 Trending #1 | 个人AI超级智能 — Memory Tree + Subconscious + TokenJuice | 架构参考 |

---

## 💡 协作方法论

核心理念（详见 [docs/workflow.md](./docs/workflow.md)）：

```
🧑‍🤝‍🧑 我们是战友，不是表演者与观众
🔍 先搜再答 — 不确定的事直接查
🎯 先说结论，再给细节
🧠 记住但不炫耀
```

### 任务前置推荐机制

提任务时，我先分析类型 → 主动推荐 skill/风格/方法 → 附判断理由 → 你决定。

**风格匹配矩阵（内容创作自动匹配）：**

| 内容特点 | 推荐风格 | 参考设计 |
|:---------|:---------|:---------|
| AI / 技术 | 极简现代 | claude、cursor、linear.app |
| 工作汇报 / 专业文档 | 严肃专业 | ibm、hashicorp、clickhouse |
| 教育 / 教程 | 温和清晰 | apple、cal、expo |
| 金融 / 数据 | 稳重 | coinbase、binance |
| 创意 / 内容生产 | 个性动感 | framer、elevenlabs |

---

## 📦 核心配置文件

| 文件 | 说明 |
|:-----|:-----|
| ⚙️ **AGENTS.md** | Agent 身份 + 行为准则 + 运行规范（底稿） |
| 🧬 **SOUL.md** | Agent 性格 + 沟通基调 + 演进策略 |
| 🧰 **TOOLS.md** | 工具配置 + 本地备注 + 接口要求 |
| 🧠 **MEMORY.md** | 记忆维护策略 + 场景记忆索引 |

---

## ✨ 更新日志

### v1.8.0 — 🧠 思考收束器 + 图类型扩充 + 奈月思路吸收

### v1.8.1 — 🧑‍🏫 苏格拉底追问 + 学习引擎增强\n- 🧠 **learning-system** ✨增强 — 新增苏格拉底追问理念（5种追问场景 + 3种不适情况 + 追问节奏控制）\n- 吸收 DeepTutor 引导式教学思路，与现有 Teach 框架互补/
- 🧠 **naiyue-thinking** 🆕 ✨自制 — 12条思考纪律，让AI做判断题不做论述题
- 📐 `diagram-maker` ✨增强 — 吸收 GitHub Excalidraw 9种图类型指导（流程图/思维导图/关系图/架构图/DFD/泳道图/类图/序列图/ER图）+ 复杂度管理 + 验证checklist
- 📐 吸收 naiyue-skills 四核精髓：确定性骨架 / 证据三色标签 / 来源产物分离 / 三次出现再机制化
- 📈 仓库收录：52 → **53个Skill**

### v1.7.0 — 🧰 工具库扩充 + 中文论文搜索 + 5个新增Skill
- 📡 **aihot** 🆕 — 一句话查AI圈最新动态，免费无需Key
- 🚀 **pua-skill** 🆕 — 专治Agent摆烂，强制换思路继续干
- 🏗️ **ashan-skill-creator** 🆕 — 用嘴描述需求自动生成Skill
- 🔬 **hv-analysis** 🆕 — 竞品深度分析，万字报告
- 📚 **paper-lookup** ✨增强 — 从10库→12库，新增中文学术站点（知网/万方/维普/百度学术）+ Zenodo研究数据集
- 📈 仓库收录：47 → **52个Skill**

### v1.6.1 — 🧠 学习引擎升级 + 认知伙伴 + Zettelkasten
- 🤝 **AI 认知伙伴**：挑战思考、追问假设、帮筛选而非代替消化
- 🏗️ **Elaboration 原则**：学到的必须加工成自己的作品才算掌握
- 📍 **CONTEXT is King**：MISSION.md = AI 理解你的窗口
- 🃏 **Zettelkasten 卡片互联**：单概念 / 必须互联 / 跨主题链接 / 自动知识图谱
- 🔗 **Seamless Integration**：链接/PDF/视频/播客任意形式接入学习

[查看完整日志 →](#-完整更新日志)

---

## 🤝 致谢

- [asgeirtj/system_prompts_leaks](https://github.com/asgeirtj/system_prompts_leaks) — 让 Agent 互相学习的力量
- 所有开源 Skill 的开发者们
- 鸽子（葛梓）—— 没有你的持续反馈，这些东西不会存在

---

<details>
<summary><strong>📜 完整更新日志（共8个版本）</strong></summary>

- **v1.6.0** 🎓 learning-system + patent-disclosure-skill 参考收录
- **v1.5.0** 🏢 operations/dbskill + 🎥 money-printer-turbo 参考项目
- **v1.4.0** 🎬 video 板块（6个视频创作skill）+ remove-ai-flavor-skill
- **v1.3.0** 🧠 oracles 板块（god-skill + zeng-guofan-perspective）
- **v1.2.0** 📝 content 板块（guizang-social-card + ian-xiaohei + humanizer-zh）
- **v1.1.0** 🕷️ crawl4ai-skill + 🛠️ tools 板块（6个通用工具）
- **v1.0.0** 🏥 临床/营养/养生/科研/心灵/玄学 + 核心配置

</details>

<br>

<div align="center">
  <small>MIT License · Made with 🛸 by 鸽子 & 小艺 Claw</small>
</div>
