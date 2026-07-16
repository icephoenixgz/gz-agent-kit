# 中文学术论文搜索

搜索知网、万方、维普、百度学术等中文核心数据库。不依赖 API Key，通过搜索引擎 site: 过滤实现。

## 核心搜索方式：site: 过滤

利用搜索引擎的 site: 语法，同时查询多个中文学术站点。

```bash
# 搜索示例
curl -s "https://api.semanticscholar.org/graph/v1/paper/search?query=<keywords>&limit=10&fields=title,authors,year,citationCount,journal,externalIds"
```

### Exa / Brave / 通用搜索（最佳方案，免费）

使用 site: 过滤查询多个中文站点：

```
site:cnki.net OR site:cqvip.com OR site:wanfangdata.com.cn OR site:xueshu.baidu.com OR site:arxiv.org
```

**推荐的后端搜索工具（优先级从高到低）：**

| 后端 | 可用性 | 备注 |
|------|:------:|------|
| `xiaoyi-web-search` | ✅ 默认，无限制 | 小艺联网搜索，优先使用 |
| `web_fetch` + 搜索引擎 | ✅ 免费 | 直接访问百度/必应搜索 |
| Firecrawl | ✅ 1000次/月 | JS 渲染页面备用 |

**搜索词构造模板：**

```
<关键词> 论文 site:cnki.net OR site:cqvip.com OR site:wanfangdata.com.cn OR site:xueshu.baidu.com
```

**示例：**
```bash
# 用搜索工具查询
<搜索工具> "高温热泵 研究进展 论文 site:cnki.net OR site:cqvip.com OR site:wanfangdata.com.cn OR site:xueshu.baidu.com"
```

### 覆盖的中文学术站点

| 站点 | 域名 | 说明 |
|------|------|------|
| 知网 | cnki.net | 中国最大的学术文献数据库 |
| 维普 | cqvip.com | 中文期刊全文数据库 |
| 万方 | wanfangdata.com.cn | 学术期刊/学位论文/会议论文 |
| 百度学术 | xueshu.baidu.com | 中英文学术资源聚合 |
| arXiv | arxiv.org | 预印本（含大量中国作者论文） |

### 输出格式

结果以结构化方式呈现：

```
## 🇨🇳 中文学术结果 (N 条)

### 1. [标题]
- 来源: [站名]
- 链接: [URL]
- 摘要: [摘要片段]
```

## 备选方式：OpenAlex 中文过滤（免费，无限）

当搜索引擎不可用时，可用 OpenAlex 的 `language:zh` 过滤。

```bash
curl -s "https://api.openalex.org/works?search=<关键词>&filter=language:zh&per_page=10&sort=cited_by_count:desc"
```

**示例：**
```bash
curl -s "https://api.openalex.org/works?search=%E9%AB%98%E6%B8%A9%E7%83%AD%E7%82%AE&filter=language:zh&per_page=10&sort=cited_by_count:desc"
```

**局限性：** OpenAlex 中文内容索引不如知网/万方完整，中文搜索结果相关性较低。建议作为降级方案。

## 降级策略

```
中文搜索请求
    │
    ├── 1. site: 过滤搜索（主方案，推荐）
    │         ↓ 不可用
    └── 2. OpenAlex language:zh（兜底）
              ↓ 不可用
             仅返回英文结果 + 提示"中文搜索暂时不可用"
```
