---
name: data-permission-scope-levels
description: Use when validating national versus provincial versus city account data visibility, row-level or query-scoped filters for org trees, or ensuring API queries enforce the same scope as the UI.
---

# 数据权限：全国 / 省 / 地市

## 规则命题（R-SEC-01）

| 账号类型 | 可见数据范围 |
|----------|----------------|
| 全国 | 全部省份及下级 |
| 省级 | 当前省及下级地市 |
| 地市 | 仅本地市 |

## 校验层次

1. **接口契约**：列表/统计/导出/详情是否带范围参数或由服务端从 token 解析组织路径。
2. **禁止仅前端隐藏**：直接请求改参数是否仍被后端拒绝（若无后端代码，标 **UNKNOWN** 并列出应测接口）。
3. **边界**：跨省调岗、下级新增数据、缓存是否导致越权片段。

## 证据类型

- 前端：`userData`、`roles`、`regionCode` 注入查询处 `[路径:行号]`。
- 后端：数据权限注解、拦截器、SQL 过滤片段引用。

## 常见漏点

- 导出接口未套同一过滤
- 详情 ID 可遍历（水平越权）
- 统计大屏单独接口漏过滤
