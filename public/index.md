# Stanlu

AI 内容可发现性审计（GEO Audit）方法论站。专注 isolated-platform discoverability 诊断、Princeton+Kevin Indig+geo-citation-lab 实证战术应用、AI Search 跨平台差异分析。

## 做什么

用 audit 框架定位「内容在自家平台能被找到，但 LLM 联网搜不会引用」这种 **isolated-platform discoverability** 断裂——这是大多数客户做了内容投入后真正的痛点。

## 方法

- **4 探针** × **3 引擎**（Google / Bing / 百度）× **6 AI 联网搜**（Perplexity / Kimi 联网 / 豆包 / 通义 / 秘塔 / 夸克）× **query 三分类**（品牌词 / 问题词 / 长尾精确词）
- **命中算法**：strict page-level（非根路径 URL 必须含 domain stem + path identifier），18 个 pinned test case 锁口径
- **三轮独立 AI brutal review** 撕过（Codex CLI passes 1 + 3，全 trail 留痕）

## 近期文章

- [2026-11-16 — 礼服卖家投 ChatGPT：点击率是平台平均的 7 倍](https://potato-uu.github.io/posts/2026-11-16-chatgpt-ads-dress-product-feed-click-rate-zh/) — 中文；礼服商品卡片头三天点击率 4.7%，对比 ChatGPT、Google 购物、Meta 基准；单次点击与保本转化率
- [2026-11-16 — Dress sellers on ChatGPT ads: a click rate 7x the ChatGPT average](https://potato-uu.github.io/posts/2026-11-16-chatgpt-ads-dress-product-feed-click-rate/) — English; a 4.7% click rate for dress product-feed ads in three days, against ChatGPT, Google Shopping and Meta benchmarks; cost per click and break-even conversion rate
- [2026-10-29 — ChatGPT 广告每周表现邮件与 Conversions 总览](https://potato-uu.github.io/posts/2026-10-29-chatgpt-ads-weekly-email-conversions-check-zh/) — 中文；每周邮件只是提醒，不是结论；Conversions 总览与每周 10 分钟体检
- [2026-10-29 — ChatGPT Ads weekly performance emails and the new Conversions overview](https://potato-uu.github.io/posts/2026-10-29-chatgpt-ads-weekly-email-conversions-check/) — English; the weekly email is a prompt, not a verdict; Conversions overview and a 10-minute weekly check
- [2026-10-22 — ChatGPT 广告归因窗口与事件质量分（EQS）](https://potato-uu.github.io/posts/2026-10-22-chatgpt-ads-attribution-window-event-quality-zh/) — 中文；窗口只改报表，计费方式才改投放；EQS 不预测效果
- [2026-10-22 — ChatGPT Ads attribution windows and Event Quality Score](https://potato-uu.github.io/posts/2026-10-22-chatgpt-ads-attribution-window-event-quality/) — English; windows change reports only, billing changes delivery, EQS checks data not results
- [2026-10-15 — ChatGPT 广告 10 月 5 日更新：改了什么、没改什么](https://potato-uu.github.io/posts/2026-10-15-chatgpt-ads-visual-ads-measurement-update-zh/) — 中文；视觉广告（美国测试）、首批第三方测量伙伴；谁能看、谁能投没变
- [2026-10-15 — ChatGPT Ads October 5, 2026 update: what changed](https://potato-uu.github.io/posts/2026-10-15-chatgpt-ads-visual-ads-measurement-update/) — English; visual ads (US test), first measurement partners; who sees ads and who can buy unchanged
- [2026-05-26 — isolated-platform discoverability：B站 5/8 rank 1 vs Google/Bing 0/4](https://potato-uu.github.io/posts/2026-05-26-isolated-platform-discoverability-audit/) — case study + GEO audit 框架 + Sales Translation

## About

Stan Lu。做 ChatGPT Ads 出海投放，写 OpenAI 官方更新的解读和 GEO 方法论。每篇出处分三类：OpenAI 官方、媒体报道、我的判断。

## 链接

- [robots.txt](https://potato-uu.github.io/robots.txt) — AI bot 策略（允许 OAI/Claude/Perplexity-SearchBot；拒绝 GPTBot/CCBot/Google-Extended/Bytespider）
- [llms.txt](https://potato-uu.github.io/llms.txt) — 站点概要
- [llms-full.txt](https://potato-uu.github.io/llms-full.txt) — 完整知识库版（含 FAQ）
- [sitemap.xml](https://potato-uu.github.io/sitemap.xml)

本站不导流也不卖货——只发可复现的方法论 + 真数据 + 失败复盘。
