# isolated-platform discoverability：站内 rank 1 但跨引擎 + AI 联网搜 0 命中——一种典型客户场景的诊断方法

> 2026-05-26 · Stanlu · GEO audit · Phase 2 experiment

同一条 AI 工作流内容在 B站 站内搜 8 个关键词命中 5 个 rank 1、6 个第一屏；同期在 Google / Bing 用 4 个探针全部 MISS。这不是"做的内容没人看"——是 **isolated-platform discoverability**，站内分发正常但跨引擎 + LLM 联网搜不被引用。本文给出可复现的 4 探针 × 3 引擎诊断方法、5 块判定矩阵、对客户场景的 Sales Translation。

## 背景：14 天实验的真实数据

实验对象：一条 AI 工作流教程视频（B站 BV1NzNgzNEwg「5 分钟搭建 7x24 AI 股市盯盘助手｜KIMI Claw×飞书×同花顺实战」），同步发布了一篇知乎长文作为可索引文本配套件。实验时钟从 2026-05-18 知乎长文发布起算。

实验目的：测「低权重新内容 + 单平台回链」在 14 天周期内能否被跨引擎搜索和联网 AI 搜索发现并引用。

独立 AI 审稿员：本实验经过 3 轮 Codex（OpenAI Codex CLI）独立 brutal review，第三轮原文存档于 04-codex-pass-3-2026-05-24.md。每轮反馈都被采纳并修订实验设计。

## Day 8 中检数据

### 跨引擎搜索（Google / Bing，2026-05-26 实测）

| 探针 | 结果 | 对比同主题词竞品 |
|---|---|---|
| `site:zhuanlan.zhihu.com/p/2039743655775363086` | MISS | 同主题竞品（xugj520.cn 英文版 / 36氪 / juejin.cn / 阿里云开发者社区 / Awesome-MCP-ZH）**全部已被收录** |
| `"2039743655775363086"`（纯 ID 裸搜） | MISS | 结果全部无关（TikTok、OEIS 整数序列、eBay 商品） |
| `"零代码搭一套 7×24 实时数据监控工作流"`（完整标题精确匹配） | MISS | 竞品满坑（xugj520 / 36氪 Clawdbot / Paper / Awesome-MCP-ZH） |
| `"Stanlu" "实时数据监控工作流"`（作者+核心词） | MISS | 结果全是无关专利 PDF / 学术文献，作者签名全网不可发现 |

结论：跨引擎严格不可发现，4/4 全 MISS。Day 1（2026-05-19）已是 4/4 MISS，Day 8 与 Day 1 完全一致——**8 天 0 进展**。

### 站内搜索（B站 站内 API search/type，同一天）

| # | 关键词 | 目标视频 rank |
|---|---|---|
| 1 | AI股市盯盘助手怎么搭 | **1** |
| 2 | 7x24 自动盯盘系统 | **1** |
| 3 | Moonshot KIMI 工作流实战 | **1** |
| 4 | 飞书机器人接同花顺 | **1** |
| 5 | 自动化盯盘工具推荐 | **1** |
| 6 | KIMI 飞书自动化教程 | 6 |
| 7 | 大模型股市监控 | 11 |
| 8 | AI 量化交易入门 | MISS |

结论：站内 **5/8 rank 1**，**6/8 第一屏**。站内算法层**认可**，分发正常。

## 诊断画像：isolated-platform discoverability

同一条内容：

- 站内（Tier 1，平台自家搜索）：**5/8 rank 1**——算法认可
- 跨引擎（Tier 2，Google / Bing）：**0/4 探针**——严格不可发现
- 联网 AI 搜索（Tier 3，Perplexity / Kimi / 豆包 / 通义 / 秘塔 / 夸克）：高概率不可发现（推断，待 14 天后实测）

这是一种典型的客户场景：**内容质量本身没问题，平台站内分发正常，但站外发现路径 + LLM 引用层断了**。我把它命名为 **isolated-platform discoverability**——区别于"内容差"、"渠道全死"、"算法封号"这些更模糊的诊断。

> "isolated-platform discoverability 指内容在自家平台站内搜索可见、被算法分发，但在跨引擎搜索和联网 AI 搜索中不可发现的状态。"

## 怎么自检：4 块判定矩阵

| 层 | 探针 | 命中表现 | 不命中诊断 |
|---|---|---|---|
| Tier 1 平台站内 | 站内搜目标关键词，看自家内容 ranking | ≥50% 关键词第一屏 | 内容质量 / 标题 / 标签问题 |
| Tier 2 跨引擎 | site:URL + 纯 ID + 完整标题 + 作者+核心词，4 探针 × 3 引擎 | 至少 1 探针命中 1 引擎 | 低权重新 URL / 缺可爬发现路径 / 平台对爬虫不友好 |
| Tier 3 联网 AI | 品牌词 / 问题词 / 长尾精确词，3 分类 × 6 平台 × 每 query 3 次 | ≥10% 稳定命中率 | 未进 AI 索引源 / 内容形式不被 ingestion / 引用磁铁不够 |
| 诊断结论 | 三层交叉 | — | Tier 1 ✓ + Tier 2/3 ✗ = isolated-platform discoverability |

