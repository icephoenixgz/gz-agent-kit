---
name: diagram-maker
description: Create SVG/HTML or Excalidraw diagrams for concepts, architecture, flows, and whiteboards. 支持流程图、关系图、思维导图、架构图、数据流图、泳道图、类图、序列图、ER图9种图类型。
metadata: { "openclaw": { "emoji": "🧭" } }
---

# Diagram Maker

Create diagrams as artifacts, not prose. Start by identifying diagram type, then follow the workflow.

## 输出模式选择

- `excalidraw`: 可编辑手绘风格（默认推荐，可继续编辑）
- `clean-svg`: 教育概念、物理系统、流程、生命周期、简单数据流
- `architecture-svg`: 软件/云/基础设施拓扑

**Routing：**
- 用户想要可编辑/可协作 → Excalidraw
- 用户想要精美独立展示 → SVG/HTML
- 软件架构含基础设施 → architecture SVG
- 科学/产品/流程/概念 → clean SVG
- 不确定 → 只问一个简短问题决定格式，否则默认 clean SVG

## 工作流

### Step 1：识别图类型

根据用户描述判断图类型。有9种专项类型，对应详细指导：

| 图类型 | 参考文件 | 适合场景 |
|--------|---------|---------|
| 流程图 Flowchart | `references/diagram-types.md` | 流程、步骤、操作顺序 |
| 思维导图 Mind Map | `references/diagram-types.md` | 概念层级、头脑风暴 |
| 关系图 Relationship | `references/diagram-types.md` | 连接、依赖、关联 |
| 架构图 Architecture | `references/diagram-types.md` | 系统组件、架构 |
| 数据流图 DFD | `references/diagram-types.md` | 数据流转、输入输出 |
| 泳道图 Swimlane | `references/diagram-types.md` | 跨角色流程、职责划分 |
| 类图 Class Diagram | `references/diagram-types.md` | 类结构、OOP设计 |
| 序列图 Sequence | `references/diagram-types.md` | 对象交互、消息顺序 |
| ER图 ER Diagram | `references/diagram-types.md` | 数据库设计、实体关系 |

**如果用户描述模糊（"帮我画张图"），先问一句图类型，再按对应指导执行。**

### Step 2：提取信息 + 布局

按 `references/diagram-types.md` 对应图类型的指导提取节点、关系和布局方式。

### Step 3：评估复杂度

按 `references/complexity.md` 的元素数量建议表检查。
- 超过上限 → 拆分为多张图（先高层总览，再逐个展开）
- 在范围内 → 继续下一步

### Step 4：生成文件

- Excalidraw → `.excalidraw` JSON（符合 Excalidraw 格式）
- SVG/HTML → 单文件 `.html`（使用 `references/svg-template.md`）

### Step 5：验证

按 `references/complexity.md` 的 checklist 逐项验证，通过后交付。

## Excalidraw 元素规则

所有图类型通用：
- Save `.excalidraw` JSON with `type`, `version`, `source`, `elements`, and `appState`.
- Use bound text for shape labels. Do not use a nonstandard `label` property.
- Keep bound text immediately after its container in the elements array.
- Minimum labeled shape: 120x60. Minimum body text: 16px.
- Use roughness `1`, `fontFamily: 1`, and simple fills.
- **所有文字元素使用 `fontFamily: 5`（Excalifont）**

Excalidraw 元素片段见 `references/excalidraw-patterns.md`。

## SVG 规则

- Single standalone `.html` file with inline CSS and inline SVG.
- No external fonts, JS, images, gradients, glows, decorative blobs, or remote assets.
- Use semantic colors, not rainbow sequences: neutral, input, process, storage, external, risk.
- Draw connectors before nodes so arrows sit behind boxes.
- Every connector path has `fill="none"` and a marker arrow when directed.
- Leave 24px text padding inside boxes; do not let text touch borders.
- Legend only when symbols/colors are not obvious.

SVG 模板见 `references/svg-template.md`。
