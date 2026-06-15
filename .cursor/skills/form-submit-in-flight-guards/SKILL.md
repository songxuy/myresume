---
name: 表单防重复提交（form-submit-in-flight-guards）
description: >-
  校验「请求结束前防止重复提交」时使用：loading/锁、全分支复位、竞态等；适用于 Vue 2 / Vue 3
  （选项式、组合式、SFC）、JSX/TSX 渲染函数，以及 Element Plus、Ant Design Vue 或自定义按钮；仅前端 Promise 链终态，
  不测接口真实耗时。对用户输出时 PASS 略过，只列缺口明细（须带序号；单行顺序为 FAIL、[路径:行号]、判定原因：）。
---

# 表单防重复提交（仅前端）

## 范围边界

1. **包含**：提交入口、请求封装、`loading` / `disabled` / 互斥锁等与同一请求生命周期绑定的逻辑；**与 Vue 主版本、模板语法（SFC / JSX）无强绑定**，凡能在前端静态追到「提交 → 请求 → 终态复位」链路的项目均可按本 skill 核对。
2. **不包含**：后端幂等、接口耗时、Network 抓包结论。

## 规则标准表述（对齐产品语言）

**命题**：在未收到本次提交对应请求的**最终**前端结果（`resolve` / `reject`、业务错误分支、HTTP 错误、超时、用户取消）之前，用户不能通过同一提交入口再次触发提交。

「最终」以**前端 Promise 链或 async 函数结束**为准；**不要求**验证接口真实耗时或后端幂等。

## 必须通过的信号（至少满足一类，并覆盖全路径）

在代码审查中至少确认以下模式之一**完整绑定到提交按钮与同一请求生命周期**：

| 序号 | 模式 | 典型实现 | 失败征象 |
|:----:|------|----------|----------|
| 1 | 状态门闩 | `isSubmitting` / `loading` 为 true 时直接 return 或禁用按钮 | 仅 `disabled` 无 early return，仍可从键盘/程序路径重复调用 |
| 2 | 互斥锁 | `submitLock`、队列长度为 1 | 锁在 catch/finally 外未释放，导致永久卡死 |
| 3 | 请求层去重 | 同一 key 合并进行中的请求 | 不同实例仍并发 |
| 4 | UI 层 | SFC：`:disabled` / `:loading`；JSX：`disabled` / `loading`；`pointer-events` 与逻辑一致 | 样式禁用但点击/键盘仍触发提交 |

## 校验步骤（对单表单）

1. 定位「提交」入口：SFC 模板中的 `@submit` / `@click`；**JSX/TSX** 中的 `onClick` / `onSubmit` / `onFinish`；或封装组件暴露的事件（**`el-button` / `a-button` / `<button>` / `Button` 均可**）。
2. 找到处理函数：`async` 内第一次 `await` 之前的**同步段**是否仍可能被二次进入（Vue 2 / Vue 3 或纯函数组件均适用）。
3. 找到真实请求：`axios` / `fetch` / 封装 `request`；若一次提交触发多个串行请求，确认产品是否视为「一次提交」并一并加锁。
4. 核对**所有出口**：`try` / `catch` / `finally` 中是否正确复位 `loading` / 锁；错误提示后是否允许再次提交。
5. 核对**竞态**：若存在丢弃过期响应的逻辑，说明是否与产品一致。

## Vue 2 / Vue 3 / JSX 快速检索关键词

`submit`、`handleSubmit`、`loading`、`isSubmitting`、`pending`、`disabled`、`debounce`、`throttle`、`inFlight`、`mutex`

在 `src/views`、`src/components` 中从按钮文案或主按钮附近向上追踪；**JSX/TSX** 文件可额外搜 `onClick`、`onFinish`、`loading=`、`disabled=`。

## 结论标签（内部分类，供核对用）

1. **PASS**：`handleSubmit` 在请求前设 `loading=true`，`finally` 复位；函数首行有 guard；按钮在 SFC 中为 `:loading` / `:disabled`，在 JSX 中为 `loading` / `disabled` prop，且与同一状态绑定。
2. **FAIL**：仅 `@click` 上 `debounce(300)`，慢网络下仍可连发；无 in-flight 门闩；或首段 `await` 未与同一 `loading`/锁绑定等。
3. **UNKNOWN**：提交逻辑在子组件内但未找到可追踪的 loading 状态。

## 输出规则（对用户报告）

1. **不输出 PASS 明细**：已满足 **R-FORM-01** 的入口**不要**逐条写入报告正文，**不**占用「明细」有序列表篇幅。
2. **只输出缺口明细**（本专项下 **FAIL** 或与 FAIL 等价的需跟进项，含「仅部分分支加锁」「首段 await 无门闩」等）：以 **有序编号**（`1.`、`2.`、…）逐条列出；**每条单行**，顺序须为 **`{序号}. FAIL [{仓库相对路径:行号}] 判定原因：{一句话}`**（**UNKNOWN** 用时替换 **FAIL**）；「判定原因」内写门闩、loading、全分支复位等缺失信号。**不得**省略序号。
3. **UNKNOWN / PARTIAL**：**不得**单独用 PASS 充数；须输出时**并入**上述有序列表并占用序号（写明「待补门闩或待追子组件」等），或于文末**一行**汇总「待查 N 处」，仍**不**展开 PASS。
4. **可选一句总括**：仅在需要时于报告**末尾**加一句（可不编号），例如「其余已检提交入口未见需列入 R-FORM-01 的缺口」，**不得**展开 PASS 列表。

## 与总控 `verifying-ui-functional-rules` 的关系

1. 用户 **`@` 总控**或要求按 **RULE-CATALOG** 整体验证时：须遵守总控的总览表（「风险条数」与下方各章明细条数一致），以及以 `- **明细**：` 起头的有序编号列表等输出约定；**R-FORM-01** 子项在明细中**只列缺口**，且**每条须带序号**；不在总控明细里堆 PASS。
2. 用户**仅 `@` 本专项**时：正文**只写缺口明细**（与上节「输出规则」第 2 条一致），每条 **须带序号**；单行顺序与总控「统一明细行格式」一致：**FAIL → [路径:行号] → 判定原因：**；内部分类仍可用 PASS/FAIL/UNKNOWN 自洽核对。
