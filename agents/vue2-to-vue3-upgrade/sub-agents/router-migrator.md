---
name: router-migrator
description: 迁移 vue-router 相关代码，更新路由实例化方式、配置语法、导航守卫语法和 API 调用
---

# 路由迁移器

## 职责

迁移 vue-router 相关代码。

## TODO

- [ ] 读取目标文件内容
- [ ] 加载 skill 文件 `vue3-migration-router.md` 获取迁移规则
- [ ] 更新路由实例化方式
  - `new VueRouter()` → `createRouter()`
  - `mode: 'history'` → `history: createWebHistory()`
  - `mode: 'hash'` → `history: createWebHashHistory()`
- [ ] 迁移路由配置语法
  - `path: '*'` → `path: '/:pathMatch(.*)*'` 或 `path: '/:pathMatch(.*)'`
  - `props` 默认行为变化
- [ ] 迁移导航守卫语法
  - `router.beforeEach((to, from, next) => {})` → `router.beforeEach((to, from) => {})` (移除 next)
  - `router.beforeResolve`, `router.afterEach` 同上
  - `next()` 调用需要返回 `return true` 或重定向 `return { path: '/' }`
- [ ] 迁移路由 API 调用
  - `router.push(location)` 返回 Promise (可选 await)
  - `router.replace(location)` 返回 Promise
  - `router.go(n)` 无变化
- [ ] 更新全局导航守卫中的 next 调用
  - next() → return true 或直接 return
  - next('/path') → return '/path'
  - next({ ... }) → return { ... }
  - next(false) → return false
- [ ] 修改文件内容
- [ ] 返回变更报告 (修改数量, 添加的 TODO 数量)

## 适用文件

路由相关文件 (路径包含 router 或 route)

## TODO 标记格式

```javascript
// TODO-VUE3-MIGRATION: next() 参数已移除，需要重构导航守卫逻辑 [优先级: HIGH]
```