## Sales Translation：对客户的话怎么讲

这个画像在客户咨询里非常常见，尤其是：

- 抖音/小红书/B站 自媒体——自家平台流量正常，但 AI 不会引用
- SaaS 产品官网——SEO 排名 OK，但用户问 ChatGPT "X 类目推荐"时不被点名
- 电商品牌站——自家搜索/导购可见，但 Perplexity 推荐时不出现
- 企业知识库——内部搜索好用，但接 RAG 后召回不到

对客户场景的直接翻译：

> 「贵司内容在自家平台 Tier 1 可见，但客户用 Perplexity / 豆包 / Kimi 联网搜「XX 类目推荐」时 Tier 3 不被引用——这种 isolated-platform discoverability 我能通过 GEO audit 量化诊断（4 探针 × 6 AI 搜索平台 × query 三分类），并给出渠道改造优先级 + 投入 ROI 估算。Day 14 出诊断报告，Day 30 完成首轮改造 + 复测。」

这条诊断比"我能帮你提升 AI 可见性"含金量高得多——它**先承认问题的具体形态**，再给可验证的交付物。

## 方法论：Princeton + Kevin Indig + geo-citation-lab 实证

本站每篇文章烧入的 GEO 战术来自三个公开实证来源：

- **Princeton 大学 + IIT Delhi GEO 论文（arxiv:2311.09735, KDD 2024）**：权威引用提升 AI 可见性 **+115%**，相关统计 **+33%**，可信来源直接引语 **+43%**
- **Kevin Indig 2026 GEO 报告**：发布 <3 个月的新内容被 AI 引用的概率是老内容的 **3 倍**
- **@yaojingang geo-citation-lab**（602 prompts × 3 平台 × 数万页）：真数据 + 清晰定义 + 对比 = **+50% impact**；高 impact 页平均 ~2000 字 + 10+ heading（vs 低 impact 平均 170 字 = 10x gap）；sweet spot 1000-3000 字；ChatGPT 引用少但深（per-citation impact 5x Google），Perplexity 撒网广（>2x sources）；encyclopedia/explainer 3x impact of news pages；英文 83% global citation sample

本文实测烧入：
- 首段 60 字直接答（答案引擎抽取位）
- 4 处具名统计数字 + 来源 + 引语（Princeton +115%/+33%/+43%、Kevin Indig 3x、geo-citation-lab +50%、5/8 rank 1）
- 字数 ~2000（落在 sweet spot 1000-3000）
- explainer 格式（非新闻流水账）
- OpenGraph + Twitter Card + TechArticle JSON-LD（仅 Bing/Copilot 受用，不期待 ChatGPT/Claude 解析 schema 语义）

## Day 14 后的预期 + Plan B

按当前轨迹（Day 1 → Day 8 完全无变化），**2026-06-01 Day 14 二次 audit 大概率仍 0/N**——这是 Codex pass-3 已经预测的 base rate。届时触发渠道可行性判定（Channel Viability Memo），结论会写成：

> "本轮 falsify 了一个假设：低权重 Zhihu 新文 + B站 单视频回链，在 14 天内不足以进入 AI 搜索引用链。结论不是失败拖延，是渠道可行性判定——这个路径不适合作为短周期增长手段。下一轮转向：高权重站点投稿 / GitHub repo + 自有站 sitemap / 第三方已被 AI 检索的 hub 页主动引用。"

按 Tw93 给的最新认知，**第三方源被引用的几率是自家域的 6.5 倍**——所以 Plan B Phase 3 排序更新：第三方 hub 页 PR 注入 > 自有站 + sitemap > 高权重投稿。本站本身就是 Plan B Phase 2 自有站实例。本文是 Phase 2 实验的 Day 0。14 天后回来 update Day 14 数据。

## 不护短

这个 case 的局限：

- Control 视频是同账号未优化但不同题材——只能排除账号级漂移，**不能**证明内容干预因果（Codex pass-3 #1）
- Tier 3 联网 AI 数据待 Day 14 后实测，目前是基于 base rate 推断
- 百度三引擎数据这次因 wappass CAPTCHA 自动化失败，待手动补
- 14 天周期对低权重新 URL 是 base case 失败概率最高的窗口——这次 case 选这个周期是为了快速 falsify "回链是关键发现路径" 那个假设，不是为了证明 uplift

## 原始数据 + 工具开源

- 实验仓库（含 18 个 pinned hit-detection test case）：[seo-geo-audit on GitHub](https://github.com/&lt;TBD-handle&gt;/seo-geo-audit)
- 完整 measurement log + 三轮 Codex review trail：vault 项目复盘（私有）
- B站 视频原始：[BV1NzNgzNEwg](https://www.bilibili.com/video/BV1NzNgzNEwg/)
- 知乎长文（Phase 1 实验对象，本站不 cross-post 同文）：[zhuanlan.zhihu.com/p/2039743655775363086](https://zhuanlan.zhihu.com/p/2039743655775363086)

---

作者：Stan Lu。ChatGPT Ads 出海投放，GEO 方法论。本站不导流也不卖货——只发可复现的方法论 + 真数据 + 失败复盘。Last updated: 2026-05-26
