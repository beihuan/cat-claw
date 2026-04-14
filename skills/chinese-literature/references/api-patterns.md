# 中文学术数据库检索参考

## 秘塔AI搜索 (Metaso) ⭐ 首选

- **MCP 服务页**: `https://www.modelscope.cn/mcp/servers/metasota/metaso-search`
- **官网**: `https://metaso.cn`
- **覆盖范围**: 网页、学术论文、文档、图片、视频、播客
- **核心优势**:
  - AI 搜索引擎，对学术论文召回率高
  - 支持 `scope: "paper"` 专门搜索论文
  - `includeSummary: true` 可获取网页摘要信息
  - `includeWebContent: true` 可抓取所有来源网页的原文
  - 内置 `metaso_web_reader` 工具，可直接读取任意 URL 的全文内容（支持 markdown/json 输出）
- **三个工具**:

  ### metaso_web_search — 智能搜索
  | 参数 | 必填 | 说明 |
  |------|------|------|
  | `q` | ✅ | 搜索关键词 |
  | `scope` | ❌ | 搜索范围：`"web"` / `"doc"` / `"paper"` / `"image"` / `"video"` / `"podcast"` |
  | `includeSummary` | ❌ | 是否通过网页摘要增强搜索结果召回 |
  | `includeWebContent` | ❌ | 是否抓取所有来源网页的原文 |
  | `size` | ❌ | 返回结果数量，默认 10 |

  **论文搜索示例**:
  ```json
  {"q": "鲁迅小说讽刺叙事研究", "scope": "paper", "includeSummary": true, "size": 10}
  ```

  ### metaso_web_reader — 网页内容读取
  | 参数 | 必填 | 说明 |
  |------|------|------|
  | `url` | ✅ | 要读取的 URL |
  | `format` | ✅ | 输出格式：`"json"` / `"markdown"` |

  **读取论文全文示例**:
  ```json
  {"url": "https://example.com/paper.pdf", "format": "markdown"}
  ```

  ### metaso_chat — 智能问答
  | 参数 | 必填 | 说明 |
  |------|------|------|
  | `q` | ✅ | 问题 |
  | `scope` | ❌ | 搜索范围 |
  | `includeSummary` | ❌ | 是否包含摘要 |

- **访问方式**:
  - **MCP 协议**: 通过 MCP SSE 端点调用
  - **HTTP 调用**: `POST https://metaso.cn/api/mcp`，JSON-RPC 2.0 格式
  - **认证**: `Authorization: Bearer <API_KEY>`
  - **API Key**: 已配置（存储于长期记忆中，不在此文件明文记录）
- **五个工具**:

  ### metaso_web_search — 智能搜索
  | 参数 | 必填 | 说明 |
  |------|------|------|
  | `q` | ✅ | 搜索关键词 |
  | `scope` | ❌ | 搜索范围：`"webpage"` / `"document"` / `"paper"` / `"image"` / `"video"` / `"podcast"` |
  | `includeSummary` | ❌ | 是否通过网页摘要增强搜索结果召回 |
  | `includeRawContent` | ❌ | 是否抓取所有来源网页的原始内容 |
  | `size` | ❌ | 返回结果数量，默认 10 |

  > ⚠️ **实测发现（2026-04-14）**：`scope` 参数**未生效**。`scope: "paper"` 与 `scope: "webpage"` 与不传 scope 返回**完全相同的结果**。`scope: "document"` 返回 total>0 但实际结果为空。因此**不要依赖 scope 做学术过滤**，应使用默认 scope 并在结果端做域名后过滤。

  **论文搜索示例**（使用默认 scope + 后过滤）：
  ```json
  {"q": "鲁迅小说讽刺叙事研究", "includeSummary": true, "size": 10}
  ```

  ### metaso_web_reader — 网页内容读取
  | 参数 | 必填 | 说明 |
  |------|------|------|
  | `url` | ✅ | 要读取的 URL |
  | `format` | ✅ | 输出格式：`"json"` / `"markdown"` |

  **读取论文全文示例**:
  ```json
  {"url": "https://example.com/paper.pdf", "format": "markdown"}
  ```

  ### metaso_chat — 智能问答
  | 参数 | 必填 | 说明 |
  |------|------|------|
  | `message` | ✅ | 用户问题 |
  | `model` | ❌ | 使用的模型，默认 fast |

  ### metaso_topic_list — 专题列表
  获取当前用户可访问的所有 V2 专题列表（自建+订阅），返回专题 ID、名称和简介。

  ### metaso_topic_search — 专题知识库检索
  | 参数 | 必填 | 说明 |
  |------|------|------|
  | `query` | ✅ | 检索查询词 |
  | `topic_id` | ✅ | 专题 ID（从 topic_list 获取） |
  | `size` | ❌ | 返回条数，默认 10，最大 20 |

  ### metaso_topic_file_content — 专题文件内容下载
  | 参数 | 必填 | 说明 |
  |------|------|------|
  | `topic_id` | ✅ | 专题 ID |
  | `file_uuid` | ✅ | 文件 ID（从 topic_search 的 snippet 中获取） |

## 中国知网 (CNKI)

