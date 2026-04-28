---
stepsCompleted:
  - step-01-init
  - step-02-discovery
  - step-02b-vision
  - step-02c-executive-summary
  - step-03-success
  - step-04-journeys
  - step-05-domain
  - step-06-innovation
  - step-07-project-type
  - step-08-scoping
  - step-09-functional
  - step-10-nonfunctional
  - step-11-polish
  - step-12-complete
status: complete
completedAt: 2026-04-28
releaseMode: phased
inputDocuments:
  - PROJECT_BRIEF.md
documentCounts:
  briefs: 1
  research: 0
  brainstorming: 0
  projectDocs: 0
classification:
  projectType: web_app
  domain: general
  complexity: medium
  projectContext: greenfield
workflowType: prd
---

# Product Requirements Document - myspace

**Author:** boss
**Date:** 2026-04-28
**Source of Truth:** [`PROJECT_BRIEF.md`](../../PROJECT_BRIEF.md)（357 行权威输入）
**Capability Contract:** §10 Functional Requirements（FR1-FR61）+ §11 Non-Functional Requirements（NFR1-NFR24）

---

## Document Map（双受众速读）

> 给人类读者：按 1→13 顺序读。给 AI agent：按需跳转，每节自包含。

| § | 章节 | 用途 |
|---|---|---|
| 1 | Executive Summary | 一分钟读懂愿景 + 用户分层 + 差异化 |
| 2 | Project Classification | web_app / general / medium / greenfield |
| 3 | Success Criteria | User / Business（激进版）/ Technical / Measurable Outcomes |
| 4 | Product Scope | MVP（M0+M1）/ Growth（M2+M3）/ Vision（M4+） |
| 5 | User Journeys | J1 Linda（雇主）/ J2 Tom（F1）/ J3 boss 运营 / J4 新 AI Agent |
| 6 | Domain-Specific Requirements | GDPR 自律 / F1 数据版权 / AI 标识 |
| 7 | Innovation & Novel Patterns | F1 AI 战术解读三层管道（唯一真 novel） |
| 8 | Web App Specific Requirements | RSC + SSR / Hero & Animation Vocabulary / SEO / a11y |
| 9 | Project Scoping & Phased Development | MVP Strategy / Phase-Journey 映射 / 风险整合 |
| 10 | **Functional Requirements** | **FR1-FR61, 9 类。Capability Contract — 未列即不存在** |
| 11 | **Non-Functional Requirements** | **NFR1-NFR24, 6 类。Quality Attributes — 全 testable** |

**跨节交叉引用：**
- 性能 → §3 Technical Success → §8 Performance Targets → §11 NFR1-4
- a11y → §3 Technical Success → §8 Accessibility Level → §11 NFR13-16
- 鲁棒性 / 降级 → §6 Risk Mitigations → §7 Risk Mitigation → §11 NFR9-12
- AI agent 接力 → §5 Journey 4 → §10 FR58-61 → 项目根 `MEMORY.md` + `docs/`

---

## Executive Summary

myspace 是 boss 的个人综合站，三合一形态：Portfolio（作品集）+ F1 内容站 + AI Lab（实验室），共享同一套设计系统与工程标准。产品定位是"工程师的审美标本"——视觉与工程并重，作为 boss "AI 创新者 + 产品人" 身份的长期可演进数字门面。

**目标用户分层：**

- **P1a 雇主 / 合作方**（首次访问，3 分钟判断窗口）—— 靠 Portfolio 案例 + 工程深度建立信任
- **P1b 同行 / AI 爱好者** —— 靠 Lab 可交互 demo + Portfolio 技术细节留住停留时间
- **P1c F1 读者**（搜索流量为主）—— 靠日报订阅式打卡与 AI 战术解读形成口碑
- **P2 boss 自己**（内容创作 + 数据查看）—— 长期可维护、AI 协作流畅
- **P0.5 AI Agent**（Claude / Codex / 未来 agent）—— 规范无歧义、工作流可机读

**解决的真问题：** 不是缺一个网站放作品。boss 需要一个能反映"技术品味、产品判断、工作流方法论"的长期可演进数字载体——能被反复回访、能被分享、能在 AI 时代帮 boss 赢得"这人值得聊"的判断。

### What Makes This Special

1. **三合一不是拼盘** —— 每个板块都是独立可消费的迷你产品，但共享 Design Tokens + 工程标准，确保整站审美与工程在同一水位
2. **F1 AI 战术解读**（核心差异化）—— Jolpica API + 4 路 RSS 数据源 → Claude 生成长文 → 人工 review → 发布的三层管道；不是另一个赛果聚合站，是"AI 帮你看懂赛后战术"
3. **审美 + 工程双在线** —— landonorris 级仪式感（大字 / 滚动驱动 / **首屏鼠标轨迹头盔 mask reveal** / 法拉利红 Rosso #DC0000 品牌时刻）+ WCAG 2.2 AA + LCP p75 < 2.0s + JS 首屏 < 200KB gzipped；大多数个人站二者只占其一
4. **AI Native 工作流的活样本** —— 站本身就是开发流程（BMAD V6 + Claude + Codex 多 agent + Obsidian 追踪）的成品，工作流可被讲、可被复用、可被借鉴

**核心洞察：** AI 时代技术栈不再是壁垒，工程品味变成稀缺资源。F1 兴趣不是装饰，是"AI 协作把个人爱好做成可发布产品"的最佳示范，对应 boss 的 Agentic Workflow 实践方向。

## Project Classification

- **Project Type:** Web App（Next.js 15 App Router + TypeScript strict）
- **Domain:** General（个人内容站；隐私自律基线参考 GDPR，无强合规要求）
- **Complexity:** Medium —— 多模块 / 多数据源 / AI 集成 / 双语 / 自建埋点 / 严苛性能预算；但单人开发、无登录、无支付、无多租户
- **Project Context:** Greenfield（全新建，无遗留代码 / 数据 / 用户）

