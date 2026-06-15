---
name: 超长内容与 Tooltip 布局（layout-long-content-overflow-tooltip）
description: >-
  专项检测：已使用单行省略/溢出隐藏等「截断」样式或等价配置时，是否在静态代码上可观察到配套的 `title`、
  `Tooltip`/`Popover`、或组件库自带的 overflow 浮层（如 `show-overflow-tooltip`）；不裁决业务应采用折行、
  下拉还是展开面板。覆盖 Vue 模板/JSX、Less/SCSS、Ant Design Vue / Element Plus。仅静态代码，不测悬停帧率。
  对用户输出时默认省略 PASS；须输出项须带序号；格式为 `[路径:行号]`。
---

# 超长内容展示与 Tooltip 统一（仅前端）

## 范围边界

1. **包含**：**R-UI-01** 中与「**已出现截断语义**」强相关的静态信号：省略样式 / `ellipsis` / `line-clamp` 等与 **`title` / `Tooltip` / `Popover` / 组件库等价能力** 是否成对出现（含表格列 `ellipsis` 与 `customRender` 内 Tooltip）。
2. **明确不包含（本 skill 不判）**：业务上应选择**折行**、**下拉展开**还是**弹层编辑**等产品形态；凡未使用单行截断语义（例如纯 `word-break`、多行 `white-space: normal`、整块区域 `overflow: auto` 可滚动读全文），**不在本 skill 的 FAIL 范围内**，除非规则另行要求。
3. **不包含**：无障碍/读屏的完整达标证明（除非规则明确要求）。

## 规则命题（R-UI-01，可检测表述）

**核心**：若某展示用元素在代码上已经采用「**单行省略 / 溢出隐藏**」一类效果（见下节**截断信号**），则须在**同一展示单元**（当前节点、直接包裹子节点、或表格列 `customRender` 返回的同一单元）上，能静态观察到至少一种**可读全文**途径：`title`、`Tooltip`、`Popover`、`a-tooltip`、`el-tooltip`、`el-table` 的 `show-overflow-tooltip`，或 Ant Design Vue `Table` 列 `ellipsis` 且**未**关闭默认 `title`/且另有文档约定的全文展示（按项目所用 major 版本核对文档，版本不明时标 **UNKNOWN** 并写明版本未锁定）。

**不做什么**：不要求 Agent 判断「这里该不该用下拉/折叠菜单」；只判断「**已经写了省略**」时有没有补上 **`title` / Tooltip 系**（或组件库等价物）。

## 截断信号（命中后再查 title/Tooltip）

在模板、JSX、列配置、`<style>` 中检索以下**任一**即视为「已采用截断语义」，须继续向下文「全文途径」核对：

| 序号 | 类别 | 示例 |
|:----:|------|------|
| 1 | CSS / Less | `text-overflow: ellipsis`、`text-overflow:ellipsis`、`line-clamp`、`webkit-line-clamp`、`overflow: hidden` 与 `white-space: nowrap` 同规则集合并用于文本单元 |
| 2 | Ant Design Vue | `Table` 列 `ellipsis: true`、列 `ellipsis: { ... }`、`Typography.Text` 的 `ellipsis` |
| 3 | Element Plus | `el-table-column` `show-overflow-tooltip`（视为已带全文途径，**一般 PASS** 该点，除非显式关闭） |
| 4 | 类名 / 变量 | 项目内统一 `ellipsis`、`text-ellipsis`、`single-line` 等且样式表中对应到上述省略组合 |

## 全文途径（与截断成对出现即倾向 PASS）

| 序号 | 来源 | 示例 |
|:----:|------|------|
| 1 | 原生 | 文本节点所在元素或父级 `:title="..."`、`title="..."`（含动态绑定） |
| 2 | Ant Design Vue | `a-tooltip` / `Tooltip` 包裹文本、`Table` `customRender` 返回带 Tooltip 的 VNode |
| 3 | Element Plus | `el-tooltip`、`show-overflow-tooltip` |

**Ant Design Vue `Table` 特例**：若仅配置 `ellipsis: true`，须对照所用 **antd-vue 大版本**文档：部分版本会为单元格附带原生 `title`，此时可 **PASS**；若配置为 `ellipsis: { showTitle: false }` 且未见自定义 Tooltip → 倾向 **FAIL**。

## 静态检索建议（全量时用）

