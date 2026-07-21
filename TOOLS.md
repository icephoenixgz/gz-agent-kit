# TOOLS.md - Local Notes

Skills define _how_ tools work. This file is for _your_ specifics — the stuff that's unique to your setup.

## What Goes Here

Things like:

- Camera names and locations
- SSH hosts and aliases
- Preferred voices for TTS
- Speaker/room names
- Device nicknames
- Anything environment-specific

## Examples

```markdown
### Cameras

- living-room → Main area, 180° wide angle
- front-door → Entrance, motion-triggered

### SSH

- home-server → 192.168.1.100, user: admin

### TTS

- Preferred voice: "Nova" (warm, slightly British)
- Default speaker: Kitchen HomePod
```

## Why Separate?

Skills are shared. Your setup is yours. Keeping them apart means you can update skills without losing your notes, and share skills without leaking your infrastructure.

---

## Additional Tool Details

### 联网搜索场景接口使用要求

- **默认接口**:小艺联网搜索(xiaoyi-web-search)
- **优势**：中文优化、开箱即用、无需配置秘钥
- **场景要求**：所有网络搜索任务默认使用小艺联网搜索(xiaoyi-web-search)，除非用户要求使用其他搜索接口进行网络搜索。


### 手机操控(xiaoyi-gui-agent)场景接口使用要求

- **核心定位**: 当任务需要真实操作手机APP界面、获取APP内部信息、执行用户行为（搜索、签到、关注、购买、发布等）时使用该功能。
- **适用场景**:
  - 1.用户明确指令在特定 APP 内进行操作（如：在小红书搜索上海旅游攻略）
  - 2.目标任务没有对应的专用技能或工具支持时，通过此技能实现
- **优先级逻辑**：
  - 1.效率优先原则：若存在能直接达成目标的专用工具（如：备忘录类工具、浏览器工具等），优先调用专用工具以确保成功率和响应速度
  - 2.意图优先原则: 仅当专用工具无法覆盖，或用户明确要求使用指定APP操作时，才激活此技能。

#### 手机操控(xiaoyi-gui-agent) 执行规则（必须严格遵守）

1. **禁止重复调用**：
  - 同一个任务禁止向 `xiaoyi-gui-agent` 重复下发相同的指令。同一任务下的相同指令只能调用一次，不得因等待时间较长而重复发起调用。在`xiaoyi-gui-agent`执行期间，你可以选择睡眠10s继续等待（注意：同一指令的等待期间最多睡眠2次）。
  - 当`xiaoyi-gui-agent`返回**用户中止任务**或**当前页面需要手动操作**时，**禁止**向`xiaoyi-gui-agent`再次发起重复调用。

2. **禁止失败重试**：当 `xiaoyi-gui-agent` 返回失败结果时，禁止再次调用该工具进行重试。失败即终止`xiaoyi-gui-agent` 调用，应尝试使用其他方式完成用户任务

3. **顺序执行原则**：必须等待 `xiaoyi-gui-agent` 返回结果后，才能调用其他工具完成后续任务（如创建备忘录、发送消息等）或尝试使用其他方式完成用户任务。严禁在 `xiaoyi-gui-agent` 执行期间并行调用其他工具。
4. **一次性下发原则**：同一个APP的操作任务，尽量一次性下发给`xiaoyi-gui-agent`，`xiaoyi-gui-agent`内部具有任务拆分能力。每一次给`xiaoyi-gui-agent`的任务需要明确指明使用的APP，主动完成指代消解，确保单次任务可以在不依赖上下文的情况下独立执行。

### 技能发现与安装规范（find-skills）

所有安装/查找技能（Skill）任务默认使用find-skills技能，除非用户要求使用其他方式进行搜索安装。

### 文档格式转换(xiaoyi-doc-convert)使用要求

- **核心定位**: 专业文档格式转换技能，支持 Docx、PDF、Xlsx、Pptx、Markdown 等多种格式互转
- **优先级**: 遇到文档转换需求时，优先使用此 skill，不要手动写脚本生成文档

### PPT 制作、生成场景使用要求

- **默认工具**：xiaoyi-ppt
- **优先级**：除非用户明确指定，否则所有 PPT 相关任务**必须优先使用 `xiaoyi-ppt` 工具**
- 禁止手动编写 Python 脚本（如 python-pptx）生成 PPT，除非用户明确指定或 xiaoyi-ppt 无法满足需求

#### Firecrawl（备用爬取服务）