## Success Criteria

### User Success

按 4 类用户分层定义"用户体验到的成功"：

- **P1a 雇主 / 合作方** —— 3 分钟内读完至少 1 份完整作品案例（背景→做了什么→结果→回看四段式可读完），并触发后续动作（点 contact / 复制邮箱 / 点外链）
- **P1b 同行 / AI 爱好者** —— Lab 至少 1 次 demo 完成交互；全站停留 ≥ 3 分钟
- **P1c F1 读者** —— 日报读完率（scroll_depth ≥ 90%）≥ 50%；7 日内复访率 ≥ 20%
- **P2 boss 自己** —— 发布单篇内容（Obsidian → MDX → push）≤ 30 分钟；半年后回看代码 + docs 能在 10 分钟内重建上下文
- **P0.5 AI Agent** —— 新 agent 读完 PROJECT_BRIEF + PRD + docs/ 即可独立加 feature，**不需要追问横切规范**

### Business Success（激进版 — boss 拍板）

个人站语境下，"business"映射为个人 brand 与影响力：

- **3 个月**：站上线、Portfolio ≥ 5 份作品、F1 日报连续 30 天稳定产出、F1 战术解读 ≥ 3 篇、月独立访客 ≥ 1500、≥ 3 次外部分享 / 引用
- **6 个月**：F1 战术解读 ≥ 10 篇；Lab ≥ 2 个可分享 demo；月独立访客 ≥ 5000；≥ 1 篇内容被同行 / 媒体引用
- **12 个月**：通过站获得 ≥ 2 次实际合作机会（雇主 / 同行 / 媒体 / 外部需求）；F1 内容 30 日复访率 ≥ 30%；月独立访客 ≥ 15000

### Technical Success

- **CWV p75**：LCP < 2.0s（S 级页面 < 1.8s）/ INP < 200ms / CLS < 0.1
- **JS Budget**：首屏 ≤ 200KB gzipped；动效库总和 ≤ 80KB gzipped
- **可访问性**：WCAG 2.2 AA 全站达标；Lighthouse A11y ≥ 95；键盘 100% 可达；prefers-reduced-motion 降级生效
- **质量门**：Vitest 覆盖单元 + 组件；Playwright 覆盖核心 E2E；axe-core CI 红线；PR 必过 review
- **F1 数据可靠性**：GitHub Actions cron 7 日稳定率 ≥ 95%；失败能被邮件 / 企业微信告警，能手动补跑
- **AI 成本可控**：Anthropic 调用每月预算上限可见、可设阈值告警

### Measurable Outcomes

| 指标 | 测量手段 | 目标值 |
|---|---|---|
| CWV 三色 "Good" 占比（p75） | Vercel Speed Insights | ≥ 75% |
| Lighthouse A11y | CI 自动跑 | ≥ 95 |
| 月独立访客 | Vercel Analytics + 自建 visitorId | M2 起 ≥ 1500 / 6mo ≥ 5000 / 12mo ≥ 15000 |
| F1 日报产出连续天数 | cron 成功记录 | M2 起 ≥ 30 天连续 |
| F1 战术解读累计 | `/admin/queue` 已发布数 | 3mo ≥ 3 / 6mo ≥ 10 |
| 外部触达事件 | 埋点 `external_link_clicked` / `contact` | ≥ 5 次 / 月（M2 起） |
| Story 闭环时长（PRD → 上线） | BMAD `_bmad-output` 时间戳 | < 5 工作日 / story（含前后端 + 测试） |
| 实际合作机会触发 | boss 自记录 | 12 个月 ≥ 2 次 |

## Product Scope

### MVP - Minimum Viable Product（对应 BRIEF M0 + M1）

**判断标准：** 站能上线、能展示 boss 的工程品味、新 agent 接手能继续干活

- 项目脚手架（Next.js 15 + Tailwind v4 + shadcn + Design Tokens 编译）
- 横切规范 `docs/` 重建（≥ 8 条 ADR、组件规范、内容规范、a11y 规范）
- BMAD V6 工作流装好、可闭环（新 feature 能走完整 PRD → story 链路）
- **Home 页**（仪式感开场，承担"3 秒抓住眼球 + 30 秒说清是谁"）
- **Portfolio 列表 + 详情**（3-5 份作品 MDX，四段式叙事）
- **About / Contact**
- **双语 zh / en 切换可用**（next-intl + 路由 `/[locale]/...`）
- **Vercel 部署上线**（暂用默认子域）

### Growth Features (Post-MVP)（对应 BRIEF M2 + M3）

- **F1 整套子模块**：F1 首页 / 日报列表 + 详情 / 车手 / 车队 / 积分榜 / 赛程 / 比赛详情 / AI 战术解读
- **F1 数据管道**：Jolpica + 4 路 RSS + GitHub Actions cron 自动产出
- **F1 AI 战术解读**：Claude 生成 + 人工 review 三层流
- **自建埋点系统**：`/api/track` + Turso + 关键事件清单
- **Admin 只读看板**：`/admin/{analytics,f1,queue,ai-usage}` Basic Auth
- **AI Lab**：至少 1 个可交互 demo（建议与 F1 / Portfolio 主题相关）
- **Sentry**（M2 起）

### Vision (Future)（对应 BRIEF M4+）

- 博客系列化（技术文 + 观点文，深度长文为主）
- F1 内容生态化（newsletter 订阅 / 长内容深度报道）
- 全站搜索（minisearch / 视量级评估 Algolia）
- PostHog（量大才接）
- 更多 Lab demo / 跨 demo 数据互通
- 视情况升级数据层（MDX → Turso → Postgres）

## User Journeys

### Journey 1 — Linda（P1a 雇主，Success Path）

