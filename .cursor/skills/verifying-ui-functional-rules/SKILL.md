---
name: 前端功能静态规则总控（verifying-ui-functional-rules）
description: >-
  按 RULE-CATALOG 与 6 个子专项对指定路径做静态核对；产出合并 Markdown 报告，
  且每次执行后须将报告覆盖写入 `docs/ui-functional-static-audit.md`（见 SKILL「总则」「报告落盘」）。
  总控第 1～6 章风险条数及明细须与同路径下单独执行各子 skill 的结论一致，不得以泛化推论替代子 skill 全量观测。
---

# 前端功能静态规则总控（仅前端静态）

## 定位

本 skill 为 **总控编排**：不重复定义各子项命题。执行时须 **依次** 打开 [RULE-CATALOG.md](./RULE-CATALOG.md) 与下列 **6** 个子 skill 的 `SKILL.md`，严格按其「范围边界」「命题/观测」「输出规则」核对，再在同一轮交付中输出 **一份合并的 Markdown 报告**，并完成 **「报告落盘」**（写入仓库 `docs` 下固定文件名的 Markdown 文件）。

## 总则（报告文件与命名）

1. **文件名**：落盘 Markdown 文件名 **固定** 为 `ui-functional-static-audit.md`；每次执行在对应 `docs/` 下 **覆盖写入** 同一文件，避免多文件与重复授权/确认。
2. **落盘路径**（仓库根）：检测范围在 **`xxx/`**（含子路径）→ `xxx/docs/ui-functional-static-audit.md`；其他与 `xxx/` 平级的应用根 → `{该目录}/docs/ui-functional-static-audit.md`；仅仓库根或未形成单一应用根 → `docs/ui-functional-static-audit.md`（`docs/` 不存在则创建）。
3. **报告正文**：合并报告 **不包含**「附：检测方法说明」章节（已取消）。若需额外历史副本，须在对话中由用户 **明确给出** 另一文件的完整相对路径与文件名。

## 子专项清单（须全部覆盖；与 RULE-CATALOG 一致）

| 序号 | 子 skill（仓库内路径） | 规则 ID |
|:----:|------------------------|---------|
| 1 | [file-upload-import-validation](../file-upload-import-validation/SKILL.md) | **R-FILE-01** |
| 2 | [form-submit-in-flight-guards](../form-submit-in-flight-guards/SKILL.md) | **R-FORM-01** |
| 3 | [form-input-length-limits](../form-input-length-limits/SKILL.md) | **R-FORM-02** / **R-FORM-03**（及与 **R-UI-01** 协同） |
| 4 | [layout-long-content-overflow-tooltip](../layout-long-content-overflow-tooltip/SKILL.md) | **R-UI-01** |
| 5 | [list-export-table-conventions](../list-export-table-conventions/SKILL.md) | **R-EXPORT-01** |
| 6 | [spa-state-navigation-selection-linkage](../spa-state-navigation-selection-linkage/SKILL.md) | **R-NAV-01** |

## 与子 skill 结论对齐

1. **等价于单独执行**：对每个子 skill，须假设「用户仅 `@` 该子 skill、且检测范围与总控相同」；总控对应章节的 **风险条数**、**有序明细**（含 **FAIL** / **UNKNOWN** / 子 skill 要求写出的豁免项等）须与该假设下单独跑子 skill 的结论 **一致**。禁止用「版本默认 PASS」「抽样未见问题」等 **未按该子 skill 观测清单逐项核对** 的表述，把该章明细压成 0 条或更少条。
2. **风险条数的「可合并」边界以子 skill 为准**：若子 skill 正文规定了 **每条 FAIL 对应的最小粒度**（例如按「源文件」「独立表单项入口」「独立上传入口」等），总控该章 **有序列表条数** 与 **总览风险数** 须采用 **同一粒度**；子 skill 未允许合并时，**禁止**为缩短列表把多文件、多入口、多组件根路径压成一条。
3. **禁止以一类实现替代另一类**：例如 **R-UI-01** 不得以「Ant Design Vue `Table` 列 `ellipsis` 可能自带 `title`」替代对 **Less/SCSS + 模板中单行省略**（`text-overflow: ellipsis` 等与 `nowrap`/`overflow` 组合）的逐路径核对；表格列与自定义单元格、弹窗内文本须 **分别** 按子 skill 命中截断信号后再判。
4. **总览表与明细一致**：「总览」中该规则 **风险条数** = 该章 `- **明细**：` 下 **有序列表** 条数（或子 skill 认可的等价统计）；**不得**出现总览为 0 而明细有项、或总览大于明细之和。
5. **子 skill 输出格式优先**：每条明细末尾须带规则 ID 等要求时，以子 skill 正文为准（如 **R-EXPORT-01** 等）；**字段顺序** 以本节「统一明细行格式」为准，子 skill 要求的结构化信息（如 **R-UI-01** 的场景/策略）**并入**「判定原因」一句或同句内分号衔接，**不**在标签与 `[路径:行号]` 之间插入大段小标题。

## 统一明细行格式（各章 `- **明细**：` 下有序列表）

1. **单行**：每条风险占 **一行**（有序列表的一项），**不**拆成「先标签、下一行再路径」等多行写法。
2. **字段顺序（须遵守）**：`{序号}. {判定标签} [{仓库相对路径:行号}] 判定原因：{一句话}`  
   - **判定标签**：与子 skill 一致，一般为 **FAIL**；允许 **UNKNOWN**、**CONDITIONAL-PASS**、**PASS（豁免）** 等子 skill 明文允许的标签；**不**对风险项写 **PASS**。
   - **`[{路径:行号}]`**：半角方括号；路径为从仓库根起的相对路径（如 `jiangxi/src/views/.../x.vue`）；行号取 **最关键锚点**（连续行块可取 **起始行**，并在「判定原因」中必要时点明至结束行）；**不**再单独用反引号包一层路径以免与方括号重复混乱。
   - **判定原因**：固定前缀 **`判定原因：`**（半角冒号），后为简短说明；缺何种信号、豁免依据、样式行范围等 **均写在该前缀之后**。