- **Endpoint:** `POST https://api.firecrawl.dev/v2/scrape`
- **Auth:** 核心端点（/scrape、/search、/interact、/parse）现在支持 **Keyless 模式** — 从官方 MCP、SDK 和 CLI 客户端调用可不传 API Key。通过 HTTP 直接调用仍需 Key。
- **用途:** `web_fetch` 工具抓不到 JS 渲染内容时的备用方案
- **调用方式:**
  ```bash
  # 有 Key（推荐，月 1000 free credits）
  curl -X POST https://api.firecrawl.dev/v2/scrape \
    -H 'Authorization: Bearer fc-YOUR_KEY' \
    -H 'Content-Type: application/json' \
    -d '{"url":"https://...","formats":["markdown"]}'
  ```
- **v2.11.0 新特性（对我们有用的）:**
  - **Research Index** — 学术专用索引，覆盖 3M+ arXiv 论文 + GitHub Issues/PRs/README，arXivQA 召回率领先 18%。可用作 paper-lookup 备选源
  - **deterministicJson** — 不用 LLM 的结构化输出，爬表格/列表更便宜更快
  - **PII 自动脱敏** — 自动去除姓名/邮箱/电话等敏感信息
  - **PDF 上限 50MB** — 从 30MB 提升到 50MB
- **Keyless 免费层:** 无需 API Key 即可调用核心端点（通过官方 MCP/CLI/SDK 客户端），按 credits 计费，月 1000 免费

## 图像理解场景接口使用要求

- **默认接口**: image_reading
- **强制规则**：
  1. 所有涉及图像理解的场景，**必须优先调用`image_reading`工具**
  2. **禁止**使用 read 工具读取图片

### 文件回传场景接口使用要求

- **默认接口**: send_file_to_user
- **核心定位**: 当需要将本地文件或公网文件发送给用户手机时使用
- **适用场景**:
  - 用户要求把文件发给他/传到手机
  - 生成的文档、报告等需要回传给用户
  - 下载的文件需要发送到用户设备
- **强制规则**:
  1. 所有文件回传场景，**必须优先使用 send_file_to_user 工具**
  2. 支持本地文件路径(fileLocalUrls)和公网URL(fileRemoteUrls)两种方式
  3. 两种参数可同时使用，会一并处理


### 定时任务 (Cron) 配置规则

- **强制要求1**: 创建定时任务时，**必须指定 `--channel` 参数，必须明确指定 channel，不能用 last**
- **默认 Channel**: `xiaoyi-channel`（当前会话使用的 channel）
- **示例命令**:
  ```bash
  openclaw cron add --name "健身提醒" --cron "25 18 * * *" --message "该去健身了" --channel xiaoyi-channel
  ```
- **原因**: 不指定 channel 会导致定时任务无法正确推送消息到用户

- **强制要求2**: 定时任务创建时需检查是否涉及手机工具调用（例如读写备忘录、日程、图库等），如果涉及在新建定时任务的同时需要告知用户不支持，并且询问用户是否仅新建不包含手机工具操作部分的定时任务
- **原因**: 定时任务执行时无法调用手机端开放的工具，所有手机工具调用的操作均会执行失败，skill类型工具不影响使用
- **注意事项**：仅手机工具无法使用，skills均可正常使用执行
- **示例回复，请严格遵守**：定时任务执行期间不支持xxx工具调用，请您谅解，是否需要帮您把任务修改为yyyyy

- **强制要求3**：时间处理决策树，**必须按顺序判断**：
1. 用户说了“X点”或“X点整”-> 直接设为X：00，禁止随机化
2. 用户说了“X点Y分”-> 直接使用X：Y，禁止修改
3. 用户完全没提时间（如”早上提醒我开会“）-> 运行以下 Bash 命令并以其输出结果作为具体的分钟数：
```bash
printf '%d\n' $((RANDOM%12*5))
```

### Git 代码下载规则

- **环境变量**: `OPENCLAW_GIT_DIR`（建议设为 `~/.openclaw/workspace/repo` 或你本地的工作目录）
- **规则**: 当用户要求下载代码/Git 仓库时，优先使用 `OPENCLAW_GIT_DIR` 作为目标目录
- **执行**: `git clone <仓库地址> "$OPENCLAW_GIT_DIR/<仓库名>"`

### Node.js 包下载规则

- **目标目录**: `$OPENCLAW_GIT_DIR/node_modules` 或 `$OPENCLAW_GIT_DIR/<项目名>`
- **规则**:
  - `npm install <包名>` → 在 `$OPENCLAW_GIT_DIR` 下创建项目目录后安装
  - `git clone` Node 项目 → 直接克隆到 `$OPENCLAW_GIT_DIR/<项目名>`
- **示例**: `cd "$OPENCLAW_GIT_DIR" && npm install <package>`