Linda 在 LinkedIn 看到 boss 的 profile，3 分钟内要判断"值不值得邀面"。点进 myspace.com，Home 大字开场 5 秒抓到方向。Portfolio 用四段式（背景→做了什么→结果→回看）展示案例，她点进 AI Agent 工程化案例看到完整方法论。意识到底部还链了 Lab 可交互 demo，点进去玩了一下："这人不只是会说还会做。"再读一篇 F1 战术解读，发现工程师还能写出有人格的内容。**Resolution:** 复制 contact 邮箱发出面试邀请。

**Reveals capabilities:** Home 仪式感开场 / Portfolio 四段式叙事 / 跨板块导流 / Contact 触达 / 埋点 `external_link_clicked` + `contact`

### Journey 2 — Tom（P1c F1 老车迷，Success + Edge Case）

**Success Path:**
朋友圈分享进站 → F1 首页扫倒计时 + 当前赛季速览 → 读战术解读（DRS 列车节奏 + 进站策略 + 两停 vs 一停 + 数据图 + 作者观点 + "AI 协作 + 人工 review" 标识）→ 翻日报列表 → 进 Lando 详情页（双语 + 数据 + 观点结合，不是维基百科复制）→ 加书签每天打卡。一周后转发到 F1 微博群。

**Edge Case:**
某天 cron 因 Jolpica API 改 schema 失败，今日日报未产出。F1 首页没崩，列表顶部显示降级 fallback："今日数据源故障，已通知作者，下方为昨日内容。"Tom 反而觉得"这站还知道告诉我"，对稳定性印象更好。第二天恢复后他看到"昨日 + 今日双日报"。

**Reveals capabilities:** F1 首页倒计时 + 速览 / 日报列表 + 详情 / 车手详情双语版 / 战术解读长文 + 来源标识 / 分享按钮 + 埋点 `share` / 错误降级 fallback UI / cron 失败告警 / 手动补跑流

### Journey 3 — boss（P2 自己运营 Operations，发布一篇 F1 战术解读）

周日晚西班牙站刚跑完。Obsidian 打开 myspace 项目笔记，cron 已经把今天的赛后摘要拉到 `_drafts/`。打开编辑器读 AI 初稿，改观点段加自己判断（"这场 Red Bull 进站是一年来最差"）。前后 25 分钟。`/admin/queue` 标记"已 review"。git push → Vercel 1 分钟部署完。`/admin/analytics` 实时看到首批读者进来。Obsidian 记一句"这次工作流跑通了"。

**Reveals capabilities:** cron 自动产 draft → `_drafts/` 工作流 → `/admin/queue` review → git push 即部署 → `/admin/analytics` 实时反馈 → Obsidian 双向追踪 / AI 成本可见 (`/admin/ai-usage`)

### Journey 4 — 新 AI Agent（P0.5，接手加 feature）

boss 开新会话让全新 Claude / Codex agent 加"F1 车队对比页"。Agent 第一步：`MEMORY.md` → `PROJECT_BRIEF.md` → `docs/index.md` → ADR 列表 → 现有路由结构。15 分钟有完整地图。启动 `bmad-create-prd` sub-feature 模式生成对比页 PRD（沿用既有决策不重新发明）→ architecture → ux-design → epic → story → dev-story → code-review → e2e。第二天 boss 醒来 PR 已开好等 merge。**全程没追问任何横切规范。**

**Reveals capabilities:** MEMORY + BRIEF + docs/ 是 agent 入口接力点 / BMAD V6 闭环 / sub-feature 模式（大 BRIEF 衍生小 PRD）/ `_bmad-output/` 状态可恢复 / 多 agent 协作让 boss 离场

### Journey Requirements Summary

| 类目 | 能力 | 来源 |
|---|---|---|
| 信息架构 | Home 仪式感 / 跨板块导流 / 双语 zh-en 切换 | J1, J2 |
| Portfolio | 列表 + 详情 / 四段式叙事 / 工程深度展示 | J1 |
| F1 | 首页 + 倒计时 / 日报 + 详情 / 车手 / 车队 / 积分榜 / 赛程 / 比赛详情 / 战术解读长文 | J2 |
| 内容流 | cron 自动 draft / `_drafts/` / `/admin/queue` review / git push 即部署 | J3 |
| Admin | `/admin/{analytics,f1,queue,ai-usage}` Basic Auth 只读看板 | J1, J3 |
| 埋点 | `external_link_clicked` / `contact` / `share` / `f1_*` / 复访追踪 | J1, J2 |
| 鲁棒性 | cron 失败告警 / fallback UI / 手动补跑 | J2 edge |
| Agent 入口 | MEMORY + BRIEF + docs/index.md + ADR 列表 / BMAD V6 闭环 | J4 |
| 协作 | sub-feature 模式 / 多 agent 协作 / `_bmad-output/` 状态可恢复 | J4 |

## Domain-Specific Requirements

虽然分类为 General domain（无强合规如 HIPAA / PCI / FedRAMP），但作为**面向公开访客的个人内容站 + 三方数据消费方 + AI 集成产品**，仍有几类 domain 特定要求需要前置约束。

### Compliance & Regulatory（合规自律）

- **GDPR / 全球隐私自律**：默认匿名 visitorId（localStorage UUID，非 Cookie）/ 不存 IP 仅取国家代码 / 尊重 `Do Not Track` 信号 / 提供 `/privacy` opt-out 入口
- **F1 数据版权边界**：仅消费白名单数据源（Jolpica API + F1 官方 RSS + Motorsport.com RSS + The Race RSS + Reddit r/formula1 Top 1d）；不爬白名单外的站；引用第三方文章必须保留 source URL 与署名
- **AI 生成内容标识**：F1 战术解读必须显式标注"AI 协作 + 人工 review"来源；不冒充人工原创；摘要类亦标注"AI 生成"
- **Cookie 极简**：除 locale 偏好外**不用 Cookie**；其余用户偏好走 localStorage

### Technical Constraints（域特定技术约束）

