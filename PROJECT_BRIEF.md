# PROJECT BRIEF — myspace

> boss 个人综合站项目的完整需求 + 已落决策汇总。
> 给 BMAD V6 工作流当**单一权威输入**。
> 凡是这份文件没说的，让 BMAD 通过 `bmad-product-brief` / `bmad-create-prd` 等 skill 在对话中向 boss 澄清。
>
> **作者：** 星期五（Claude）
> **日期：** 2026-04-28
> **状态：** Source of Truth
> **语言：** 中文
> **协作模式：** boss + AI agents（Claude + Codex + 未来）
>
> ---

## 0. 一句话项目愿景

> **"工程师的审美标本"** —— boss 的个人综合站，三合一：作品集 + F1 内容站 + AI 实验室。

## 1. 项目身份

- **代号**：`myspace`（暂定，未来可改）
- **路径**：`~/Desktop/project-web/myspace/`
- **类型**：个人站（非 SaaS、非 B2B）
- **状态**：从 0 开始，本次重启

## 2. 三大板块（Three Pillars）

### 2.1 Portfolio — 作品集 + 博客 + About
- 个人项目案例展示
- 博客（技术文 / 观点文）
- About / Contact

**叙事要求：** 每个作品按"背景 → 做了什么 → 结果 → 回看"四段式。可量化指标必须给。质 > 量。

### 2.2 F1 — F1 内容中心（重点，是迷你产品）
完整子模块：
- **F1 首页**：当前赛季速览 + 最新日报 + 倒计时
- **F1 日报**：每日聚合 + AI 摘要（**自动生成**，每天 UTC 07:00 跑）
- **车手列表 + 详情**（生平 + 数据 + 双语简介）
- **车队列表 + 详情**（历史 + 阵容 + 数据 + 品牌色）
- **积分榜**（车手 / 车队 切换）
- **赛程**
- **比赛详情**（日程 / 结果 / 圈速）
- **AI 战术解读**：赛后由 Claude 生成的长文，**人工 review 后发布**（差异化关键）

**数据源**（白名单）：
- Jolpica-F1 API（赛果 / 排位 / 车手 / 积分等结构化数据）
- F1 官方 RSS
- Motorsport.com RSS
- The Race RSS
- Reddit r/formula1 Top 1d（辅助）

### 2.3 Lab — AI 实验室
- AI 可交互 demo 展示
- 第一个 demo 建议和 F1 / Portfolio 主题相关（如 "F1 战报对话式问答"）
- 允许单 demo 用独立栈（iframe 嵌入）

## 3. 目标用户

| 画像 | 描述 | 核心诉求 |
|---|---|---|
| **P1a 潜在合作方 / 雇主** | 第一次访问，3 分钟判断 | 看作品 + 工程深度 |
| **P1b 同行 / 爱好者** | 看 demo 玩、读博客 | 技术细节、可玩性 |
| **P1c F1 读者** | 搜索进来 | 有观点的内容、不只是聚合 |
| **P2 boss 自己** | 内容创作 + 数据查看 | 更新流畅、AI 协作顺、半年后看得懂 |
| **P0.5 AI Agent** | Claude / Codex / 未来 | 规范无歧义、流程明确 |

## 4. 视觉设计方向