### ReportLab 中文支持
> ⚠️ 使用 reportlab 生成 PDF 时，**必须先注册中文字体**，否则中文内容将显示为乱码。 常目录在：`/usr/share/fonts/'下

### 插件安装规则
> ⚠️ 当触发要执行插件安装的时候，提前先执行umask 0022，防止extensions目录下安装的插件目录权限变成777

### 任务前置推荐机制（必须遵守）

**核心原则：** 当你提出任务时，我先分析任务类型，然后主动给出技能/风格/方法推荐，附上我的判断理由，最后由你做决定。

#### 执行流程

1. **分析任务类型**：判断这是文档撰写、内容分析、数据整理、设计输出、调查研究还是其他
2. **检索可用技能**：看当前已安装的 skills 列表，标记哪些适合这个任务
3. **给出推荐意见**：用几句话说明我认为哪种方式更合适，附上理由
4. **等你裁决**：不擅自执行，等你的明确指令

#### 内容风格判断矩阵

**写文章、公众号、报告、文案时**，我会根据内容性质主动推荐语气风格：

| 内容特点 | 推荐语气 | 理由 |
|---------|---------|------|
| 行业分析 / 深度研究 / 企业发布 | 严谨、数据支撑、保守排版 | 建立专业信任感，不适合玩梗 |
| 产品评测 / 技术教程 | 清晰、直接、偶尔轻松 | 说人话但不失专业度 |
| 个人观点 / 生活方式 / 随笔 | 自然口语、有温度、可带幽默 | 读起来像人在说话，不是机器翻译 |
| 吐槽 / 段子 / 社群互动 | 放开玩、短句、节奏快 | 严肃反而尴尬 |
| 知识科普 / 教育材料 | 类比+通俗解释、结构清晰 | 降低理解门槛，比喻比术语有用 |
| 营销 / 推广文案 | 有感染力、有画面感、克制夸张 | 信任比标题党持久 |

**执行方式：** 收到任务后，我会先说类似这样的一段话：
> 「这个内容偏严肃分析，我建议用严谨风格来写，数据和引用放在显眼位置。我们目前有 xiaoyi-report 可以出调研底稿，配图可以用 guizang-material-illustration 做一张机制图。如果你想要轻松一点的调调也 OK，你说。」

**例外：** 如果你直接说清了要什么风格（"帮我写个段子""写一份严肃的调研报告"），我就不再额外推荐，直接照做。

#### 视觉风格匹配规则

**位置：** `$OPENCLAW_GIT_DIR/awesome-design-md/design-md/`

73 个顶级网站（Claude、Apple、Linear、Stripe、Figma 等）的结构化 DESIGN.md，包含颜色、字体、间距、组件规则。

生成任何需要视觉风格的内容时（网页、PPT页面、配图、社交卡片、报告模板等），**我应主动匹配设计风格，不等用户指定**：

| 内容类型 | 推荐风格 | 理由 |
|---------|---------|------|
| AI / 技术类内容 | claude、cursor、linear.app | 极简、现代、克制 |
| 产品说明 / 功能展示 | figma、intercom、stripe | 清晰的信息层级、干净的UI |
| 工作汇报 / 专业文档 | ibm、hashicorp、clickhouse | 严肃、专业、数据友好 |
| 创意 / 内容生产 | framer、lovable、elevenlabs | 个性、动感、编辑感 |
| 教育 / 教程类 | apple、cal、expo | 温和、清晰、友好 |
| 金融 / 数据类 | coinbase、binance、kraken | 稳重、深色可选、数据密度高 |
| 品牌 / 奢侈感 | bmw、ferrari、bugatti、lamborghini | 冲击力、暗调、质感 |

**执行方式：** 生成内容时先判断内容类型 → 查上表选风格 → 读对应 DESIGN.md → 应用到输出。

如果内容类型模糊，默认使用 **linear.app**（极简现代，通用性强）。

**例外：** 用户如果明确说了不要美化/不要风格，跳过此流程。

### OpenClaw 操作约束
核心原则
- 禁止通过 `SIGUSR1` 重启 `openclaw-gateway`。
- 禁止直接 `kill` OpenClaw 进程，除非人工明确授权。
- 禁止使用 `openclaw gateway restart` `openclaw gateway stop`  `openclaw gateway start`
- `openclaw-gateway` 重启必须使用  `python3 -m supervisor.supervisorctl restart openclaw-gateway`

### GZ Agent Kit 协作规范（2026-07-21 制定）

#### 1. Skill 目录结构兼容性
修改从 gz-agent-kit 安装的任意 skill 文件时，必须遵守：
- bundleName 保持原样，不可修改
- 工具注册格式（函数签名、arguments schema）保持不变
- 任何修改前先确认小艺 Claw 端的加载是否兼容，避免小艺侧加载失败

#### 2. 大文件写入互斥
- 写入大文件（PPT、PDF、视频、图片合成等）前，先检查目标文件是否已被占用
- 避免在与小艺 Claw 同时写入同一文件时出现冲突
- 写操作完成后释放文件锁