- **CWV 是 SEO 命门**：内容站 SEO 强依赖 LCP / INP / CLS，p75 必须 ≥ 75% "Good"（弱于此搜索引擎降权）
- **i18n SSR 可达**：双语路由 `/[locale]/...` 必须服务端可达，搜索引擎能完整爬 zh-CN 与 en-US 两份内容（避免 hydration 才出文）
- **AI 调用预算控制**：Anthropic SDK 调用必须有月预算上限可见 + 阈值告警（90% 触发邮件，100% 暂停非关键调用）
- **Cron 跨时区一致**：F1 cron 用 UTC 触发（`0 7 * * *` UTC = 北京 15:00），避免夏令时漂移
- **Prompt Caching 强制**：所有 Claude 调用必须复用 prompt cache（system prompt + 历史背景），控成本 + 减延迟

### Integration Requirements（集成要求）

- **数据源契约**：Jolpica API 改 schema 时必须降级（fallback UI + 告警），不让站崩
- **GitHub Actions ↔ Vercel**：cron 机器自动 commit 触发 Vercel 部署；commit 消息前缀区分 `[bot]` vs `[boss]`，方便 audit
- **Anthropic SDK 模型选择**：Claude Sonnet 4.6 用于日报摘要 + 翻译；Claude Opus 4.7 用于战术解读长文（明显高质量需求才上 Opus，控成本）
- **MDX ↔ Obsidian**：boss 在 Obsidian 写、git push 触发 MDX 渲染；Obsidian wikilink `[[xxx]]` 映射到站内路由

### Risk Mitigations（domain 风险与降级）

| 风险 | 缓解 |
|---|---|
| Jolpica API 改 schema → cron 失败 | fallback UI 显示昨日内容 + 邮件告警 + `/admin/queue` 显示失败状态 + 可手动补跑 |
| AI 生成内容质量不稳 | 人工 review 兜底（战术解读必须 review 才发布；摘要类有 quality threshold） |
| 月度 AI 账单失控 | `/admin/ai-usage` 看板 + 月预算阈值告警 + Opus / Sonnet 分级使用 |
| F1 第三方 RSS 源消失 / 改版 | 多源冗余（4 路 RSS 任一可用即继续）+ 单源失败不影响整体管道 |
| 隐私争议（埋点被举报） | opt-out 入口 + 数据留存上限（90 天滚动）+ 不存 IP / 不用 Cookie |
| Vercel / GitHub Actions 服务中断 | 站静态部分继续可访问；cron 失败有重试 + 手动补跑入口 |

## Innovation & Novel Patterns

只聚焦一个真正 novel 的部分：**F1 AI 战术解读三层管道**。其他实践（Design Tokens 工程化 / 多 agent 工作流 / 三合一站架构）属于"优秀执行"而非创新，不在此节展开。

### Detected Innovation Areas

**F1 AI 战术解读**——在 F1 中文内容圈，"AI 协作 + 人工 review"形态尚未见到直接对标。现有方案二选一：

- **全人工长文**（Motorsport / The Race / The Athletic F1）：深度好但产能受限、人力贵
- **全自动赛果聚合**（多数 F1 中文公众号 / 站）：速度好但缺洞察、缺人格

myspace 走第三条路：**AI 把数据 + 多源观点摘要成战术解读初稿，boss 人工 review 后发布**——产能 × 人格双在线。

### Market Context & Competitive Landscape

- **国际**：The Athletic F1 / The Race 是人工长文标杆；尚未见"AI + 人工"双标识的中文 F1 战术内容站
- **中文圈**：F1 微博 / 虎扑 / 知乎多为社区讨论；公众号多为赛果搬运；缺"工程化的赛后战术拆解"
- **窗口期**：F1 2026 赛季新规（动力单元 + 主动空气动力学）带来大量战术调整 → 新内容形式的好契机

### Validation Approach

- **MVP 验证**：M2 阶段先发 5 篇战术解读，看 P1c 读完率（≥ 50%）+ 7 日复访率（≥ 20%）+ 主动外部分享数（≥ 3 次 / 篇）
- **质量基线**：boss 自己读一篇能否通过"我自己愿不愿意转发"的硬指标
- **同行验证**：其中 1-2 篇主动发到 F1 微博 / 知乎 F1 话题，看 1 周内是否引来真实讨论或被引用
- **退路**：如果发现 AI 初稿质量难撑 review 工作量，降级为"AI 摘要 + boss 长评论"双栏式（保留差异化但减低 AI 依赖）

### Risk Mitigation

| 风险 | 缓解 |
|---|---|
| AI 生成内容缺人格、像维基百科 | review 必改观点段 + 强制加 boss 自己的赛后判断；review 工时上限 30 分钟，超时改 boss 全人工 |
| 用户察觉"AI 味"导致信任下降 | 显式标注"AI 协作 + 人工 review"；不冒充人工原创 |
| 数据源失败（Jolpica / RSS）导致断流 | 已在 Domain Risk Mitigations 表覆盖 |
| F1 中文圈对 AI 内容反感 | 质量打消偏见——只发 boss 真认同的观点段 |
| Opus 4.7 战术解读月成本超预算 | 月预算阈值告警 + 关键场次用 Opus 一般场次降级 Sonnet 4.6 |

## Web App Specific Requirements

### Project-Type Overview

myspace 是 Next.js 15 App Router 的内容驱动型 web app，渲染策略以 **RSC + SSR 为主**，交互岛屿走 client components。SEO 是命门（F1 + 博客依赖搜索流量），可访问性与性能预算是质量门。

### Rendering Strategy（SPA / MPA / RSC 拆解）

- **主体**：RSC（React Server Components）+ SSR——首屏可爬、可读、无 hydration 阻塞
- **客户端岛屿**：仅交互必要处用 `"use client"`（双语切换 / 主题切换 / Lab demo / 部分动效）
- **动效层级**：CSS-first（L1）+ Framer Motion（L2，岛屿）+ GSAP / Lenis（L3，仅 1-2 处页面级仪式）
- **不做**：纯 SPA（CSR-only）会损 SEO；纯 MPA 会丢动效

