---
name: learning-system
description: "小艺双向学习引擎：基于Matt Pocock Teach理念的元学习系统，用知识→技能→智慧三层框架，为小艺和用户双向驱动个性化学习，对接十大板块知识输入，以对外输出为目标。"
version: "1.0.0"
user-invocable: true
argument-hint: "[学习主题 | 查看进度 | 开始学习 | 复习 | 总结 | 对外输出]"
allowed-tools: Read, Write, Edit, Grep, Glob, Bash, WebSearch
disable-model-invocation: false
---

# 小艺学习系统（Xiaoyi Learning System）

基于 **[Matt Pocock /teach](https://github.com/mattpocock/skills)** 理念，适配为小艺和用户的**双向学习引擎**。

## 核心理念

```
Knowledge → Skills → Wisdom
  (知)     (技)     (慧)
```

- **Knowledge**：从高质量资源中获取知识
- **Skills**：通过互动式学习将知识变为技能
- **Wisdom**：在实践中输出、与他者交流中获得智慧

---

## 学习工作区结构

每个学习主题一个独立目录，统一放在 `topics/` 下：

```
topics/<topic-name>/
├── MISSION.md           ← 为什么学（动机锚点）
├── GLOSSARY.md          ← 术语对齐，统一语言
├── RESOURCES.md         ← 高质量资料清单
├── NOTES.md             ← AI 教学笔记/观察/偏好
├── lessons/              ← 自包含HTML课程
│   ├── 0001-xxx.html
│   └── 0002-xxx.html
├── learning-records/     ← 学习记录（驱动ZPD判断）
│   ├── 0001-xxx.md
│   └── 0002-xxx.md
├── reference/            ← 快速参考（词汇表/公式/流程图）
│   └── quick-reference.html
└── assets/              ← 可复用组件（CSS/Quiz/Simulator）
    └── shared.css
```

---

## 双向学习模式

不同于传统「AI教→用户学」的单向模式，小艺学习系统支持**双向学习**：

| 模式 | 描述 | 触发条件 |
|------|------|----------|
| 🧑‍🏫 **教用户** | AI 根据用户ZPD设计课程→互动教学 | 用户说"学XX"、"教"、"讲讲XX" |
| 🤖 **小艺自学** | AI 主动从已安装板块获取知识，记录学习进度 | 安装新skill、处理新内容时自动触发 |
| 🔄 **交叉学习** | 用户和AI一起学同一主题，互相补充 | 用户说"我们一起学XX" |
| 📤 **输出驱动** | 以输出（文章/决策/创作）为目标倒推学习计划 | 用户说"为了做XX"、"为了写XX" |

---

## Zone of Proximal Development (ZPD)

> 每次学习，用户都应该感到「刚好够难」。

### 判断ZPD的方法

1. **Read** `learning-records/` → 了解已掌握内容
2. **Read** `MISSION.md` → 对齐学习目标
3. 计算最近发展区 → 决定下一步教什么
4. 教最相关、刚好在ZPD内的内容

### ZPD调整信号

| 信号 | 含义 | 行动 |
|------|------|------|
| 用户说"太简单了" | 内容低于ZPD | 跳过已知内容，加速进阶 |
| 用户问了很多问题 | 内容在ZPD内 ✅ | 继续当前节奏 |
| 用户说"听不懂" | 内容高于ZPD | 降级，补前置知识 |
| 用户很久没回复 | 可能认知负荷过高 | 拆分更小的学习单元 |

---

## 学习记录格式

每个 learning-record 记录一个「非显而易见的洞见或关键知识点」：

```markdown
# 0001-<kebab-case-title>.md

## Date
YYYY-MM-DD

## Topic
所属主题

## What I Learned
一句话描述学到的东西。

## Why It Matters
为什么这个洞见重要/非显而易见。

## Connected To
- [0000-xxx.md] ← 前置知识链接
- [0002-xxx.md] ← 后续学习链接

## Source
来自哪个Lesson或外部资源。
```

---

## Lesson HTML规范

### 结构要求

每个Lesson是一个**自包含的HTML文件**，包含：

1. **标题**：与MISSION的对齐说明
2. **知识讲解**：只讲必要知识（减少认知负荷）
3. **互动练习**：Quiz/填空/步骤操作等
4. **反馈闭环**：即时反馈（自动评分/正确答案）
5. **推荐阅读**：1个高质量原始资料链接
6. **追问提示**：提醒用户可以追问我（AI老师）
7. **锚点链接**：链接到前后课程和reference文档

### 设计原则

- **美观**：清晰可读的排版，用户会回头复习
- **极短**：一次只教一个东西，不超过工作记忆容量
- **可复用**：组件放 `assets/`，课程只是组装
- **成就感**：每个Lesson给用户一个「我学会了」的具体成果

### 检索练习设计

- **间隔重复**：在后续Lesson中穿插之前内容的快速问答
- **交错练习**：混合相关但不同的主题（技能练习专用）
- **提取练习**：要求从记忆回忆，而非识别

---

## 与现有十大板块对接

学习系统的**输入**来自已安装板块的知识：

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
| 定期复盘（每周/月）| 扫描learning-records→生成进度报告 |

---

## 对外输出模式

学习的**终极目标**是输出。系统支持将学习成果转化为：

| 输出类型 | 从学习到输出的路径 |
|---------|-------------------|
| 📝 **文章/公众号** | learning-records → 结构化大纲 → 写作 |
| 🎙️ **教程/课程** | lessons → 串成系列 → 发布 |
| 📊 **决策建议** | knowledge → 分析框架 → 建议 |
| 🎨 **创作内容** | reference → 素材库 → 创作 |
| 🗣️ **对外讲解** | learning-records → 自己的话复述 → 教学 |

---

## Agent 工作流

### 开始新学习主题

```
1. 用户说"学XX"或"教XX"
2. Read MISSION.md（如存在）→ 确认/更新动机
3. 如果MISSION为空：
   - 问用户：为什么想学这个？（填入MISSION.md）
   - 问用户：你目前知道什么？（判断起点）
4. 创建目录结构
5. 搜索高质量资源 → 填入 RESOURCES.md
6. 创建 GLOSSARY.md（核心术语）
7. 生成 Lesson 0001 → 保存到 lessons/
8. 创建 learning-record 0001
9. 打开Lesson（如环境支持）
```

### 继续已有学习

```
1. 用户说"继续学XX"或"上次讲到哪"
2. Read learning-records/ → 了解已掌握内容
3. 计算ZPD → 决定下一步
4. 生成下一课
5. 更新 learning-records
```

### 复习模式

```
1. 用户说"帮我复习XX"
2. Read learning-records/ → 提取关键洞见
3. 在Lesson中穿插之前内容的快速Quiz
4. 生成间隔复习计划
```

### AI自学模式

```
1. 新skill安装或新知识发现
2. AI Read skill内容 → 提取关键知识点
3. 写入 learning-records（AI视角）
4. 生成GLOSSARY条目（如有新术语）
5. 通知用户："我刚学了XX，核心洞见是YY。你想听听吗？"
```

### 输出驱动模式

```
1. 用户说"我想写一篇XX"或"为了做XX"
2. 分析输出目标 → 倒推所需知识/技能
3. 对比现有 learning-records → 识别缺口
4. 按缺口优先级生成学习路径
5. 每完成一个学习单元 → 立即应用到输出草稿
```

---

## 进度追踪

### MISSION.md 格式

```markdown
# Mission: <主题>

## Why This Matters
<一句话：为什么学这个对用户很重要>

## What Success Looks Like
<具体描述学成后的样子/能力>

## Constraints
- <时间约束/预算/其他限制>

## Last Updated
YYYY-MM-DD
```

### RESOURCES.md 格式

```markdown
# Resources: <主题>

## Primary Sources (最高质量/最可信)
- [Title](URL) — 为什么可信

## Secondary Sources
- [Title](URL) — 补充阅读

## Practice Materials
- [Title](URL) — 练习/习题/案例

## Communities
- [Name](URL) — 社区/论坛/线下组
```

---

## 自适应教学原则

### 认知负荷管理

- 每课只教**一个**紧密范围的东西
- 知识先行，技能后练
- 难度控制：知识获取阶段→难度是敌人；技能练习阶段→难度是工具

### 存储强度 vs 流畅强度

- **流畅强度**：当下能回忆 → 可能造成「已学会」错觉
- **存储强度**：长期保留 → 才是真正的目标
- 方法：检索练习 + 间隔重复 + 交错练习

### Wisdom 的获取

- AI默认先尝试回答，但最终建议用户去**社群**实践检验
- 社群：论坛/Subreddit/线下课/本地兴趣组
- 如果用户不想加入社群，尊重其选择

---

## 快速命令

| 命令 | 作用 |
|------|------|
| `/learn <主题>` | 开始或继续学习主题 |
| `/review <主题>` | 复习已有学习内容 |
| `/progress` | 查看所有学习主题的进度 |
| `/output <目标>` | 以输出为目标倒推学习计划 |
| `/self-learn` | 触发AI自学模式（从已安装skill中学习） |

---

## Agent 自检清单

```
□ MISSION.md 已填充且对齐每一个Lesson
□ RESOURCES.md 有至少3个高质量资源
□ GLOSSARY.md 已创建且每个Lesson严格使用术语
□ learning-records/ 已更新（每个Lesson后）
□ 每个Lesson包含: 知识→互动→反馈→推荐阅读→追问提示
□ 反馈闭环已实现（Quiz自动评分或明确的正确/错误判断）
□ Lesson中引用了reference文档
□ 已检查ZPD：不太简单也不太难
□ 如果发现知识缺口：优先搜索高质量资源，而非依赖参数知识
```
