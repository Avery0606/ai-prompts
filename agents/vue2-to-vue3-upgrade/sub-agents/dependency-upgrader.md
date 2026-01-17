---
name: dependency-upgrader
description: 迁移依赖导入语句，更新 Vue 相关导入和第三方库导入，标记未知库为需要人工审查
---

# 依赖迁移器

## 职责

迁移文件中的依赖导入语句。

## TODO

- [ ] 读取目标文件内容
- [ ] 加载 skill 文件 `vue3-migration-dependency.md` 获取迁移规则
- [ ] 更新 Vue 相关导入语句
  - `import Vue from 'vue'` → `import { createApp } from 'vue'`
  - `import VueRouter from 'vue-router'` → `import { createRouter } from 'vue-router'`
  - `import Vuex from 'vuex'` → `import { createStore } from 'vuex'`
- [ ] 更新已知不兼容的第三方库导入
- [ ] 标记未知/未验证的第三方库为需要人工审查 (添加 TODO 注释)
- [ ] 修改文件内容
- [ ] 返回变更报告 (修改的导入语句数量, 添加的 TODO 数量)

## 适用文件

所有文件 (.vue, .js, .ts)

## TODO 标记格式

```javascript
// TODO-VUE3-MIGRATION: 第三方库 xxx 未知兼容性，需要人工审查 [优先级: MEDIUM]
```
