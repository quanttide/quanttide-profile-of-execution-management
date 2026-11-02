# qtcrowd

## 定位

量潮联盟的 qtcrowd 业务，收口下线：信息迁往 quanttide-learn，qtcrowd 逐步下线。

> 变更（2026-08-27）：原计划「往 qtclass 上线」取消——课堂打算围绕课程体系重新做，任务书不放课堂上了。

## 重点（O/KR）

- **O**：qtcrowd 平稳收口，信息迁往 quanttide-learn。
  - KR1：6 个任务档案全部迁移完成 — 当前：未开始（卡在任务书格式拍板）
  - KR2：站点与线上资产下线（deploy workflow、CDN/DNS、FC provider） — 当前：未开始，依赖 KR1
  - KR3：不可逆收尾（删 OSS 桶、archive 仓库）经确认后执行 — 当前：未开始

## 背景（调研实况）

- crowd 的 profile（quanttide-profile-of-crowd-sourcing）是 qtcrowd 站点的数据源：6 个任务档案（业务/类别/状态 + 固定小节格式），按来源第二大脑分目录，站点 tasks.json 由 `scripts/sync-tasks.mjs` 从档案生成。
- 接收侧 learn profile（quanttide-profile-of-learning-management）的 `tasks/` 用 frontmatter 格式，与 crowd 小节格式不同。
- qtcrowd 线上资产：CDN 域名 `crowd.quanttide.com` + quanttide.com DNS 记录、站点 OSS 桶、FC 函数 qtcrowd-provider（桶为手动创建）、仓内 `deploy-site`/`deploy-provider` workflow；同一仓库被 `domains/quanttide-crowd/apps/qtcrowd` 与 `defaults/quanttide-alliance/apps/qtcrowd` 两处引用。
- ~~qtclass 为现成上线目标~~：已取消（课堂将围绕课程体系重新做），site `class.quanttide.com`、studio `studio.class.quanttide.com` 与本任务无关。

## 任务分解（顺序即依赖）

### 第一步：信息转移（crowd → learn）

1. 清点 6 个档案现状：2 个进行中（第二大脑创建插件、项目复盘系统），4 个待认领
2. 定迁移格式（待拍板，见下）
3. 逐文件迁移到 learn profile
4. crowd 侧收尾：更新 crowd profile README/AGENTS.md 口径，标记移交
5. 分层提交：learn profile → learn 域仓；crowd profile → crowd 域仓；两域仓指针 → quanttide 根仓

### 第二步：逐步下线 qtcrowd

1. 确认站点无未决认领
2. 禁用/删除 qtcrowd 仓的 deploy-site、deploy-provider workflow，停止继续发布
3. terraform 下线：CDN 域名 + quanttide.com DNS 记录 + FC provider
4. 移除两处子模块引用 + 更新相关 README
5. 不可逆收尾（单列，执行前停下确认）：删除 OSS 桶（站点桶 + qtcrowd-provider 桶）、archive qtcrowd 仓库

## 待拍板

1. 任务书转不转 learn 的 frontmatter 格式？（转=站点解析格式失效但符合 learn 约定；不转=只挪位置保留原格式）

已定：

- ~~往 qtclass 上线~~：取消，课堂将围绕课程体系重新做
- qtcloud-crowd：不在本次范围，只下线 qtcrowd

## 当前状态

- 三个 KR 均未动；第一步卡在任务书格式拍板（见下方「待拍板」）。
