---
name: file-migrator
description: 协调单个文件的所有迁移阶段，根据文件类型执行相应的子迁移器
---

# 文件迁移器

## 职责

接收文件路径，根据文件类型协调执行相应的迁移阶段，收集变更报告。

## TODO

- [ ] 接收文件路径和项目上下文作为输入
- [ ] 根据文件类型确定需要执行的迁移阶段列表
- [ ] 依次调用相应的子迁移器:
  - dependency-upgrader (加载 skill: vue3-migration-dependency.md)
  - global-api-migrator (加载 skill: vue3-migration-global-api.md)
  - component-migrator (加载 skill: vue3-migration-component.md)
  - template-migrator (加载 skill: vue3-migration-template.md)
  - style-migrator (加载 skill: vue3-migration-style.md)
  - router-migrator (加载 skill: vue3-migration-router.md) - 可选
  - vuex-migrator (加载 skill: vue3-migration-vuex.md) - 可选
- [ ] 收集每个阶段的变更记录
- [ ] 统计 TODO 标记总数量
- [ ] 统计检测到的问题数量（按高/中/低优先级分类）
- [ ] 返回执行结果报告 (status, phases, changes, error)

## 文件类型适配规则

**.vue 文件**: 执行所有阶段
- dependency-upgrader
- global-api-migrator
- component-migrator
- template-migrator
- style-migrator
- router-migrator (如果是路由文件)
- vuex-migrator (如果是 Vuex 文件)

**.js/.ts 文件**: 跳过 template 和 style 阶段
- dependency-upgrader
- global-api-migrator
- router-migrator (如果是路由文件)
- vuex-migrator (如果是 Vuex 文件)

**路由文件识别**: 文件路径包含 `router` 或 `route` 关键词

**Vuex 文件识别**: 文件路径包含 `store` 或 `vuex` 关键词

## 输出格式

```json
{
  "status": "completed" | "failed",
  "phases": ["dependency", "global-api", "component", "template", "style"],
  "changes": {
    "added_todos": 5,
    "issues": {"high": 1, "medium": 3, "low": 7}
  },
  "error": "错误信息（失败时）"
}
```

## 错误处理

- 任何阶段失败时，标记文件为 failed
- 记录详细错误信息
- 不尝试重试
