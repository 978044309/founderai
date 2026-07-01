# AI Workforce

AI Workforce（AI 劳动力网络）MVP。它不是招聘平台，也不是普通兼职平台；企业按结果调用可调度的 AI 增强劳动力，个人用技能接入网络获得收入。系统自动拆解需求、生成建议报价、匹配合适执行者，并把任务、人才、匹配记录汇总到管理后台。

## 运行

```bash
pnpm install
pnpm dev
```

打开 `http://localhost:3000`。

## MVP 页面

- 首页：平台定位与业务流程介绍
- 企业端发布任务：标题、描述、预算、截止时间、技能、AI 拆解、AI 建议报价
- 个人端资料：姓名、技能标签、可工作时间、期望收入、过往经验
- 任务大厅：任务列表，支持按技能、预算、截止时间筛选
- AI 匹配结果：推荐人才、匹配理由、推荐执行步骤
- 管理后台：企业任务、个人用户、匹配记录

## 项目结构

```text
app/
  globals.css          全局样式和 Tailwind 组件类
  layout.tsx           页面元信息和根布局
  page.tsx             MVP 主应用和六个核心页面
lib/
  mockAi.ts            模拟 AI 拆解、报价和匹配逻辑
  types.ts             核心业务类型
docs/
  database-design.sql  SQLite-first 数据库字段设计
```

## 数据与后端说明

当前版本支持两种模式：

- 未配置 Supabase：使用 `localStorage` 保存演示数据。
- 已配置 Supabase：用户可用邮箱密码注册/登录，任务、个人资料和匹配记录保存到云端数据库。

模拟 AI 逻辑位于 `lib/mockAi.ts`。

## 启用网上注册

1. 在 Supabase 创建项目。
2. 打开 Supabase SQL Editor，执行 `docs/database-design.sql`。
3. 在本地复制 `.env.example` 为 `.env.local`，填入：

```bash
NEXT_PUBLIC_SUPABASE_URL=你的 Supabase Project URL
NEXT_PUBLIC_SUPABASE_ANON_KEY=你的 Supabase anon public key
```

4. 在 GitHub 仓库 Settings → Secrets and variables → Actions 中添加同名 secrets：

```text
NEXT_PUBLIC_SUPABASE_URL
NEXT_PUBLIC_SUPABASE_ANON_KEY
```

5. 推送到 `main` 后 GitHub Pages 会重新构建，公网版本即可注册/登录。
