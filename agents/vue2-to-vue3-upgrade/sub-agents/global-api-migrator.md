---
name: global-api-migrator
description: 迁移全局 API 调用，Vue.xxx → app.xxx、Vue.component → app.component、Vue.directive → app.directive、Vue.filter 标记为重构
---

# 全局 API 迁移器

## 职责

迁移全局 API 调用。

## TODO

- [ ] 读取目标文件内容
- [ ] 加载 skill 文件 `vue3-migration-global-api.md` 获取迁移规则
- [ ] 迁移全局 API 调用
  - `Vue.use()` → `app.use()`
  - `Vue.mixin()` → `app.mixin()`
  - `Vue.component()` → `app.component()`
  - `Vue.directive()` → `app.directive()`
  - `Vue.extend()` → `defineComponent()`
  - `Vue.set()` → 使用 reactive 或重新赋值
  - `Vue.delete()` → 使用 delete 操作符或 null 赋值
  - `Vue.nextTick()` → `nextTick()` (从 vue 导入)
  - `Vue.version` → `version` (从 vue 导入)
  - `Vue.config.xxx` → `app.config.xxx`
- [ ] 迁移事件总线相关代码 (如有)
- [ ] 标记 Vue.filter 为需要重构 (过滤器已移除)
- [ ] 修改文件内容
- [ ] 返回变更报告 (修改数量, 添加的 TODO 数量)

## 适用文件

所有文件 (.vue, .js, .ts)

## TODO 标记格式

```javascript
// TODO-VUE3-MIGRATION: Vue.filter 已移除，需要重构为计算属性或全局方法 [优先级: HIGH]
```
