# Zenodo 研究数据集搜索

Zenodo 是 CERN 运营的开放研究数据仓库，收录百万级研究数据集，全学科覆盖。免费，无速率限制。

## 端点

`GET https://zenodo.org/api/records`

## 搜索参数

| 参数 | 必需 | 说明 | 示例 |
|------|:--:|------|------|
| `q` | ✅ | 搜索关键词 | `climate temperature dataset` |
| `size` | ❌ | 返回数量，默认 10，最大 100 | `5` |
| `sort` | ❌ | 排序方式：`mostrecent` / `bestmatch` | `mostrecent` |
| `page` | ❌ | 页码，默认 1 | `2` |

## 认证

无需 API Key。建议设置 `User-Agent` 标识。

## 搜索示例

```bash
# 基本搜索，按时间排序
curl -s "https://zenodo.org/api/records?q=global+temperature+dataset&size=5&sort=mostrecent"

# 翻页
curl -s "https://zenodo.org/api/records?q=climate+data&size=10&page=2&sort=bestmatch"

# 按类型过滤（dataset / publication / software / image / poster 等）
curl -s "https://zenodo.org/api/records?q=protein+structure&size=5&type=dataset"
```

## 响应格式

```json
{
  "hits": {
    "hits": [
      {
        "id": 12345678,
        "metadata": {
          "title": "Dataset title",
          "description": "Full description...",
          "creators": [{"name": "Doe, John", "affiliation": "..."}],
          "publication_date": "2024-01-15",
          "doi": "10.5281/zenodo.1234567",
          "resource_type": {"title": "Dataset"},
          "keywords": ["keyword1", "keyword2"],
          "license": {"id": "cc-by-4.0"}
        },
        "doi": "10.5281/zenodo.1234567",
        "links": {
          "self": "https://zenodo.org/api/records/12345678",
          "doi": "https://doi.org/10.5281/zenodo.1234567",
          "files": "https://zenodo.org/api/records/12345678/files"
        }
      }
    ],
    "total": 42
  }
}
```

## 输出格式

```
## 🗄️ 研究数据集 (Zenodo, N 条)

### 1. [标题]
- 作者: [作者列表]
- 日期: [发布日期]
- DOI: [10.5281/zenodo.xxx]
- 类型: [Dataset / Software / ...]
- 链接: [URL]
- 描述: [摘要片段]
```

## 使用场景

- 查询研究数据集、实验数据、训练数据
- 查找开放获取的论文配套数据
- 搜索全学科的开放研究数据

## 注意事项

- Zenodo 收录的是「数据集」和「研究产出」，不是论文搜索的主库
- 用于 SCI 写作时找可引用的数据，或补充研究方法部分的数据来源
- 每个记录都有 DOI，可在论文中直接引用
- 部分记录附带文件下载，可通过 `links.files` 获取