### Browser Support Matrix

| 类别 | 范围 |
|---|---|
| 目标浏览器（最新 + 前一版） | Chrome / Edge / Firefox / Safari Desktop & iOS Safari 16+ / Android Chrome 110+ |
| 明确不支持 | IE 11 及以下 / Opera Mini / UC 浏览器特殊渲染模式 |
| 降级策略 | CSS `@supports` + JS feature detection；不做完整 polyfill |

### Responsive Design Breakpoints

| 断点 | 宽度 | 用途 |
|---|---|---|
| `sm` | 640px+ | 大手机 / 小平板 |
| `md` | 768px+ | 平板竖屏 |
| `lg` | 1024px+ | 平板横屏 / 小笔记本 |
| `xl` | 1280px+ | 桌面（**设计起点**） |
| `2xl` | 1536px+ | 大屏 / 4K |

- **设计起点：`xl`**（桌面优先，向下响应；≥ 桌面级是 myspace 主战场）
- **触控区域**：移动端 ≥ 44×44pt 热区（WCAG 2.5.5）
- **不做**:仅移动端 / PWA 形态

### Performance Targets（web 视角浓缩）

参见 Success Criteria → Technical Success；此处补充 web 特有约束：

- LCP **S 级页面 < 1.8s** / A 级 < 2.0s / B 级 < 2.2s / C 级 < 2.5s
- 首屏 JS ≤ **200KB gzipped**；动效库总和 ≤ **80KB gzipped**
- **图片**：Next.js `<Image>` + AVIF/WebP + 关键图 priority
- **字体**：Variable Font + `font-display: swap` + preload 关键字体
- **路由 code-splitting**：默认行为，不手动划 chunk
- **Edge vs Node runtime**：HTML/API 默认 edge；Anthropic SDK / sharp / Turso 走 Node runtime

### SEO Strategy（命门）

- **Metadata API**：每路由必有 `generateMetadata`，含 title / description / OG / Twitter Card
- **结构化数据 JSON-LD**：F1 文章 `Article` + `Person` + `SportsEvent`；Portfolio `CreativeWork` + `Person`；战术解读 `Article`
- **Sitemap**：`app/sitemap.ts` 动态生成，含双语 entry + lastmod
- **Robots**：`app/robots.ts` 显式 allow/disallow（`/admin/*` disallow）
- **Hreflang**：双语 `alternate` link（`zh-CN` / `en-US` / `x-default`）
- **OG 图片**：动态 OG（`/api/og/[kind]`）+ 文章封面 fallback
- **Canonical**：每页 explicit；双语视为不同 entity 但互相 alternate
- **Web Vitals 上报**：Vercel Speed Insights + 自建 `/api/track` 双轨

### Accessibility Level

- **目标**：WCAG 2.2 AA 全站达标
- **CI 红线**：`@axe-core/playwright` 跑核心路由，违规 → build 失败
- **Lighthouse**：A11y ≥ 95（PR 必跑）
- **键盘**：100% 可达 + 焦点环可见 + skip-link
- **屏幕阅读器**：landmark 完整 + ARIA 语义正确（不滥用）
- **降级动效**：`prefers-reduced-motion: reduce` 时 L2/L3 降级到 L1 或瞬时
- **色彩对比**：文字 ≥ 4.5:1 / 大字 ≥ 3:1 / UI 元素 ≥ 3:1

### Hero & Animation Vocabulary（核心动效语汇）

参考 landonorris.com 的标志性效果，**单一深色主题（黑底 + 纸白字 + 法拉利红点缀）**：

- **首屏 Hero**：虚拟人像（boss 角色化形象，非真实照片）+ F1 车手头盔图（若隐若现叠加）+ **鼠标轨迹 mask reveal**（鼠标移入时头盔跟随光标轨迹显现，松开手停止）
- **滚动驱动**：头盔随滚动从 hero 滑出 + 尺寸 / 角度变换（GSAP / ScrollTrigger）
- **Lenis 平滑滚动**：全站默认开启，inertia smooth；`prefers-reduced-motion: reduce` 时自动禁用
- **Split text reveal**：章节标题单词级淡入（Fraunces Variable 大字号配合）
- **Counter 累计**：Portfolio "结果"段、F1 战术解读数据点用滚动到位时累计显示
- **Sticky 章节切换**：Home 页 1-2 处页面级仪式（GSAP / ScrollTrigger）
- **Mask reveal 图 / 视频**：滚动到位时 mask 揭示（Portfolio 详情、F1 文章配图）
- **路由切换过渡**：fade ≤ 200ms（Framer Motion `AnimatePresence`），不阻塞首屏 LCP
- **Marquee 跑马灯**：横向滚动文字带，用在 Portfolio "工具栈"行
- **CSS noise grain**：全站微弱噪点纹理（CSS 实现，不上 canvas，几乎零成本）
- **品牌色用法**：法拉利红 #DC0000 仅用于关键 CTA / 链接 hover / 选中态 / 强调数据点；不做大面积红色背景
- **明确不取**：cursor 被吸附磁吸 / 全屏 scroll-jacking / parallax / 3D WebGL 头盔（违 JS 200KB 预算）/ 明暗主题切换

### Implementation Considerations

- **缓存策略**：静态页 SSG + revalidate；F1 数据 ISR（每小时一次）；战术解读发布即 revalidate
- **错误边界**：每路由 `error.tsx` + `not-found.tsx` + 全局 fallback
- **Loading 态**：`loading.tsx` + skeleton（不做 suspense fallback 黑屏）
- **类型安全**：Schema 用 Zod，API 契约 OpenAPI 3.1，类型用 `openapi-typescript` 生成（双向校验）
- **路由组**：`(public)` / `(admin)` / `[locale]` 三层组织

## Project Scoping & Phased Development

### MVP Strategy & Philosophy

