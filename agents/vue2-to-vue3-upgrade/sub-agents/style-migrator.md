---
name: style-migrator
description: 迁移样式相关代码，/deep/ → :deep()、::v-deep → :deep()、处理 scoped 样式变化
---

# 样式迁移器

## 职责

迁移样式相关代码。

## TODO

- [ ] 读取目标文件内容
- [ ] 加载 skill 文件 `vue3-migration-style.md` 获取迁移规则
- [ ] 迁移深度选择器语法
  - `/deep/` → `:deep()`
  - `>>>` → `:deep()`
  - `::v-deep` → `:deep()`
  - `/deep/ selector/` → `:deep(selector)`
  - `>>> selector` → `:deep(selector)`
- [ ] 处理 scoped 样式的变化
  - `::v-slotted()` 替代 `::v-deep` 作用于 slot 内容
- [ ] 修改文件内容
- [ ] 返回变更报告 (修改数量)

## 适用文件

.vue 文件的 style 部分
