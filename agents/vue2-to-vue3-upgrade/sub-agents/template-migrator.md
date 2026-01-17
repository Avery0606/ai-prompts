---
name: template-migrator
description: 迁移模板语法，事件修饰符 .native、v-model 语法、slot 语法、transition 过渡类名、过滤器语法
---

# 模板迁移器

## 职责

迁移模板语法。

## TODO

- [ ] 读取目标文件内容
- [ ] 加载 skill 文件 `vue3-migration-template.md` 获取迁移规则
- [ ] 迁移事件修饰符
  - 移除 `.native` 修饰符 (事件监听器现在会自动继承到根元素)
- [ ] 迁移 v-model 语法
  - `.sync` → v-model 参数形式
  - `v-model` 在自定义组件上的使用方式更新
- [ ] 迁移 slot 语法
  - `slot="xxx"` → `#xxx`
  - `slot-scope="prop"` → `#xxx="prop"`
  - `v-slot:xxx` → `#xxx`
- [ ] 迁移 transition 过渡类名
  - `v-enter` → `v-enter-from`
  - `v-leave` → `v-leave-from`
- [ ] 处理过滤器语法
  - 移除管道符 `|` 过滤器
  - 标记需要用计算属性或方法替换
- [ ] 修改文件内容
- [ ] 返回变更报告 (修改数量, 添加的 TODO 数量)

## 适用文件

.vue 文件的 template 部分

## TODO 标记格式

```html
<!-- TODO-VUE3-MIGRATION: 过滤器已移除，需要用计算属性或方法替换 [优先级: MEDIUM] -->
```
