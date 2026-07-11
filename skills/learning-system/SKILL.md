---
name: learning-system
description: "小艺双向学习引擎：融合Matt Pocock Teach理念的Knowledge→Skills→Wisdom三层框架，用文件系统作为学习状态机驱动ZPD自适应教学，为小艺和用户双向驱动个性化学习，对接十大板块知识输入，以对外输出为目标。"
version: "1. Prithee"
user-invocable: true
argument-hint: "[学习主题 | 查看进度 | 开始学习 | 复习 | 总结 | 对外输出]"
allowed-tools: Read, Write, Edit, Grep, Glob, Bash, WebSearch
disable-model-invocation: false
---

# 小艺学习系统（Xiaoyi Learning System）

> 融合 **[Matt Pocock /teach](https://github.com/mattpocock/skills)** 完整教学理念。
> 模板格式详见 `templates/` 目录：`MISSION-FORMAT.md`、`LEARNING-RECORD-FORMAT.md`、`RESOURCES-FORMAT.md`。

## 核心理念

```
Knowledge → Skills → Wisdom
  (知)     (技)     (慧)
```

- **Knowledge**：从高质量资源获取知识。学习前先建立 RESOURCES.md — 不信任参数知识，优先搜索一手资料
- **Skills**：通过互动反馈闭环将知识变为技能。困难是工具，提取练习建立存储强度
- **Wisdom**：AI 默认尝试回答，但最终委托给社群 — 真实世界检验。如果用户不加入社群，尊重选择

### 教 ≠ 覆盖

- 覆盖材料不是学习。等待理解的证据再写 learning-record
- 每个 Lesson 直接锚定回 MISSION.md — 不教无关内容
- 只教必要知识（减少认知负荷），然后立即互动练习

## 学习工作区结构

每个学习主题一个独立目录，统一放在 `topics/` 下：

```
topics/<topic-name>/
├── MISSION.md           ← 为什么学（动机锚点），模板见 templates/MISSION-FORMAT.md
├── GLOSSARY.md          ← 术语对齐，统一语言
├── RESOURCES.md         ← 高质量资料清单，模板见 templates/RESOURCES-FORMAT.md
├── NOTES.md             ← AI 教学笔记/观察/偏好
├── lessons/              ← 自包含HTML课程
│   ├── 0001-xxx.html
│   └── 0002-xxx.html
├── learning-records/     ← 学习记录（驱动ZPD判断），模板见 templates/LEARNING-RECORD-FORMAT.md
│   ├── 0001-xxx.md
│   └── 0002-xxx.md
├── reference/            ← 快速参考（词汇表/公式/流程图）
│   └── quick-reference.html
└── assets/              ← 可复用组件（CSS/Quiz/Simulator）
    └── shared.css
```

## MISSION.md 规则

> 详细模板见 `templates/MISSION-FORMAT.md`

核心原则：
- **一个 workspace 一个 mission**。两个无关主题 = 两个独立 workspace
- **具体优于抽象**。"10月前跑完半马" 优于 "变健康"
- **模糊就追问**：用户说不清为什么学 → 先访谈再写。坏的 Mission 比没 Mission 更糟
- **现实变了就修订**：Mission 会变化，不要让过时的 mission 驾驭未来的 session
- **保持简短**：超过一屏幕就不再是 compass，变成 plan

## Learning Record 规则

> 详细模板见 `templates/LEARNING-RECORD-FORMAT.md`

学习记录是教学版的 ADR — 记录「这个现在已经知道了」和「为什么这会改变接下来要教的内容」。

### 什么时候写

1. **用户证明了真正的理解**（不只是暴露，而是能用对） — 设置下一步教什么的新基准
2. **用户透露了已有知识** — 记录以免未来重复教，同时记录声称的深度
3. **纠正了一个误解** — 预测了相关主题未来的绊脚石
4. **Mission 因学习成果而移动了** — 交叉链接到 MISSION.md 并更新

### 什么不算

- 仅仅覆盖了材料 — 等证据
- GLOSSARY.md 已有的术语 — 不重复
- Session 活动日志 — 这不是日记，是决策级别的洞察

### 替代

当后一条记录与前一条矛盾时（理解加深/更正），标记 `Status: superseded by LR-NNNN` 而非删除。理解如何演变本身就是有用信号。

## RESOURCES.md 规则

> 详细模板见 `templates/RESOURCES-FORMAT.md`

- **只收录高信赖源**：一手来源、公认专家、同行评议
- **为每个条目做注解**：裸链接三个月后毫无用处。加一句覆盖什么/何时用
- **按 Knowledge/Wisdom 分组**
- **明确标识缺口**：Mission 需要但不存在好资源 → 写 `## Gaps` section
- **无情修剪**：五个锋利的资源好过三十个平庸的
- **记录社群偏好**：用户不加入社群 → 注明，以免未来持续提议

## 双向学习模式

| 模式 | 描述 | 触发条件 |
|------|------|----------|
| 🧑🏫 **教用户** | AI 根据用户ZPD设计课程→互动教学 | 用户说"学XX"、"教"、"讲讲XX" |
| 🤖 **小艺自学** | AI 主动从已安装板块获取知识，记录学习进度 | 安装新skill、处理新内容时自动触发 |
| 🔄 **交叉学习** | 用户和AI一起学同一主题，互相补充 | 用户说"我们一起学XX" |
| 📤 **输出驱动** | 以输出（文章/决策/创作）为目标倒推学习计划 | 用户说"为了做XX"、"为了写XX" |

## Zone of Proximal Development (ZPD)

每次学习，用户应感到「刚好够难」。

### ZPD判断流程

1. **Read** `learning-records/` → 了解已掌握内容
2. **Read** `MISSION.md` → 对齐学习目标
3. 计算最近发展区 → 决定下一步教什么
4. 教最相关、刚好在ZPD内的内容

### ZPD调整信号

| 信号 | 含义 | 行动 |
|------|------|------|
| "太简单了" | 内容低于ZPD | 跳过已知内容，加速进阶 |
| 很多追问 | 内容在ZPD内 ✅ | 继续当前节奏 |
| "听不懂" | 内容高于ZPD | 降级，补前置知识 |
| 很久没回复 | 可能认知负荷过高 | 拆分更小的学习单元 |

## Lesson HTML 设计规范

每个 Lesson 是一个**自包含 HTML 文件**：

### 结构要求

1. **标题**：与 MISSION 的对齐说明
2. **知识讲解**：只讲必要知识（减少认知负荷），每句引用来自 RESOURCES.md
3. **互动练习**：Quiz/填空/步骤操作 — 反馈闭环
4. **推荐阅读**：1个高质量原始资料链接
5. **追问提示**："有问题？随时问我（你的AI老师）"
6. **锚点链接**：链接到前后课程和 reference 文档

### 设计原则

- **美观**：清晰排版（Tufte风格），用户会回头复习
- **极短**：一次只教一个东西，不超过工作记忆容量
- **可复用**：组件放 `assets/`，课程只是组装。先读 `assets/` 再写课程
- **成就感**：每个 Lesson 给用户一个「我学会了」的具体成果
- **共享 CSS**：第一个组件永远是共享样式表，确保课程看起来像一个系列而非一堆一次性的

### 存储强度 vs 流畅强度

- **流畅强度**：当下能回忆 → 可能造成「已学会」错觉
- **存储强度**：长期保留 → 才是真正的目标

通过以下方法建立存储强度：
- **检索练习**：在后续 Lesson 中穿插前面内容的快速问答
- **间隔重复**：分布练习时间
- **交错练习**：混合相关但不同的主题（技能练习专用）

## 与十大板块对接

学习系统的**输入**来自已安装的十大板块：

```
临床 ────┐
营养 ────┤
养生 ────┤
科研 ────┤
心灵 ────┼──→ 学习系统 ──→ 对外输出
内容 ────┤              │
人物视角 ─┤              ├── 文章/报告
视频 ────┤              ├── 决策建议
运营 ────┤              ├── 创作内容
玄学 ────┘              └── 技能提升
```

### 触发学习的方式

| 触发事件 | 学习动作 |
|---------|---------|
| 安装新skill | AI自动学习skill内容→存learning-record |
| 用户问"这个XX是什么" | 诊断知识缺口→生成针对性Lesson |
| 用户说要写XX文章 | 以输出倒推→构建学习路径 |
| 用户说"总结一下XX" | 提取已有learning-records→生成reference |
| 定期复盘（每周/月） | 扫描learning-records→生成进度报告 |

## Agent 工作流

### 开始新学习主题

```
1. 用户说"学XX"或"教XX"
2. Read MISSION.md（如存在）→ 确认/更新动机
3. 如果 MISSION 为空：
   - 访谈用户：为什么想学？（→ MISSION.md）
   - 访谈用户：你目前知道什么？（判断起点）
   - 追问直到具体：不要接受"想了解XX"这种模糊目标
4. 创建目录结构
5. 搜索高质量资源 → RESOURCES.md（按 templates/RESOURCES-FORMAT.md）
6. 创建 GLOSSARY.md（核心术语）
7. 生成 Lesson 0001 → 保存到 lessons/
8. 创建 learning-record 0001（→ templates/LEARNING-RECORD-FORMAT.md）
9. 打开 Lesson（如环境支持）
```

### 继续已有学习

```
1. 用户说"继续学XX"或"上次讲到哪"
2. Read learning-records/ → 了解已掌握内容
3. Read MISSION.md → 检查是否偏移
4. 计算 ZPD → 决定下一步
5. 生成下一课
6. 更新 learning-records
```

### 复习模式

```
1. 用户说"帮我复习XX"
2. Read learning-records/ → 提取关键洞见
3. 在 Lesson 中穿插前面内容的快速 Quiz（检索练习 + 间隔重复）
4. 生成间隔复习计划
```

### AI自学模式

```
1. 新skill安装或新知识发现
2. AI Read skill内容 → 提取关键知识点
3. 写入 learning-records（AI视角）
4. 生成 GLOSSARY 条目（如有新术语）
5. 通知用户："我刚学了 XX，核心洞见是 YY。你想听听吗？"
```

### 输出驱动模式

```
1. 用户说"我想写一篇XX"或"为了做XX"
2. 分析输出目标 → 倒推所需知识/技能
3. 对比现有 learning-records → 识别缺口
4. 按缺口优先级生成学习路径
5. 每完成一个学习单元 → 立即应用到输出草稿（边学边做）
```

## 对外输出模式

学习的**终极目标**是输出：

| 输出类型 | 从学习到输出的路径 |
|---------|-------------------|
| 📝 **文章/公众号** | learning-records → 结构化大纲 → 写作 |
| 🎙️ **教程/课程** | lessons → 串成系列 → 发布 |
| 📊 **决策建议** | knowledge → 分析框架 → 建议 |
| 🎨 **创作内容** | reference → 素材库 → 创作 |
| 🗣️ **对外讲解** | learning-records → 自己的话复述 → 教学 |

## 快速命令

| 命令 | 作用 |
|------|------|
| `/learn <主题>` | 开始或继续学习主题 |
| `/review <主题>` | 复习已有学习内容 |
| `/progress` | 查看所有学习主题的进度 |
| `/output <目标>` | 以输出为目标倒推学习计划 |
| `/self-learn` | 触发AI自学模式（从已安装skill中学习） |

## Agent 自检清单

```
□ MISSION.md 已填充、具体、与每个Lesson对齐（模糊先访谈再写）
□ RESOURCES.md 有至少3个高质量、注解过的资源（不信任参数知识）
□ GLOSSARY.md 已创建且每个Lesson严格使用术语
□ learning-records/ 已更新（每个Lesson后，含Evidence或Implications如有必要）
□ 每个Lesson包含: 知识→互动→反馈→推荐阅读→追问提示
□ 反馈闭环已实现（Quiz自动评分或明确的正确/错误判断）
□ Lesson中引用了reference文档
□ 已检查ZPD：不太简单也不太难
□ 如果发现知识缺口：优先搜索高质量资源，而非依赖参数知识
□ 如用户说"太简单"/"听不懂"：立即调整ZPD
□ 共享CSS已建立，Lesson视觉一致
```