**Release Mode:** **Phased** —— boss 在 PROJECT_BRIEF 第 11 节明确请求 M0~M4+ 阶段交付，沿用既有阶段定义不重新发明。

**MVP Approach:** **Experience-led + Problem-solving Hybrid**

- **主驱动**：Experience MVP —— 靠"看起来精致 + 工程上经得起拆"建立 P1a 雇主 / P1b 同行的 brand 信任
- **嵌入**：Problem-solving for P1c —— M2 起的 F1 AI 战术解读解决"看懂赛后战术"这个真实痛点

**Why this approach:**

1. 个人站不靠转化率赢，靠"工程审美"建立长期可信度 → Experience 优先
2. F1 板块是差异化命门，必须解决真问题 → Problem-solving 嵌入
3. 不做 Platform / Revenue MVP（无 SaaS / 无收费模型）

### Resource Requirements

| 资源 | 现状 |
|---|---|
| 团队规模 | 单人（boss）+ AI 协作（Claude + Codex 多 agent） |
| 时间投入 | 业余 + 周末 |
| 工作流 | BMAD V6 + Claude Code + Obsidian 追踪 |
| 关键依赖 | Vercel（部署）/ GitHub Actions（cron）/ Anthropic SDK / Turso / Jolpica F1 API |

### Phase-to-Journey Mapping

| Journey | MVP (M0+M1) | Growth (M2+M3) | Vision (M4+) |
|---|---|---|---|
| **J1 Linda（雇主）** | ✅ Home + Portfolio + Contact 完整可用；Lab demo 链接占位 | ✅ Lab demo 真上线；F1 战术解读引流 | — |
| **J2 Tom（F1 老车迷）** | ❌ F1 模块未上线，Tom 暂不可服务 | ✅ F1 全模块 + 战术解读 + 错误降级 fallback | ✅ Newsletter 订阅 |
| **J3 boss 运营** | ⚠️ MDX 手工流可走（无 cron / 无 admin） | ✅ cron + `_drafts/` + `/admin/queue` + analytics 全套 | ✅ 跨 demo 数据互通 |
| **J4 新 AI Agent** | ✅ MEMORY + BRIEF + docs/ + BMAD 闭环已具备 | ✅ sub-feature 模式可用 | ✅ 跨 agent 协作模式成熟 |

**关键观察：** MVP 阶段 J2（F1 用户）**暂不可服务**——这是有意识的延迟，不是疏忽。理由：M0+M1 优先建立 brand 与工程基础，F1 模块依赖 M2 的数据管道 + cron。

### Risk Mitigation Strategy（整合）

**Technical Risks:**

| 风险 | MVP 阶段缓解 | 整体缓解 |
|---|---|---|
| Tailwind v4 / Next.js 15 / Fumadocs 等"较新"栈兼容性 | M0 做技术 spike，遇阻塞回滚到稳定版 | Context7 持续查最新文档；breaking change 走 ADR |
| F1 数据源稳定性 | M2 启动前做数据源健康检查；多源冗余设计 | Domain Risk Mitigations 表已覆盖 |
| AI 内容质量不达标 | 战术解读人工 review 兜底 | Innovation Risk Mitigation 表已覆盖 |

**Market Risks:**

| 风险 | 缓解 |
|---|---|
| F1 中文圈对个人站冷漠 | 不靠流量验证 brand——靠 P1a / P1b 高质量低数量（≥ 3 次外部分享比 1500 UV 更重要） |
| Portfolio 看到的人少 | LinkedIn / Twitter / 个人邮件主动 share，不被动等流量 |
| Lab demo 没人玩 | 第一个 demo 与 F1 / Portfolio 主题强关联，复用现有流量 |

**Resource Risks（单人 + 业余）:**

| 风险 | 缓解 |
|---|---|
| 业余时间不够推进 | BMAD 工作流让"思考一次 + AI 自跑"；Story 闭环目标 < 5 工作日 |
| AI 调用月成本超个人预算 | `/admin/ai-usage` 看板 + 月预算阈值告警 + Opus / Sonnet 分级 |
| 一个 phase 卡住影响下个 phase | 每个 phase 出口条件明确（见下）；卡住时开 ADR 记录权衡 |
| boss 兴趣转移导致项目搁浅 | M0+M1 出口包括"半年后 10 分钟重建上下文"——保证可重启而不是死亡 |

### Phase Exit Criteria（每个 phase 何时算"完"）

- **M0 + M1 出口**：站上线 + Vercel CI 通过 + Lighthouse A11y ≥ 95 + LCP < 2.0s + **任一新 agent 读完 docs/ 后能独立提 PR 加 feature**
- **M2 + M3 出口**：F1 cron 7 日稳定率 ≥ 95% + 战术解读累计 ≥ 5 篇 + admin 看板可用 + Lab ≥ 1 个 demo 可玩
- **M4+ 持续**：无固定出口，按 Vision 列表按需推进；触发条件：流量 / 内容 / 个人方向变化

## Functional Requirements

> **Capability Contract.** 此清单是产品所有能力的权威边界。UX / Architect / Dev 只支持这里列的能力，未列即不存在；如需新增，必须显式追加。

### Core Site & Information Architecture

- **FR1**: 访客可在 zh / en 之间切换语言，URL 持久化（`/[locale]/...`），偏好持久（localStorage）
- **FR2**: 访客可通过全局导航在 Portfolio / F1 / Lab 三大板块间快速切换
- **FR3**: 系统对所有公开页面提供 a11y 基线（skip-link / 键盘焦点环 / 面包屑或层级返回）
- **FR4**: 系统对所有公开页面提供 SEO 基线（`generateMetadata` / OG 图 / JSON-LD / hreflang / sitemap / canonical）
- **FR5**: 访客可通过 Contact 入口获得 boss 联系方式（邮箱 + 社交链接）

### Hero & Brand Animation

