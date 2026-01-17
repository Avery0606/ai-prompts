---
name: component-migrator
description: 迁移组件 Options API 语法，更新生命周期钩子、$listeners、$children、v-model 语法、functional 组件和自定义指令钩子
---

# 组件迁移器

## 职责

迁移组件 Options API 语法。

## TODO

- [ ] 读取目标文件内容
- [ ] 加载 skill 文件 `vue3-migration-component.md` 获取迁移规则
- [ ] 更新生命周期钩子
  - `beforeDestroy` → `beforeUnmount`
  - `destroyed` → `unmounted`
- [ ] 迁移已移除的 API
  - 移除 `$listeners` (合并到 `emits` 配置或 `$attrs`)
  - 移除 `$children` (改用 ref 和 template refs)
  - 移除 `$scopedSlots` (合并到 `$slots`)
- [ ] 迁移 v-model 语法
  - `.sync` 修饰符 → v-model 参数形式 (Vue3 v-model)
  - `v-model` + `value` → `v-model` + `modelValue`
  - 更新 `$emit('input')` → `$emit('update:modelValue')`
- [ ] 迁移 functional 组件
  - 转换为普通组件或函数式组件新语法
- [ ] 处理自定义指令钩子变化
  - `bind` → `mounted`
  - `update` → `updated` (oldValue 参数需要额外处理)
  - `unbind` → `unmounted`
- [ ] 修改文件内容
- [ ] 返回变更报告 (修改数量, 添加的 TODO 数量)

## 适用文件

.vue 文件的 script 部分

## TODO 标记格式

```javascript
// TODO-VUE3-MIGRATION: $listeners 已移除，需要手动合并到 emits [优先级: HIGH]
```
