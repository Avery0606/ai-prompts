# Vue2 升级 Vue3 智能体

## 用途

本智能体用于协助将 Vue2 项目升级到 Vue3，主要功能包括：

- 识别 Vue2 中的过时语法和API
- 根据规则将 Vue2 代码转换为 Vue3 兼容代码
- 采用文件级别的细粒度迁移策略，每个文件独立完成所有迁移阶段
- 通过任务队列跟踪所有文件的升级进度，支持可中断、可恢复
- 处理常见的升级场景和兼容性问题
- 标记需要人工审查的代码变更

## 使用方式

### 自动模式

适用于支持子智能体调用的 AI coding 工具（如 OpenCode 等）：

```
agent: vue2-to-vue3-upgrade
```

主智能体将自动执行：初始化 → 循环处理每个文件 → 验证。

### 手动模式

适用于不支持子智能体调用的 AI coding 工具：

1. **准备阶段**
    - 读取 `agent.md` 了解完整迁移流程
    - 检查项目是否为 Git 仓库，提交所有未提交变更（推荐）

2. **初始化阶段**
    - 调用 `task-initializer` 创建任务队列（`.vue3-upgrade-tasks.json`）
    - 调用 `project-analyzer` 分析项目结构
    - 调用 `progress-tracker` 查看初始状态

3. **循环阶段**
    - 调用 `file-queue-manager` 获取下一个待处理文件
    - 调用 `file-migrator [文件路径]` 升级该文件
    - 调用 `progress-tracker` 查看当前进度
    - 重复上述步骤直到所有文件完成

4. **验证阶段**
    - 调用 `progress-tracker` 查看最终报告
    - 调用 `migration-validator` 验证迁移结果

## 子智能体说明

每个子智能体均可独立运行，只需将对应的 `.md` 文件内容作为 prompt 传入 AI 工具，并提供必要的项目上下文。

### 初始化阶段子智能体

- `project-analyzer.md` - 分析项目结构和 Vue2 特性
- `task-initializer.md` - 扫描项目文件，创建任务队列

### 循环阶段子智能体

- `file-queue-manager.md` - 管理任务队列，获取下一个文件，更新状态
- `file-migrator.md` - 对单个文件执行所有迁移阶段

### 验证阶段子智能体

- `progress-tracker.md` - 查看当前升级进展和结果摘要（可随时执行）
- `migration-validator.md` - 验证所有文件的迁移结果

### 文件迁移阶段

在 `file-migrator` 内部依次执行以下阶段：

- **dependency-migrator** - 迁移依赖导入语句（适用所有文件）
- **global-api-migrator** - 迁移全局 API 调用（适用所有文件）
- **component-migrator** - 迁移组件 Options API 语法（仅 .vue 文件）
- **template-migrator** - 迁移模板语法（仅 .vue 文件）
- **style-migrator** - 迁移样式相关代码（仅 .vue 文件）
- **router-migrator** - 迁移 vue-router 相关代码（可选）
- **vuex-migrator** - 迁移 Vuex 相关代码（可选）

### Skills 迁移规则

子智能体执行时会自动加载对应的 skill 文件，该文件包含该阶段的迁移规则和代码示例：

| Skill | 描述 |
|-------|------|
| vue3-migration-dependency.md | 依赖导入迁移规则 |
| vue3-migration-breaking-changes.md | 破坏性变更列表 |
| vue3-migration-global-api.md | 全局 API 迁移规则 |
| vue3-migration-component.md | 组件语法迁移规则 |
| vue3-migration-template.md | 模板语法迁移规则 |
| vue3-migration-router.md | Vue Router 迁移规则 |
| vue3-migration-vuex.md | Vuex 迁移规则 |
| vue3-migration-style.md | 样式迁移规则 |
| vue3-migration-compat.md | @vue/compat 使用指南 |

Skill 采用渐进式披露模式，每个子智能体仅加载相关的 skill 文件，避免上下文污染。

## 任务队列文件

智能体会在项目根目录创建 `.vue3-upgrade-tasks.json` 文件，记录所有文件的迁移状态。

### 文件结构

```json
{
  "project": "项目名称",
  "created_at": "2025-01-17T00:00:00Z",
  "updated_at": "2025-01-17T01:00:00Z",
  "config": {
    "include_patterns": ["**/*.vue", "**/*.js", "**/*.ts"],
    "exclude_patterns": ["node_modules", "dist", ".git", ".vue3-upgrade-tasks.json"]
  },
  "files": [
    {
      "path": "src/components/Header.vue",
      "status": "pending",
      "phases": {}
    },
    {
      "path": "src/App.vue",
      "status": "completed",
      "phases": {
        "dependency": true,
        "global-api": true,
        "component": true,
        "template": true,
        "style": true,
        "router": false,
        "vuex": false
      },
      "completed_at": "2025-01-17T01:00:00Z",
      "changes": {
        "added_todos": 2,
        "issues": {"high": 0, "medium": 1, "low": 3}
      }
    }
  ],
  "summary": {
    "total": 150,
    "completed": 1,
    "pending": 148,
    "failed": 1,
    "progress": "0.7%"
  }
}
```

### 状态说明

- **pending**: 待处理
- **completed**: 已完成
- **failed**: 失败（不重试，需要用户手动处理）

## 注意事项

1. **文件级别迁移**：每个文件独立完成所有迁移阶段，可随时中断恢复
2. **任务跟踪**：所有状态保存在 `.vue3-upgrade-tasks.json`，建议添加到 `.gitignore`
3. **失败处理**：失败的文件不会自动重试，需要用户手动处理并标记状态
4. **上下文传递**：手动调用时需提供当前项目上下文和文件路径
5. **可回滚**：基于 Git 历史记录，每个文件的变更均可独立回滚
6. **渐进式**：优先使用 @vue/compat 迁移 build，逐步解决兼容性警告

## 中断恢复

- 每完成一个文件后，任务文件立即更新
- 用户可随时中断（Ctrl+C）
- 下次启动时自动从最后一个 completed 文件的下一个继续
- 用户可选择删除任务文件重新开始
