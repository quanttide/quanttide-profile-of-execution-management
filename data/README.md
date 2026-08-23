# data/ — 机器种子数据

`tasks.json` 是结构化任务清单（`{ "lists": [{ "id", "name", "tasks": [...] }] }`），为服务端/CLI 的种子数据（`QTCLOUD_EXECUTE_DATA`），部署时注入并持续维护。

- 字段与取值约定见根目录 [AGENTS.md](../AGENTS.md)。
- 必须与 `docs/` 当前状态一致（先改 docs 叙事，再校正本种子）。
- 上传：部署时上传到 OSS 数据桶 `qtcloud-execute-provider` 的 `data/tasks.json`（与 fc.tf 的 `QTCLOUD_EXECUTE_DATA` 对象键一致）。