3. **规则 ID**：子 skill 要求每条须带规则 ID 的，写在 **判定原因** 句末或同句内（如 **R-EXPORT-01**、**R-FILE-01**）。
4. **对话中的 skill 输出**：用户 **`@` 总控** 或 **`@` 任一子 skill** 时，风险明细列表 **同样** 采用本条顺序，便于与落盘 `ui-functional-static-audit.md` 对照。

## 执行要求（对 Agent）

1. **范围**：以用户 `@` 的路径为准；未指定则须向用户确认，**不得**默认扩大到全 monorepo。
2. **子 skill**：对上表 **每一项** 阅读对应 `SKILL.md`，完成其静态检索与判定后再写对应章节。
3. **结论合并**：各子专项 **PASS 不写入报告正文**；**风险 / UNKNOWN / 须跟进项** 全部写入对应章节，且 **有序号**，每条 **单行** 格式须符合上节「统一明细行格式」并与子 skill 对规则 ID、标签的要求一致。
4. **Markdown 报告**：在对话中输出完整 Markdown 正文；**必须**将同一正文按 **总则** 路径覆盖写入 `ui-functional-static-audit.md`；结构须使用下文模板的一级/二级标题；对话末尾 **一行** 写明已写入的仓库相对路径。

## Markdown 报告模板（复制后填空；`{变量}` 由 Agent 替换）

```markdown
# 前端功能静态检测报告

- **检测范围**：{指定目录}
- **说明**：本报告为静态代码核对结论，不含接口真实耗时、后端幂等、无障碍完整达标等未在子 skill 范围内之证明。

## 总览

*「风险条数」列须与同编号章节「明细」中有序列表条数一致；约束见上文「与子 skill 结论对齐」第 3 条。*

| 子专项 | 规则 ID | 风险条数 |
|--------|---------|----------|
| 上传与导入 | R-FILE-01 | {n1} |
| 防重复提交 | R-FORM-01 | {n2} |
| 表单长度与只读截断 | R-FORM-02 / R-FORM-03 | {n3} |
| 超长与 Tooltip | R-UI-01 | {n4} |
| 导出反馈 | R-EXPORT-01 | {n5} |
| 返回态与筛选 | R-NAV-01 | {n6} |

**汇总**：{n1+n2+n3+n4+n5+n6 或等价说明；含 UNKNOWN 时须在此句点明}

---

## 1. 上传与导入（R-FILE-01）

> 子 skill：[file-upload-import-validation](../file-upload-import-validation/SKILL.md)

- **明细**：

{仅列风险；无则写：「未发现须跟进项（PASS 省略）。」；有则每项一行，顺序见本 SKILL「统一明细行格式」。示例：1. FAIL [jiangxi/src/views/_components/importModal/index.vue:17] 判定原因：无 accept 与用户可见类型/大小拦截，缺 **R-FILE-01**。}

---

## 2. 防重复提交（R-FORM-01）

> 子 skill：[form-submit-in-flight-guards](../form-submit-in-flight-guards/SKILL.md)

- **明细**：

{同上。示例：1. FAIL [jiangxi/src/views/permission/_components/formMenu.jsx:171] 判定原因：getFormData 在首个 await 前无门闩与 loading，缺 **R-FORM-01**。}

---

## 3. 表单字符长度与边界（R-FORM-02 / R-FORM-03）

> 子 skill：[form-input-length-limits](../form-input-length-limits/SKILL.md)

- **明细**：

{同上。示例：1. FAIL [jiangxi/src/views/permission/index.jsx:251] 判定原因：可编辑 a-input 无 maxlength 与字数提示，缺 **R-FORM-02**。}

---

## 4. 超长内容与 Tooltip（R-UI-01）

> 子 skill：[layout-long-content-overflow-tooltip](../layout-long-content-overflow-tooltip/SKILL.md)

- **明细**：

{同上；子 skill 要求的场景/策略/全文途径等写入「判定原因」内。示例：1. FAIL [jiangxi/src/views/Report/_components/reportBody/UploadDrawer.vue:37] 判定原因：已选文件名截断（ellipsis+nowrap）且无 title 或 Tooltip 全文途径，**R-UI-01**。}

---

## 5. 列表导出与表格约定（R-EXPORT-01）

> 子 skill：[list-export-table-conventions](../list-export-table-conventions/SKILL.md)

- **明细**：

{同上；句末须含 **R-EXPORT-01**。示例：1. FAIL [jiangxi/src/views/permission/index.jsx:103] 判定原因：async export 无与导出绑定的 loading 或禁用，缺进行中反馈 **R-EXPORT-01**。}

---

## 6. 返回态与筛选持久化（R-NAV-01）

> 子 skill：[spa-state-navigation-selection-linkage](../spa-state-navigation-selection-linkage/SKILL.md)

- **明细**：

{同上。示例：1. FAIL [jiangxi/src/views/project/index.jsx:21] 判定原因：activated 内重置 engineeringId 易覆盖用户筛选，缺 **R-NAV-01**。}

```

## 与子 skill 输出冲突时的优先级

1. **子 skill 明文规定** 优先于本模板。
2. **RULE-CATALOG** 仅约束 **规则 ID 命名与归属**；检测步骤仍以子 skill 为真源。
3. **计数与分列冲突时**：以子 skill 中 **「风险计数与分列」**（或等价标题）及 **输出规则** 为准；总控仅在不违背子 skill 的前提下统一行序与字段格式。
