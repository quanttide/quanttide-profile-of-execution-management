# data/ — 机器种子数据

`seed_tasks.json` 是结构化任务清单（`{ "lists": [{ "id", "name", "tasks": [...] }] }`），为服务端/CLI 的种子数据（`QTCLOUD_EXECUTE_DATA`），部署时注入并持续维护。

- 字段与取值约定见根目录 [AGENTS.md](../AGENTS.md)。
- 必须与 `docs/` 当前状态一致（先改 docs 叙事，再校正本种子）。
- 来源：从 `apps/qtcloud-execute/src/studio/assets/data/seed_tasks.json` 同步。