- **网址**: `https://www.cnki.net` / `https://kns.cnki.net`
- **覆盖范围**: 期刊论文、硕博学位论文、会议论文、报纸文章、年鉴等
- **汉语言文学相关数据库**:
  - 中国学术期刊全文数据库（含 CSSCI 来源期刊）
  - 中国优秀硕士/博士学位论文全文数据库
  - 中国重要会议论文全文数据库
- **检索技巧**:
  - 主题检索：同时匹配标题、关键词、摘要
  - 篇名检索：仅匹配标题（精确度高）
  - 关键词检索：匹配作者标注的关键词
  - 全文检索：匹配全文内容（召回率高但噪声大）
  - 可使用 `+` (AND)、`-` (NOT)、`|` (OR) 构建布尔查询
  - 高级检索支持按学科类别（文学→中国语言文学）、核心期刊、CSSCI 等筛选
- **文献质量层次**:
  - CSSCI (南大核心) > 北大核心 > 一般期刊
  - 博士论文 > 硕士论文（一般而言）
- **导出格式**: 支持 GB/T 7714、NoteExpress、EndNote、BibTeX 等
- **访问限制**: 需要机构账号或个人账号登录

## 万方数据

- **网址**: `https://www.wanfangdata.com.cn`
- **覆盖范围**: 期刊论文、学位论文、会议论文、专利、标准
- **特点**: 学位论文收录独立于知网，可能找到知网未收录的论文
- **检索技巧**:
  - 支持按学科分类筛选（文学→中国语言文学）
  - 可按核心期刊、CSSCI 筛选
- **访问限制**: 需要登录

## 维普资讯 (VIP)

- **网址**: `https://www.cqvip.com`
- **覆盖范围**: 中文期刊全文
- **特点**: 部分老旧期刊的收录可能优于知网
- **访问限制**: 需要登录

## 国家哲学社会科学文献中心

- **网址**: `https://www.ncpssd.cn`
- **覆盖范围**: 社科类中文期刊（开放获取）
- **特点**: **免费开放**，无需机构账号，适合无知网权限时使用
- **检索技巧**: 支持按学科门类筛选（中国语言文学）
- **局限**: 收录量小于知网，不包含学位论文

## Semantic Scholar

- **API**: `https://api.semanticscholar.org/graph/v1`
- **用途**: 补充外文文献（如西方叙事学、比较文学方向）
- **检索要点**:
  - 中文论文收录有限，主要用于检索英文文献
  - 对有 DOI 的中文论文可通过 DOI 查询
  - `GET /paper/search?query={query}&fields=title,authors,year,citationCount,externalIds,venue`
- **速率限制**: 100 次/5分钟

## 辅助资源

### DBLP（计算机文学交叉方向）
- 仅在涉及数字人文、计算语言学等交叉方向时使用

### 读秀学术搜索
- **网址**: `https://www.duxiu.com`
- **用途**: 查找学术专著的章节信息
- **特点**: 可查到专著中某一章节是否讨论了特定话题

---

## 汉语言文学常用理论框架与对应检索词

在构建检索策略时，可参考以下常见理论视角与对应的中英文检索关键词：

| 理论方向 | 中文检索词 | 英文检索词（外文补充） |
|----------|-----------|----------------------|
| 叙事学 | 叙事学、叙述学、叙事视角、叙事时间、叙述者 | narratology, narrative perspective, focalization |
| 接受美学 | 接受美学、读者反应、期待视野、隐含读者 | reception aesthetics, reader response, horizon of expectations |
| 对话理论 | 巴赫金、对话理论、复调、狂欢化 | Bakhtin, dialogism, polyphony, carnivalesque |
| 原型批评 | 原型批评、荣格、神话原型、集体无意识 | archetype criticism, Jung, mythological criticism |
| 女性主义批评 | 女性主义、性别叙事、女性书写、社会性别 | feminism, gender narrative, écriture féminine |
| 后殖民理论 | 后殖民、东方主义、文化身份、他者 | postcolonialism, Orientalism, cultural identity |
| 文体学 | 文体学、修辞分析、语言风格、语篇分析 | stylistics, rhetorical analysis, discourse analysis |
| 比较文学 | 比较文学、影响研究、平行研究、跨文化 | comparative literature, influence study, intertextuality |
| 数字人文 | 数字人文、文本挖掘、计量文体学、远读 | digital humanities, text mining, distant reading |

---

## 检索结果质量评估标准

在筛选文献时，使用以下标准评判文献质量（适用于汉语言文学方向）：

| 等级 | 期刊/来源类型 | 通常可信度 |
|------|-------------|-----------|
| A | CSSCI 来源期刊（如《文学评论》《文学遗产》《中国现代文学研究丛刊》） | 高 |
| B | 北大核心期刊 | 较高 |
| C | 普通学术期刊 | 中等，需结合内容判断 |
| D1 | 博士学位论文 | 较高（经过答辩和同行评审） |
| D2 | 硕士学位论文 | 中等（可作为线索来源，引用时需谨慎） |
| E | 学术专著 | 视出版社和作者而定 |

**汉语言文学方向重要期刊（不完全列表）**:
- 《文学评论》
- 《文学遗产》
- 《中国现代文学研究丛刊》
- 《文艺研究》
- 《文艺争鸣》
- 《当代作家评论》
- 《中国比较文学》
- 《民族文学研究》
- 《红楼梦学刊》
- 《鲁迅研究月刊》
