# AGENTS.md — 执行档案（profile）仓库约定

> 供 Agent/协作者查阅的本仓库目录与维护约定。

## 仓库定位

执行档案（quanttide-profile-of-execution-management）：按 **业务 × 职能** 记录量潮各业务的执行情况。脱敏公开版——只含产品/技术事实；人事/客户/治理细节保留在私有仓库。

## 目录结构

```
quanttide-tech/   # 量潮科技
  qtdata/    # 量潮数据：客户项目复现、数据产品（index + business/product）
  qtclass/   # 量潮课堂：实训基地招聘运营、课堂创新（index + operation/product）
  qtcloud/   # 量潮云：媒体云、执行云（index + qtcloud-media/qtcloud-execute 任务分解）
quanttide-alliance/   # 量潮联盟
  qtrecurit/
  qtcrowd/
quanttide-founder/   # 创始人（目标与关键结果）
quanttide-institute/   # 量潮研究院（目标与关键结果）
quanttide-academy/   # 量潮实训基地（目标与关键结果）
README.md
LICENSE
```

- 每个业务含 `index.md`（目标、关键结果；任务：按任务组分三级标题）+ 职能档案（`product|operation|business`）；任务也可按任务组另立任务分解文件（如 qtcloud/ 的 `qtcloud-media.md`、`qtcloud-execute.md`），index 只留当前状态并链到分解文件。
- 职能档案是「发生过什么、当前进展」的**叙事**来源，变更节奏相对慢（沉淀经验）。

## 维护约定

- **更新流程**：改业务/职能 md 后，同步该业务 `index.md` 的任务状态。
- **结果口径**：「目标」一句话方向；「关键结果」写可验收的结果（如原型变生产可用上线、获取付费客户），不写活动；「任务」按任务组分三级标题，只写当前状态，任务叙事留在职能档案与任务分解。
- **索引归 README**：`index.md` 不写目录/索引，索引写入仓库 `README.md`。
- **目录即语义**：新业务按同级目录 + `index.md` 模式加入，不另配数据文件。
- **提交**：变更在 `data/profile` 子模块内提交，并在父仓库更新 submodule 引用后一并提交。
