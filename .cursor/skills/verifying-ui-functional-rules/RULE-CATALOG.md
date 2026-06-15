# 前端功能静态规则总表（RULE-CATALOG）

本表为 **规则 ID → 检测边界** 的索引，**命题与观测清单以各子 skill 的 `SKILL.md` 为准**；本文件不重复定义检测步骤。

| 规则 ID | 名称（简述） | 子 skill（仓库路径） |
|---------|--------------|----------------------|
| **R-FILE-01** | 上传/导入发起前类型与大小拦截、可见提示 | [file-upload-import-validation](../file-upload-import-validation/SKILL.md) |
| **R-FORM-01** | 提交请求结束前防重复（门闩/loading/全分支复位） | [form-submit-in-flight-guards](../form-submit-in-flight-guards/SKILL.md) |
| **R-FORM-02** | 可编辑文本前端硬上限与可见字数提示 | [form-input-length-limits](../form-input-length-limits/SKILL.md) |
| **R-FORM-03** | 只读截断与 **R-UI-01** 协同（展示边界） | [form-input-length-limits](../form-input-length-limits/SKILL.md) |
| **R-UI-01** | 已采用截断语义时须配 `title`/Tooltip 等全文途径 | [layout-long-content-overflow-tooltip](../layout-long-content-overflow-tooltip/SKILL.md) |
| **R-EXPORT-01** | 导出/下载请求生命周期内可感知的进行中反馈 | [list-export-table-conventions](../list-export-table-conventions/SKILL.md) |
| **R-NAV-01** | 返回列表后筛选等前端状态与跳转前一致 | [spa-state-navigation-selection-linkage](../spa-state-navigation-selection-linkage/SKILL.md) |

## 与总控的关系

执行 **`@` verifying-ui-functional-rules**（总控 skill）时：须同时阅读 [SKILL.md](./SKILL.md)，并按上表将各规则章节与子 skill 对齐；报告内规则 ID 以本表为准；各章风险**明细**单行字段顺序以 SKILL 中「**统一明细行格式**」为准（判定标签 → `[路径:行号]` → `判定原因：`）。总控每次跑完后还须将合并报告覆盖写入检测根目录下 **`docs/ui-functional-static-audit.md`**（文件名不含日期，路径规则见 SKILL **总则**）。
