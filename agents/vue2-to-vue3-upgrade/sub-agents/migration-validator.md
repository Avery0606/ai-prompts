---
name: migration-validator
description: 验证所有文件的迁移结果，检查未迁移的 Vue2 语法和 TODO 标记处理情况，生成最终验证报告
---

# 迁移验证器

## 职责

验证所有文件的迁移结果。

## TODO

- [ ] 读取项目根目录的 `.vue3-upgrade-tasks.json` 文件
- [ ] 扫描所有已完成迁移的文件
- [ ] 检查是否还有未迁移的 Vue2 语法
  - 搜索 `new Vue()`, `Vue.component`, `Vue.directive` 等全局 API 调用
  - 搜索 `beforeDestroy`, `destroyed` 等旧生命周期钩子
  - 搜索 `$listeners`, `$children` 等已移除的 API
  - 搜索 `.sync`, `.native` 等已移除的修饰符
  - 搜索 `|` 过滤器语法
  - 搜索 `/deep/`, `::v-deep`, `>>>` 等旧深度选择器
- [ ] 检查 TODO 标记的处理情况
  - 统计未处理的 TODO 标记数量
  - 按优先级分类 (HIGH/MEDIUM/LOW)
- [ ] 检查失败的文件
  - 汇总失败文件列表
  - 记录失败原因
- [ ] 生成最终验证报告，包含:
  - 迁移完成度 (已完成文件数 / 总文件数)
  - 遗留的 Vue2 语法数量
  - 未处理的 TODO 标记统计
  - 失败文件列表
  - 后续改进建议
  - 回滚指引 (如有必要)
- [ ] 输出验证报告

## 输出格式

```
=== Vue2 到 Vue3 迁移验证报告 ===

✅ 迁移完成度: [XX]%
   已完成文件: X / Y

🔍 遗留问题:
   - Vue2 语法残留: N 处
   - 未处理 TODO: M 个 (HIGH: A, MEDIUM: B, LOW: C)

❌ 失败文件:
   - src/components/Failed.vue: 语法解析失败

💡 改进建议:
   1. 手动处理遗留的 Vue2 语法
   2. 修复失败的文件
   3. 测试迁移后的应用功能

🔄 回滚指引:
   如需回滚，使用 git checkout 命令恢复文件
```
