---
name: api-response-time-slo
description: Use when validating stated API latency targets for normal queries, complex operations, or statistical reports, or when the user mentions 3s, 5s, or 10s response expectations.
---

# 接口响应时间期望（SLO）

## 规则命题（R-PERF-01）

| 类型 | 目标 |
|------|------|
| 一般查询接口 | ≤ 3s |
| 复杂操作 | ≤ 5s |
| 统计型报表 | ≤ 10s |

环境（网络、数据量、并发）以产品/测试基线为准。

## 静态代码可检项

- 不必要 N+1、全表拉取、未分页的大列表。
- 前端重复请求、瀑布串行可合并处。
- 超时配置是否与 SLO 一致（过短误杀、过长掩盖问题）。

## 达标证据类型（须在报告中标注）

- **EVIDENCE-RUNTIME**：浏览器 Network  timing、后端日志、APM、压测报告摘要。
- 纯静态审查无法对 **PASS** 签字；最多 **CONDITIONAL-PASS**（无反模式）或 **UNKNOWN**。

## 报告写法

对每个相关接口列：名称、判定、证据类型、采样条件（数据量、并发）。