- **核心参考**：[landonorris.com](https://landonorris.com)（仪式感开场、大字号衬线、滚动驱动、**首屏鼠标轨迹头盔 mask reveal**、法拉利红品牌时刻）
- **借鉴**：Google Material 3 的系统化（动效时序 / 排版规范 / 色彩 tokens）
- **取**：情绪 + 节奏 + 大字 + 留白 + 鼠标轨迹 mask 效果 + 滚动驱动头盔位移
- **不取**：cursor 被吸附磁吸 / 全屏 parallax / scroll-jacking

### 品牌方向
- **品牌色**：**法拉利红 Rosso #DC0000**（致敬 Scuderia Ferrari 跃马，全站点缀色 + 关键 CTA + hover 状态）
- **基调**：**单一深色主题**（黑底 + 纸白字 + 法拉利红点缀）；**不做明暗切换**
- **字体**：英文衬线 Fraunces Variable + 英文 Sans Inter；中文 霞鹜文楷 + 鸿蒙 Sans SC；等宽 JetBrains Mono
- **品牌人格**：克制、专业、有态度、有幽默
- **首屏标志性元素**：**虚拟人像**（boss 的角色化形象，非真实照片）+ **F1 车手头盔图**（若隐若现叠加）+ **鼠标轨迹 mask reveal**（鼠标移入触发头盔跟随轨迹显现，参考 landonorris 首屏交互）
- **禁忌**：模板化插画、AI 生成的烂大街风格、彩虹渐变

### 双语
- 中文 + 英文，路由 `/[locale]/...`
- MDX 长文双文件 `xxx.{zh,en}.mdx`
- UI 字符串 next-intl messages
- 结构化数据字段双语对象 `{ zh, en }`

## 5. 技术栈（已选定，可作为 BMAD architect 输入直接采纳）

### 框架与运行时
- **Next.js 15 App Router** + TypeScript strict
- **pnpm** 包管理器
- 单仓库（不拆 monorepo）
- Vercel 部署 + Edge / Node Runtime

### UI / 样式 / 动效
- Tailwind CSS v4
- shadcn/ui（复制粘贴，不是依赖）
- **Design Tokens**：W3C DTCG 格式 → style-dictionary 编译 → Tailwind config + CSS vars + TS 类型
- 动效三层：CSS（L1）+ Framer Motion（L2）+ GSAP/ScrollTrigger/Lenis（L3）
- L3 在一个页面最多出现 1-2 处

### 国际化
- next-intl

### 内容
- **MDX 引擎：Fumadocs MDX**（待 boss 拍板，推荐）
- frontmatter 走 Zod 校验

### 数据契约
- Schema：Zod
- API 契约：OpenAPI 3.1 YAML
- 类型生成：openapi-typescript

### 后端 / API
- Next.js Route Handlers
- Anthropic SDK（Claude Sonnet / Opus）做 F1 摘要 + 战术解读 + 翻译

### 定时任务
- GitHub Actions Cron（**不**用 Vercel Cron，超时受限）
- F1 日报 cron `0 7 * * *` UTC
- F1 赛后结果 cron 由赛历驱动
- 自动 commit 回仓库 → Vercel 自动部署

### 测试
- Vitest（单元 / 组件）
- Playwright（E2E）
- @axe-core/playwright（a11y）

### 监控
- Vercel Analytics + Speed Insights（M1 起）
- Sentry（M2 起）
- GH Actions 邮件 / 企业微信告警

### 工作流
- **BMAD Method V6**（feature 工作流，已确定）
- 项目级横切规范走 `docs/`（待重建）

## 6. 数据 & 隐私

### 内容存储
- M1-M2：MDX + JSON 文件落盘（git 即数据库）
- M3+ 量大时：Turso (SQLite on edge) 或 Postgres

### 访客分析（重要）
**三层分工：**

| 阶段 | 工具 | 看什么 |
|---|---|---|
| M1 起 | **Vercel Analytics + Speed Insights** | PV / UV / 国家 / 设备 / referrer / CWV |
| M2 起 | **自建 `/api/track` + Turso** | 自定义事件（读完率、漏斗、按维度切片）+ 匿名 visitorId |
| M3 起 | **`/admin/*` 只读看板（Basic Auth 保护）** | 数据可视化 + F1 数据健康 + 待审队列 + AI 成本 |
| M4+ | PostHog（观望） | 量大才考虑 |

### 关键事件清单
- 核心：`page_view` / `page_leave` / `scroll_depth` / `click` / `external_link` / `locale_switch` / `theme_toggle` / `share` / `error`
- F1：`f1_daily_opened` / `f1_daily_read_through` / `f1_driver_viewed` / `f1_team_viewed` / `f1_race_viewed` / `f1_analysis_viewed` / `f1_standings_filter`
- Portfolio：`portfolio_opened` / `portfolio_live_clicked` / `portfolio_repo_clicked`
- Blog：`blog_opened` / `blog_read_through`
- Lab：`lab_demo_opened` / `lab_demo_interaction`

### 隐私边界
- ✅ 匿名 `visitorId`（localStorage UUID，**不是 cookie**）
- ✅ 不存 IP，仅取国家代码
- ✅ 尊重 `Do Not Track` + 提供 `/privacy` opt-out
- ❌ Session Replay（默认关）
- ❌ 第三方 analytics（GA / 百度）
- ❌ Cookie（除 locale 偏好）

## 7. 性能 & 质量约束

### Core Web Vitals 目标（p75）
- **LCP < 2.0s**（S 级页面 < 1.8s）
- **INP < 200ms**
- **CLS < 0.1**

### JS Budget
- 首屏首次加载 ≤ 200 KB gzipped
- 动效库（GSAP + ScrollTrigger + Lenis + Framer Motion）总 ≤ 80 KB gzipped

### 无障碍
- **WCAG 2.2 AA** 全站达标
- Lighthouse A11y ≥ 95
- 键盘 100% 可达、焦点可见、prefers-reduced-motion 降级

### 页面分级
- **S 级**（Home / F1 首页 / Portfolio 列表）：像素级雕琢 + 动效 + LCP < 1.8s
- **A 级**（重点落地页）：精致 + LCP < 2.0s
- **B 级**（标准页）：符合规范 + LCP < 2.2s
- **C 级**（辅助页）：够用 + LCP < 2.5s

## 8. 工作流 & 协作

### Feature 工作流：BMAD V6
每个 feature 走：
```
bmad-brainstorming / bmad-product-brief（可选）
  → bmad-create-prd
  → bmad-validate-prd
  → bmad-create-architecture
  → bmad-create-ux-design
  → bmad-create-epics-and-stories
  → bmad-check-implementation-readiness
  → bmad-create-story
  → bmad-dev-story
  → bmad-code-review / bmad-review-edge-case-hunter
  → bmad-qa-generate-e2e-tests
  → bmad-retrospective
```

### 项目规范
- 横切规范放 `docs/`（之前已写过 81 个文件，本次需重建）
- Feature 产出放 `_bmad-output/`
- 决策记录走 ADR（Michael Nygard 格式）
- 变更日志走 Keep a Changelog

### Git
- main 分支保护，必须过 PR + CI
- Conventional Commits
- Squash and merge

## 9. 协作规则（boss 个人偏好，必须遵守）

- **称呼**：所有 AI 对话以 "boss" 开头
- **语言**：中文为主，关键术语保留英文（LoRA / RAG / DRS）
- **风格**：先给可执行清单，再讲原理；不教学式解释；直给方案
- **节奏**：默认直接干，干完汇报；只在需求模糊或不可逆操作时停下确认
- **输出**：先给"下一步"，再给原理；尽量给"常见坑 + 评估指标 + 模板"
- **多 agent**：Claude 主写代码 / 批量改动；Codex 做对手戏 review、找逻辑漏洞、收边界

## 10. 明确不做的（Negative Scope）

❌ **登录系统 / 用户账号**（个人站不需要）
❌ **CMS（增删改查 UI）** —— MDX + Git + Obsidian + VS Code 已是最优解
❌ **评论 / 点赞 / 分享计数** —— 反垃圾成本 > 收益
❌ **付费 / 会员**
❌ **App / 小程序 / 桌面端**
❌ **PWA**（M3+ 才评估）
❌ **第三方 analytics**（GA / 百度）
❌ **Session Replay**（隐私风险）
❌ **大型搜索系统**（M3+ 视需求加 minisearch / Algolia）
❌ **F1 实时数据流**（轮询足够）
❌ **追求 SEO 流量峰值** / 内容农场化

## 11. Roadmap（里程碑，不是时间表）

| Milestone | 目标 | 出口条件 |
|---|---|---|
| **M0** | 架构与规范 | docs/ 完整 + BMAD 装好 + 工作流闭环；任何新 AI 读完能独立加 feature |
| **M1** | 项目骨架 + Home + Portfolio | Vercel 上线、tokens 生效、3-5 份作品 MDX、双语切换可用 |
| **M2** | F1 模块 + 自建埋点 | 连续 7 天稳定产日报、车手/车队/积分榜可用、`/api/track` + Turso 跑通 |
| **M3** | AI Lab + Admin 看板 | 至少一个可交互 demo、`/admin/*` 数据可视化 |
| **M4+** | 持续进化 | 评估 PostHog、博客系列、全站搜索、视情况升级 |

## 12. 已落决策（8 条 ADR — 本次重启沿用）

| ID | 决策 | 选择 |
|---|---|---|
| 0001 | 主框架 | Next.js 15 App Router + TS |
| 0002 | 仓库结构 | 单仓库 |
| 0003 | i18n | next-intl |
| 0004 | 定时任务 | GitHub Actions Cron |
| 0005 | Design Tokens | W3C DTCG + style-dictionary |
| 0006 | Feature 工作流 | BMAD V6 |
| 0007 | 包管理器 | pnpm |
| 0008 | 埋点 + Admin | 自建 `/api/track` + Turso + `/admin` 只读看板，**不做 CMS** |

新 session 重建 docs/ 时，把这 8 条 ADR 一起重建。

## 13. 待决策（Open Questions）

| # | 问题 | 倾向 | 必须决的时间 |
|---|---|---|---|
| D002 | **MDX 引擎** | **Fumadocs MDX** | 项目初始化前 |
| D003 | 字体最终确认 | Fraunces + 霞鹜文楷 + Inter + 鸿蒙 + JetBrains Mono | 做 Home 前 |
| D006 | F1 新闻聚合源最终白名单 | Jolpica + F1 官方 + Motorsport + The Race + 有限 Reddit | M2 启动前 |
| D007 | 域名 | 暂用 Vercel 默认子域 | M1 上线前 |
| D009 | F1 战术解读发布是否全自动 | 否，必须人工 review | M2 启动前 |

## 14. 信息架构（站点路由总览）

```
/[locale]/                    zh | en
├── /                          Home
├── /about
├── /contact
├── /portfolio                 列表
│   └── /portfolio/[slug]      详情
├── /blog
│   └── /blog/[slug]
├── /f1                        F1 首页
│   ├── /f1/daily              日报列表
│   │   └── /f1/daily/[date]
│   ├── /f1/drivers
│   │   └── /f1/drivers/[slug]
│   ├── /f1/teams
│   │   └── /f1/teams/[slug]
│   ├── /f1/standings
│   ├── /f1/calendar
│   ├── /f1/races/[slug]
│   ├── /f1/analysis
│   │   └── /f1/analysis/[slug]
│   └── /f1/season/[year]
├── /lab
│   └── /lab/[slug]
├── /admin                     口令保护，不在导航
│   ├── /admin/analytics
│   ├── /admin/f1
│   ├── /admin/queue
│   └── /admin/ai-usage
└── /privacy

/api/
├── /api/f1/...
├── /api/track                 埋点
├── /api/admin/analytics/...   Basic Auth
├── /api/og/[kind]             动态 OG
└── /api/revalidate
```

## 15. boss 的偏好提醒（给 AI 的元层）

- 探索新东西，不喜欢被框架限制
- 工程场景直接给方案 + 代码，不要教学语气
- AI 时代技术栈不重要，但工程品味重要
- F1 类比能讲清概念时优先用（调参=赛车设定）
- 涉及"最新赛事 / 库版本"时，主动说"建议查文档"
- 探索性项目允许大胆尝试，做不下去开 ADR 记录权衡

## 16. 给 BMAD 的元指令（新 session 启动时，agent 要做的）

1. 读完本 BRIEF
2. 调用 `bmad-help`（或检查 `_bmad-output/` 现状）判断当前阶段
3. 推进顺序建议：
   - 第一步：用 `bmad-create-prd` 把本 BRIEF 展开成 Portfolio / Home 的 PRD（M1 第一个 feature）
   - 第二步：`bmad-create-architecture` 出技术方案
   - 第三步：`bmad-create-ux-design` 出 UX 细节
   - 第四步：`bmad-create-epics-and-stories` 拆 story
   - 第五步：先做项目脚手架（不是某个 feature 的 story，是 infra），再做第一个 feature
4. 如果 boss 让"开始建 docs/" → 按本 BRIEF + 8 条 ADR 重建横切规范
5. 不要重新发明已经决定的事情；ADR 没说的可以问

## 17. 文件清单（新 session 接入点）

| 路径 | 状态 | 用途 |
|---|---|---|
| `PROJECT_BRIEF.md`（本文件） | ✅ 现存 | 单一权威输入 |
| `_bmad-output/` | 部分存在 | feature 产出目录 |
| `_bmad/` | ❌ 需重装 | BMAD 本体 |
| `docs/` | ❌ 需重建 | 横切规范 |
| `.claude/skills/bmad-*` | ❌ 需重装 | BMAD skills |

---

**END OF BRIEF**

如果 boss 想从这份文件开始，告诉新 session 的 AI："先读 PROJECT_BRIEF.md，再决定下一步。"
