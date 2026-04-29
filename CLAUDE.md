# CLAUDE.md — planet-xlu（本地代号 myspace）

> 任何 AI agent 接手前必读。**< 200 行硬约束**——超过就精简，不增 lint。
> 三类内容：① 怎么干 ② 命名约定 ③ 永远不要做 X
> 想看完整愿景与 FR/NFR：读 `PROJECT_BRIEF.md` + `_bmad-output/planning-artifacts/prd.md`

## 0. 接力入口

新 agent 进来按顺序读：
1. **本文件**（30 秒看完做事）
2. `PROJECT_BRIEF.md`（357 行权威输入）
3. `_bmad-output/planning-artifacts/prd.md`（11 章节 / 61 FR / 24 NFR）
4. `~/Library/Mobile Documents/iCloud~md~obsidian/Documents/ai-Knowledge/myspace-项目/README.md`（跨会话叙事接力）

## 1. 怎么干（构建命令）

```bash
# 包管理（强制 pnpm，禁 npm/yarn）
pnpm install
pnpm dev               # Next.js dev server
pnpm build             # 生产构建（含 type check）
pnpm lint              # eslint + prettier
pnpm typecheck         # tsc --noEmit

# 测试三层
pnpm test              # Vitest 单元 + 组件
pnpm test:e2e          # Playwright E2E（核心 user journey）
pnpm test:a11y         # @axe-core/playwright（CI 红线）
pnpm test:visual       # Playwright 截图回归（Home + Portfolio 详情）

# Design Tokens
pnpm tokens:build      # W3C DTCG → Tailwind config + CSS vars + TS types

# Bundle 监控
pnpm analyze           # bundle analyzer（首屏 ≤ 200KB gzipped 红线）
```

## 2. 命名约定

### 路由（Next.js 15 App Router）
- 路由组：`(public)` / `(admin)` / `[locale]` 三层
- 文件：`page.tsx` / `layout.tsx` / `error.tsx` / `not-found.tsx` / `loading.tsx`
- 特殊：`/admin/*` 必须 Basic Auth，必须 `disallow` 进 `robots.ts`

### 组件
- 路径：`components/{ui,sections,brand,a11y}/PascalCase.tsx`
- `ui/`：shadcn 复制粘贴的基础原子（不是 npm 依赖）
- `sections/`：页面级大块（HeroHelmet / PortfolioGrid 等）
- `brand/`：法拉利红 + 头盔 + Marquee 等品牌动效
- `a11y/`：SkipLink / FocusRing / ReducedMotionGuard

### Story（BMAD V6）
- 格式：`feat-<area>-<verb>-<short>` 例 `feat-home-helmet-mask-reveal`
- Story spec：`_bmad-output/implementation-artifacts/{story-id}.md`
- Acceptance criteria 必须 testable

### E2E
- 路径：`tests/e2e/<route>.spec.ts`
- 命名：`route + verb + outcome` 例 `home.helmet-cursor-reveals.spec.ts`
- **每个 story 至少 1 条 happy path + 1 条主要 error case**

### Commit
- Conventional Commits（`feat` / `fix` / `chore` / `docs` / `refactor` / `test`）
- 自动 commit（cron 写入）前缀 `[bot]`；人工 review 后 commit 前缀 `[boss]`（见 ADR 0008）
- Squash and merge

### 分支 / Worktree
- 主分支 `main`（保护，必须过 PR + CI）
- Story 分支 `feat/<story-id>` 或 `fix/<story-id>`
- 多 agent 并行用 `git worktree add ../planet-xlu-<story-id>`

## 3. 工作流（轻量化 BMAD V6 + Anthropic 节奏）

```
PRD ✅ → architecture.md (≤150 行) → ux-design (prototype-first) →
GitHub Issues 拆 epic/story → 单 story 循环：
  ① 先写 Playwright E2E + AC（契约）  ← 测试先行
  ② Claude/Codex 在 worktree 全栈实现 ← 不分前后端
  ③ CI: 测试 + axe + 视觉回归         ← 自验证
  ④ 测试全过 → PR → merge
  ⑤ 踩坑 → Claude 自己写回本文件 §4   ← Compounding
```

