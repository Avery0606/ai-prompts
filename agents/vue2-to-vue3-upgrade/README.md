# Vue2 升级 Vue3 智能体

## 用途

本智能体用于协助将 Vue2 项目升级到 Vue3，主要功能包括：

- 识别 Vue2 中的过时语法和API
- 根据规则将 Vue2 代码转换为 Vue3 兼容代码
- 处理常见的升级场景和兼容性问题
- 标记需要人工审查的代码变更

## 使用方式

### 自动模式

适用于支持子智能体调用的 AI coding 工具（如 OpenCode 等）：

```
agent: vue2-to-vue3-upgrade
```

主智能体将自动按阶段调用各子智能体完成迁移。

### 手动模式

适用于不支持子智能体调用的 AI coding 工具：

1. **准备阶段**
    - 读取 `agent.md` 了解完整迁移流程
    - 检查项目是否为 Git 仓库，提交所有未提交变更

2. **按阶段执行**
    - 读取 `sub-agents/{stage-name}.md` 文件
    - 读取对应的 `skills/{skill-name}.md` 获取迁移规则
    - 将两者内容作为 prompt 传递给 AI 工具
    - 附上项目上下文信息（如 package.json、项目结构）
    - 执行该阶段任务
    - 查看 AI 工具的输出和变更

3. **阶段确认**
    - 每个阶段完成后，检查修改的文件
    - 确认无误后进入下一阶段
    - 如有问题可回滚到该阶段前

   4. **阶段顺序**
    ```
    0. progress-tracker.md        → 查看升级进展（可随时执行）
    1. project-analyzer.md        → 分析项目
    2. dependency-upgrader.md     → 升级依赖
    3. global-api-migrator.md     → 全局API迁移
    4. component-migrator.md      → 组件迁移
    5. template-migrator.md       → 模板迁移
    6. router-migrator.md         → 路由迁移（如使用）
    7. vuex-migrator.md           → Vuex迁移（如使用）
    8. style-migrator.md          → 样式迁移
    9. migration-validator.md     → 验证迁移
    ```

## 子智能体说明

每个子智能体均可独立运行，只需将对应的 `.md` 文件内容作为 prompt 传入 AI 工具，并提供必要的项目上下文。

### Skills 迁移规则

子智能体执行时会自动加载对应的 skill 文件，该文件包含该阶段的迁移规则和代码示例：

| Skill | 描述 |
|-------|------|
| vue3-migration-breaking-changes.md | 破坏性变更列表 |
| vue3-migration-global-api.md | 全局 API 迁移规则 |
| vue3-migration-component.md | 组件语法迁移规则 |
| vue3-migration-template.md | 模板语法迁移规则 |
| vue3-migration-router.md | Vue Router 迁移规则 |
| vue3-migration-vuex.md | Vuex 迁移规则 |
| vue3-migration-style.md | 样式迁移规则 |
| vue3-migration-compat.md | @vue/compat 使用指南 |

Skill 采用渐进式披露模式，每个子智能体仅加载相关的 skill 文件，避免上下文污染。

### 进度跟踪
- `progress-tracker.md` - 查看当前升级进展和结果摘要（可随时执行）

### 必需阶段
- `project-analyzer.md` - 分析项目结构和依赖
- `dependency-upgrader.md` - 升级核心依赖包
- `global-api-migrator.md` - 迁移全局 API 调用
- `component-migrator.md` - 迁移组件语法
- `template-migrator.md` - 迁移模板语法
- `style-migrator.md` - 迁移样式相关代码
- `migration-validator.md` - 验证迁移结果

### 可选阶段
- `router-migrator.md` - 仅项目使用 vue-router 时执行
- `vuex-migrator.md` - 仅项目使用 vuex 时执行

## 注意事项

1. **独立运行**：每个子智能体设计为可独立运行，不依赖其他子智能体的输出
2. **上下文传递**：手动调用时需提供当前项目上下文（package.json、相关配置文件等）
3. **阶段隔离**：每个阶段聚焦特定任务，完成后等待确认再继续
4. **可回滚**：基于 Git 历史记录，每个阶段均可独立回滚
5. **渐进式**：优先使用 @vue/compat 迁移 build，逐步解决兼容性警告