- **FR6**: Home 首屏提供"虚拟人像 + F1 车手头盔图"开场仪式：人像作为静态背景，头盔以若隐若现的半透明态叠加
- **FR7**: 首屏鼠标移入时，头盔跟随鼠标光标轨迹通过 mask reveal 显现（鼠标停止则头盔逐渐淡去），致敬 landonorris.com
- **FR8**: 系统对核心章节标题使用 split text reveal（单词级淡入）
- **FR9**: 站点提供 Lenis 平滑滚动（全站默认开启，`prefers-reduced-motion: reduce` 时自动禁用）
- **FR10**: Home 页提供滚动驱动的头盔位移 / 旋转动画（GSAP / ScrollTrigger）
- **FR11**: Home 页提供 1-2 处 sticky 章节切换（页面级仪式动画）
- **FR12**: Portfolio "结果"段与 F1 战术解读数据点支持 Counter 累计动画（滚动到位时触发）
- **FR13**: 关键图 / 视频提供 mask reveal（滚动到位时揭示）
- **FR14**: 路由切换提供 fade 过渡（≤ 200ms，Framer Motion `AnimatePresence`）
- **FR15**: Portfolio "工具栈"行提供 Marquee 跑马灯动效
- **FR16**: 全站提供 CSS noise grain 微弱噪点纹理（CSS 实现，零 JS 成本）
- **FR17**: 所有 L2 / L3 动效在 `prefers-reduced-motion: reduce` 时降级到 L1 或瞬时

### Portfolio Showcase

- **FR18**: 访客可在 Portfolio 列表浏览所有公开作品（按时间或分类）
- **FR19**: 访客可阅读单篇作品详情，按"背景 → 做了什么 → 结果 → 回看"四段式呈现
- **FR20**: 访客可在作品详情跨链到相关 Lab demo 或 F1 文章（跨板块导流）
- **FR21**: boss 可通过 MDX + frontmatter 添加新作品，发布前 Zod 校验通过

### F1 Content Hub

- **FR22**: 访客可在 F1 首页查看当前赛季速览（积分榜前 N / 下一场倒计时 / 最新日报入口）
- **FR23**: 访客可浏览日报列表（按日期倒序）并阅读单日日报详情
- **FR24**: 访客可浏览车手 / 车队列表，并查看双语详情页（生平 + 数据 + 观点）
- **FR25**: 访客可查看车手积分榜与车队积分榜，可在两者间切换
- **FR26**: 访客可查看完整赛程与单场比赛详情（日程 / 结果 / 圈速）
- **FR27**: 访客可阅读 F1 战术解读长文，每篇显示"AI 协作 + 人工 review"标识与数据源署名
- **FR28**: 系统每日 UTC 07:00 自动从 Jolpica + 4 路 RSS 拉取数据并产出日报草稿
- **FR29**: 系统在赛后由赛历驱动产出战术解读初稿到 `_drafts/` 目录
- **FR30**: 系统在数据源失败时显示降级 fallback UI（昨日内容 + 故障提示）
- **FR31**: 访客可通过分享按钮把 F1 文章分享到外部平台，触发 `share` 埋点

### AI Lab

- **FR32**: 访客可在 Lab 列表浏览所有可交互 demo
- **FR33**: 访客可在单个 demo 页面与 AI 产品 / agent 实时交互
- **FR34**: 单个 demo 可使用独立技术栈（iframe 嵌入），共享 Lab 外壳的导航与样式
- **FR35**: 访客的 demo 交互行为可被埋点采集（`lab_demo_opened` / `lab_demo_interaction`）

### Content Authoring & Operations

- **FR36**: boss 可通过 Obsidian 编辑 markdown，git push 触发 Vercel 部署上线
- **FR37**: boss 可在 `/admin/queue` 查看待审 / 已审 / 已发布的 F1 内容队列
- **FR38**: boss 可对战术解读初稿做 review（修改观点段、加自己判断），review 完后标记发布状态
- **FR39**: 系统区分"机器自动 commit"（`[bot]` 前缀）与"人工 review 后 commit"（`[boss]` 前缀）
- **FR40**: boss 可在 cron 失败后通过 `/admin/queue` 触发手动补跑

### Analytics & Admin

- **FR41**: 系统采集核心事件（`page_view` / `page_leave` / `scroll_depth` / `click` / `external_link_clicked` / `locale_switch` / `share` / `error`）。**注：不再包含 `theme_toggle`，因为去掉了明暗切换**
- **FR42**: 系统采集 F1 特定事件（`f1_daily_opened` / `f1_daily_read_through` / `f1_driver_viewed` / `f1_team_viewed` / `f1_race_viewed` / `f1_analysis_viewed` / `f1_standings_filter`）
- **FR43**: 系统采集 Portfolio / Blog / Lab 特定事件（`portfolio_*` / `blog_*` / `lab_demo_*`）
- **FR44**: 系统采集 Hero 区交互事件（`hero_helmet_revealed` / `hero_helmet_track_dwell_ms`）—— 量化首屏标志性动画的吸引力
- **FR45**: boss 可在 `/admin/analytics` 查看 PV / UV / 国家 / 设备 / referrer / CWV
- **FR46**: boss 可在 `/admin/f1` 查看 F1 数据健康（cron 状态 / 数据源覆盖率 / 最近失败）
- **FR47**: boss 可在 `/admin/ai-usage` 查看 AI 调用月度成本与阈值告警状态
- **FR48**: 所有 `/admin/*` 路由通过 Basic Auth 保护，未授权返回 401，不入站点导航与 sitemap

### Privacy & Compliance

- **FR49**: 访客的 visitorId 使用 localStorage UUID 生成（**非 Cookie**）
- **FR50**: 系统不存访客 IP，仅通过 Vercel 边缘节点取国家代码
- **FR51**: 系统在 `Do Not Track: 1` 时停止采集自定义事件
- **FR52**: 访客可在 `/privacy` 页面查看隐私政策并选择 opt-out
- **FR53**: 系统对采集事件执行 90 天滚动留存；不使用第三方 analytics（GA / 百度）；除 locale 偏好外不用 Cookie

