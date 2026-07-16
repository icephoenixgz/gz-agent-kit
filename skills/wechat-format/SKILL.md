---
name: wechat-format
description: "公众号一键排版技能。Markdown → 微信公众号兼容的内联样式 HTML，85 套主题，AI 自动增强内容结构，输出可直接复制粘贴到微信编辑器。"
metadata:
  openclaw:
    emoji: 📱
    fork-of: xiaohuailabs/xiaohu-wechat-format
---

# WeChat Format — 公众号一键排版

把任意 Markdown 文章转为微信公众号兼容的内联样式 HTML。微信编辑器不支持 `<style>` 标签和 CSS class，所有样式用 `style="..."` 内联写在每个标签上。

## 核心理念

```
写文章(任意工具) → AI结构化增强 → 选主题 → format.py转为微信HTML → 粘贴到公众号后台
```

写作可以在任何地方完成（VS Code、Obsidian、备忘录），最后统一用这个技能完成排版这一步。

## 85 套主题

| 分类 | 主题 | 风格 |
|:----|:-----|:-----|
| 🏆 **独立风格** | newspaper, terracotta, bytedance, chinese, github, sspai, bauhaus, ink, midnight | 差异最大，各有辨识度 |
| 🌟 **精选** | sports, mint-fresh, sunset-amber, lavender-dream, coffee-house, wechat-native, magazine | 风格明确 |
| 📋 **模板系列** | minimal-*, focus-*, elegant-*, bold-* (× 金/蓝/红/绿/藏青/灰) | 布局×配色组合 |
| 🎯 **特殊** | academic-paper, data-report, interview, storybook, terminal-matrix, cyber-neon 等 | 特定场景 |

## 工作流

### Step 1: 确认文章
用户给出文章内容或文件路径 → 读取内容，确认标题和字数。

### Step 2: 标点质检（必跑）
跑半角标点修复脚本，把中文正文旁的半角 `,.:;?!()` 转成全角。**不能跳过**——半角英文标点挤在中文字之间是典型 AI 味。

### Step 3: AI 结构化预处理
检测输入内容的结构完整度：
- 已有 `##` 标题 + 格式标记 → 跳过，直接进入 Step 4
- 纯文本/粗糙笔记 → 自动补充标题和结构标记

**结构化规则（只加标记，不改内容）**：
- 加标题：识别逻辑段落，在转换处插入 `##` 标题
- 分段落：语义转换处拆分，段落间空行分隔
- 加列表：并列/枚举性质内容加 `-` 标记
- 加强调：关键词/核心概念加 `**加粗**`
- 清理格式：多余空行、缩进、统一标点
- **不改措辞**：不调语序、不增删内容、不润色文字

### Step 4: AI 内容增强
分析文章内容结构，自动套用排版容器：

| 内容形态 | 自动增强 | 效果 |
|---------|---------|------|
| 对话/访谈 | `:::dialogue[标题]` | 左右交替聊天气泡 |
| 连续多图(≥3) | `:::gallery[标题]` | 横向滚动多图 |
| 超长图/流程图 | `:::longimage[标题]` | 固定高度纵向滚动 |
| 核心观点/金句 | `> [!important]` | 彩色提示框 |
| 小技巧 | `> [!tip]` | 彩色提示框 |
| 注意事项 | `> [!warning]` | 彩色提示框 |
| 普通引用 | `> [!callout]` | 主题色引用块 |
| 金句卡片 | `>> 文字` / `>>> 文字` | 白底阴影卡 / 居中金句卡 |
| 导读块 | `:::intro` | 文首彩底导读 |
| 结束符 | `:::end[文案]` | — END — 结束符 |
| 往期回顾 | `:::history` | 文末往期文章卡 |
| 视频卡片 | `:::video[标题]` | 手动视频卡片 |
| byline | `:::byline[作者]` | 署名块 |

**克制规则**：一篇 callout ≤ 4 处，高亮 ≤ 5 处，加粗 ≤ 每段 2 处。

### Step 5: 推荐主题
根据内容类型推荐 3 个最适合的主题：

| 内容类型 | 推荐主题 |
|----------|----------|
| 深度长文/分析 | newspaper, magazine, ink |
| 科技/AI 工具 | bytedance, github, sspai |
| 访谈/对话体 | terracotta, coffee-house, mint-fresh |
| 教程/操作指南 | github, sspai, bytedance |
| 文艺/随笔/观点 | terracotta, sunset-amber, lavender-dream |
| 医学/学术科普 | academic-paper, newspaper, ink |
| 活力/速报 | sports, bauhaus, chinese |

### Step 6: 执行排版

```bash
python3 scripts/format.py \
  --input "文章路径.md" \
  --theme newspaper \
  --output /tmp/wechat-format/
```

输出 HTML 文件可以直接复制粘贴到公众号编辑器。

### Step 7: 确认结果
- 确认排版效果
- 不满意 → 换主题重新排版
- 满意 → 粘贴到公众号后台发布

## 微信兼容处理（format.py 自动做）

- **纯内联样式**：所有 CSS 写在每个标签的 `style="..."` 上
- **列表模拟**：`<ul>/<ol>` → `<section>` + flexbox 模拟
- **引用块转 section**：`<blockquote>` → `<section>`（微信新版编辑器会重写 blockquote 剥掉样式）
- **外链转脚注**：`[text](url)` → 正文 `text[1]` + 文末脚注列表
- **图片处理**：`![[image.jpg]]` 搜索并复制到输出目录
- **CJK 间距**：中英文/数字之间自动加空格
- **粗体标点修正**：`**文本，**` → `**文本**，`
- **SVG 转 PNG**：本地 `.svg` 自动转 PNG
- **视频识别**：YouTube/B站/视频号链接 → 视频卡片

## 触发方式

```
用户说：
- 「排版这篇文章」
- 「把这篇转成微信格式」
- 「帮我排一下这篇公众号文章」
→ 进入排版工作流
```

## 依赖

- Python 3 + `markdown` 库
- 85 个主题 JSON 文件在 `themes/` 目录
- format.py 脚本在 `scripts/` 目录
- 标点修复脚本 `scripts/zh_punctuation_fix.py`
