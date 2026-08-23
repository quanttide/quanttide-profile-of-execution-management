# AGENTS.md — 执行档案（profile）仓库约定

> 供 Agent/协作者查阅的本仓库目录与维护约定。

## 仓库定位

执行档案（quanttide-profile-of-execution-management）：按 **业务 × 职能** 记录量潮各业务的执行情况。脱敏公开版——只含产品/技术事实；人事/客户/治理细节保留在私有仓库。

## 目录结构

```
docs/   # 人类可读的执行档案·叙事
  qtdata/   # 量潮数据：客户项目复现、数据产品
  qtclass/  # 量潮课堂：实训基地招聘运营、课堂创新
  qtcloud/  # 量潮云：平台建设、三朵云、业务云
data/   # 机器可读的种子数据·状态
  tasks.json
README.md
LICENSE
```

- `docs/` — 按 `业务（qtdata|qtclass|qtcloud）× 职能（product|operation|business）` 组织，每个业务含 `index.md`（定位/重点/当前状态）+ 职能档案。是「发生过什么、当前进展」的**叙述**来源。
- `data/` — `tasks.json` 是**结构化任务清单**，是机器可读的唯一事实源。部署时注入，运行时作为活数据持续维护（含服务端 upsert 写回）。
- `README.md` — 仓库入口说明；`AGENTS.md` — 本文件（目录与维护约定）。

## data/ 与 docs/ 的职责边界

| | docs/ | data/ |
|---|---|---|
| 面向 | 人 | 机器 |
| 内容 | 叙事：定位、当前状态、职能档案 | 状态：结构化任务清单 |
| 变更节奏 | 相对慢（沉淀经验） | 随业务推进变化（含运行时写回） |
| 事实源 | 叙事的源头 | **机器唯一事实源**（`tasks.json`） |

## data/tasks.json 数据契约

顶层 `{ "lists": [ { "id", "name", "tasks": [ { "id", "title", "description", "status", "priority", "category" } ] } ] }`。

- `status ∈ { notStarted, inProgress, reviewing, done }`
- `priority ∈ { urgent, high, medium, low }`
- `category ∈ { business, operation, product }`（对应 docs/ 里的职能）
- 服务端/CLI 通过 `QTCLOUD_EXECUTE_DATA`（默认 `data/tasks.json`）读取，部署后作为活数据维护。

## 维护约定

- **一致性**：`data/tasks.json` 必须与 `docs/` 当前状态一致——docs 描述的事实（如「xx 已上线」「xx 阻塞」）应体现在种子对应任务的 `status`/`description` 上。
- **更新流程**：先改 `docs/`（叙事），再校正 `data/tasks.json`（状态）；新增/移动/完成的任务都要同步进种子。
- **种子是唯一机器事实源**：不要在业务/职能 md 里再配一份 json；机器只读 `data/tasks.json`。
- **同步来源**：部署时把 `data/tasks.json` 上传到 OSS 数据桶 `qtcloud-execute-provider` 的 `data/tasks.json`（与 fc.tf 的 `QTCLOUD_EXECUTE_DATA` 对象键一致）；不再从 studio assets 同步。
- **提交**：变更在 `data/profile` 子模块内提交，并在父仓库更新 submodule 引用后一并提交。