### Resilience & Operations Health

- **FR54**: 系统在 cron 失败时向 boss 发送告警（邮件 / 企业微信）
- **FR55**: 系统对 AI 调用月度预算设置阈值告警（90% 邮件，100% 暂停非关键调用）
- **FR56**: 系统对所有路由提供 `error.tsx` / `not-found.tsx` / `loading.tsx` 骨架占位
- **FR57**: 系统对 F1 数据源采用多源冗余（4 路 RSS 任一可用即继续管道）

### AI Agent Workflow Support

- **FR58**: 项目提供 AI agent 入口接力点：`MEMORY.md` + `PROJECT_BRIEF.md` + `docs/index.md` + ADR 列表 + 当前 PRD
- **FR59**: 项目支持 BMAD V6 完整工作流（PRD → architecture → ux-design → epics-and-stories → dev-story → code-review → e2e → retrospective）
- **FR60**: BMAD `_bmad-output/` 所有 step file 可恢复（frontmatter `stepsCompleted` 数组）
- **FR61**: 项目支持 sub-feature 模式：子 feature 可从 PROJECT_BRIEF 衍生小 PRD，沿用既有 ADR 不重新发明

## Non-Functional Requirements

### Performance

- **NFR1 — Core Web Vitals**: LCP p75 < 2.0s（S 级 < 1.8s）/ INP < 200ms / CLS < 0.1。验证：Vercel Speed Insights 7 日滚动指标
- **NFR2 — JS Budget**: 首屏 ≤ 200KB gzipped；动效库总和（GSAP + ScrollTrigger + Lenis + Framer Motion）≤ 80KB gzipped。验证：CI bundle analyzer 红线
- **NFR3 — TTFB**: Edge runtime < 200ms p75 / Node runtime < 500ms p75。验证：Vercel Speed Insights
- **NFR4 — Hero 动画 60fps**: 首屏头盔 mask reveal 必须 60fps 不掉帧，使用 GPU 加速 transform / opacity。验证：Chrome DevTools Performance + Lighthouse

### Security

- **NFR5 — Secret 管理**: Anthropic API Key / Turso 连接串 / Admin 密码全部存 Vercel 环境变量；不进 git；不在 client bundle 暴露（CI build 检查）
- **NFR6 — Admin 鉴权**: `/admin/*` HTTP Basic Auth；密码 ≥ 16 字符；失败 5 次锁定来源 IP 1 小时
- **NFR7 — 数据库访问**: Turso 仅在服务端 route handler 写入；client 端不直接连数据库
- **NFR8 — CSP / XSS**: Content-Security-Policy header 限制脚本来源；Lab demo iframe `src` 走白名单

### Reliability

- **NFR9 — Cron 稳定**: GitHub Actions cron 7 日成功率 ≥ 95%；单次失败自动重试 3 次（指数退避 10s / 60s / 300s）；3 次都失败才告警
- **NFR10 — F1 数据降级**: 数据源失败时显示 fallback UI（昨日内容 + 故障提示），不返 5xx，不让站崩
- **NFR11 — AI 调用 fallback**: Claude 调用失败时，日报降级为"原始 RSS 摘要 + 数据源链接"；战术解读队列不写入
- **NFR12 — 服务中断**: Vercel / GH Actions 中断时静态部分（SSG 页面）继续可访问；ISR 路由 fallback 到上一成功版本

### Accessibility

- **NFR13 — WCAG 2.2 AA**: 全站达标；Lighthouse A11y ≥ 95；CI 跑 `@axe-core/playwright`，违规 = build 失败
- **NFR14 — 键盘 + 焦点**: 所有交互可键盘到达（Tab / Shift+Tab / Enter / Space）；焦点环可见；每页提供 skip-link
- **NFR15 — 屏幕阅读器 + 色彩**: landmark roles 完整（`<header>` / `<nav>` / `<main>` / `<aside>` / `<footer>`）；ARIA 仅在原生语义不足时使用；文字 ≥ 4.5:1，大字 ≥ 3:1，UI 元素 ≥ 3:1
- **NFR16 — 降级动效**: `prefers-reduced-motion: reduce` 时 L2 / L3 动效降级到 L1（CSS transition < 200ms）或瞬时；**Hero 鼠标 mask reveal 在 reduced-motion 时降级为静态显示头盔图**

### Integration

- **NFR17 — Jolpica 契约监控**: 每日 cron 校验关键字段是否齐全（车手 ID / 车队 ID / 圈速 / 积分）；schema 变更触发人工介入告警
- **NFR18 — RSS 多源冗余**: 4 路 RSS（F1 官方 / Motorsport / The Race / Reddit）任一可用即继续日报；4 路全失败才触发告警
- **NFR19 — Anthropic SDK 版本**: Sonnet 4.6 用于摘要 + 翻译；Opus 4.7 用于战术解读长文；模型版本变更走 ADR 流程
- **NFR20 — Turso 边缘性能**: 读延迟 p95 < 100ms（边缘节点）；所有写操作仅服务端

### Maintainability

- **NFR21 — BMAD 闭环**: 任何新 feature 必须走完整 BMAD V6 流程（PRD → architecture → ux-design → epic → story → dev-story → code-review → e2e → retrospective）；跳步必须 ADR 记录原因
- **NFR22 — 文档自更新**: PRD `stepsCompleted` 即时更新；docs/ 中 ADR / 横切规范变更时与代码同步
- **NFR23 — Story 闭环时长**: PRD → 上线全流程 **< 5 工作日 / story**（含前后端 + 测试 + code review）
- **NFR24 — 测试覆盖**: 核心业务逻辑 Vitest 单元测试覆盖率 ≥ 80%；Playwright E2E 覆盖关键 user journey（J1 / J2 / J3）；Home + Portfolio 详情过视觉回归（截图对比）