1. `grep` / ripgrep：`text-overflow`、`line-clamp`、`ellipsis`、`white-space:\s*nowrap`（结合 `overflow`）。
2. 对命中文件：从该选择器或模板节点**向外**一层层查看是否有 `title` / `Tooltip` / `a-tooltip` / `show-overflow-tooltip`；表格则看**列定义**与 **slots/customRender**。
3. 对「样式在全局 Less、类名在模板」的拆分：两处路径都写入报告 **`[路径:行号]`**。

## 代码与设计观测（可选增强）

- [ ] 是否存在**项目级统一封装**（如 `EllipsisText`），封装内是否已内置 `title` 或 Tooltip。
- [ ] 图表轴标签、图例：若使用截断类 CSS，是否配置库自带的 `formatter` + Tooltip 或等价。
- [ ] Tooltip 内容来自用户输入时，是否需转义（若安全规则要求）。

## 判定注意


- 已出现「**截断信号**」（见上节表及「静态检索建议」第 1 条；**非**仅限 `text-overflow: ellipsis` 或等价 CSS）且**同路径下未见** `title` / Tooltip 系 / 组件库 overflow 浮层 → **FAIL**（本 skill 核心负面模式）。
- 未命中任何「截断信号」的纯布局 → **不适用本专项**，勿标 FAIL。
- 版本/文档无法确认 `ellipsis` 是否自带 `title` → **UNKNOWN**，明细写明 antd-vue 版本未在仓库锁定。

## 输出规则（对用户报告）

1. **不输出 PASS 明细**：经核对**未发现**需跟进项、或已按豁免处理的，**默认视为 PASS**，**不要**逐条写入报告正文，**不**占用「明细」有序列表篇幅。
2. **只输出须跟进项明细**（**FAIL**、与 FAIL 等价的缺口、**CONDITIONAL-PASS**、**UNKNOWN**、产品豁免的 **PASS（豁免）**）：以 **有序编号**（`1.`、`2.`、…）逐条列出；**每条单行**，顺序须为 **`{序号}. {判定标签} [{仓库相对路径:行号}] 判定原因：{一句话}`**；判定标签为 **FAIL** / **CONDITIONAL-PASS** / **UNKNOWN** / **PASS（豁免）** 之一；`[路径:行号]` 指向模板/列定义/样式中最关键一处（跨文件可拆成多条，每条仍守本顺序）。**判定原因** 一句内需能回答（可用分号衔接，**不**再拆多行小标题）：场景（表格列/弹窗/卡片等）；策略归类（截断信号 + 全文途径 title 或 Tooltip 系或无）；UNKNOWN 须写明缺何信息（如 antd-vue 版本未锁定）；Ant Design Vue Table 项须点明 ellipsis 字面量、是否 showTitle: false、是否另有 customRender 与 Tooltip；PASS（豁免）须有一句依据。**不得**省略序号。
3. **UNKNOWN / PARTIAL**：**不得**单独用 PASS 充数；须输出时**并入**上述有序列表并占用序号，或于文末**一行**汇总「待查 N 处」/「依赖版本或上下文再定 N 处」，仍**不**展开 PASS。写入总控时 **CONDITIONAL-PASS** 宜映射为 **UNKNOWN** 或 **FAIL**，总控明细中不单列该标签。
4. **可选一句总括**：若全文**无任何** FAIL / CONDITIONAL-PASS / UNKNOWN / PASS（豁免），可用**一行**总结替代长列表（可不编号），例如：`「R-UI-01：已按截断信号检索，未发现需输出项（PASS 默认省略）。」`；否则仅于末尾按需加一句归纳，**不得**展开 PASS 列表。**汇总段**（按页面/路由归纳）仅当存在多项问题时可选写。

## 与总控 `verifying-ui-functional-rules` 的关系

1. 用户 **`@` 总控**或要求按 **RULE-CATALOG** 整体验证时：须遵守总控的总览表（「风险条数」与下方各章明细条数一致），以及以 `- **明细**：` 起头的有序编号列表等输出约定；对 **R-UI-01** 须使用总控的 **PASS / FAIL / UNKNOWN / N/A**；子项在明细中**只列须跟进项**，且**每条须带序号**；**CONDITIONAL-PASS** 宜映射后再写入；不在总控明细里堆 PASS。
2. 用户**仅 `@` 本专项**时：正文遵循上节「输出规则」（以须跟进项为主，**每条须带序号**）；单行顺序与总控「统一明细行格式」一致：**判定标签 → [路径:行号] → 判定原因：**（结构化信息并入「判定原因」）。