## 4. 永远不要做 X（每次踩坑就追加一条）

### 工程
- **永远不要**用 npm 或 yarn —— 强制 pnpm（ADR 0007）
- **永远不要**用 cookie 存用户偏好 —— 除 locale 外全部 localStorage（NFR Privacy）
- **永远不要**写完代码再写 E2E —— 测试先写当契约（ADR 0010）
- **永远不要**前端 agent / 后端 agent 分开跑 —— 一个 agent 跑全栈（ADR 0010）
- **永远不要**让 client 直连 Turso —— 写操作仅服务端 route handler（NFR7）
- **永远不要**把 Anthropic API key / Turso 连接串 / Admin 密码进 git —— 走 Vercel env（NFR5）
- **永远不要**`--no-verify` 跳 git hook，除非 boss 明确说

### 视觉与动效
- **永远不要**做明暗主题切换 —— 单一深色（ADR 0009）
- **永远不要**用橙色 / Papaya / McLaren 致敬 —— 主题色是法拉利红 #DC0000（ADR 0009）
- **永远不要**做 cursor 磁吸（被吸附）/ 全屏 scroll-jacking / 3D WebGL 头盔 —— BRIEF 第 4 节明确不取
- **永远不要**忽略 `prefers-reduced-motion: reduce` —— L2/L3 动效必须降级到 L1 或瞬时（NFR16）

### 内容与合规
- **永远不要**爬白名单外的 F1 站 —— 仅 Jolpica + 4 路 RSS（Domain Compliance）
- **永远不要**让 AI 战术解读自动发布 —— 必须人工 review（D009 + Innovation Risk）
- **永远不要**冒充人工原创 —— AI 内容必须显式标注"AI 协作 + 人工 review"（FR15 / FR27）
- **永远不要**存访客 IP —— 仅取国家代码（NFR Privacy / FR37）
- **永远不要**接 GA / 百度 / Session Replay（FR40）

### Agent 协作 / 上下文管理
- **永远不要**打字纠正 Claude（"不对，应该 X"）—— `Esc Esc` 回退到上一个 prompt 重写（feedback_workflow_anthropic）
- **永远不要**硬推连续出错的实现 —— 出错 2 次立刻退回 Plan mode re-plan
- **永远不要**在不可逆操作（删数据 / 推线上 / 付费调用）前不问 boss
- **永远不要**重新发明 BRIEF / PRD / ADR 已经决定的事 —— sub-feature 沿用既有决策（ADR 0006 + 0012）
- **永远不要**让 PRD `stepsCompleted` frontmatter 跟磁盘状态分裂 —— 每 step 完成立即更新

### 性能 / a11y 红线
- **永远不要**让首屏 JS > 200KB gzipped；动效库总和 > 80KB gzipped（NFR2）
- **永远不要**让 LCP S 级页面 > 1.8s / A 级 > 2.0s（NFR1）
- **永远不要**让 Lighthouse A11y < 95 或 axe-core 报错过 build（NFR13）

## 5. 上下文管理（跨会话）

- 一次对话只做一件事；上下文 50% 主动收束开新对话
- 完成 milestone 回 Obsidian README 更新
- BMAD step file 的 `stepsCompleted` 是机器接力点；Obsidian README 是人 + agent 双受众叙事接力点
- 不可逆操作（删数据 / 推线上 / 付费调用）必须停下问 boss

## 6. 项目代号约定

- GitHub 仓库：`xxxxlu/planet-xlu`
- 本地目录：`~/Desktop/project-web/myspace/`（保留旧名不动，避免 IDE 重建）
- 代号：**planet-xlu**（一切文档 / config / agent 内部）
- 矛盾时以 GitHub 仓库名为准
