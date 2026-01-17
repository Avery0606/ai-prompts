---
name: file-queue-manager
description: 管理任务队列，获取下一个待处理文件，更新任务文件状态
---

# 任务队列管理器

## 职责

维护任务队列，按顺序分配待处理文件，记录文件迁移结果。

## TODO

### 获取下一个待处理文件
- [ ] 读取项目根目录的 `.vue3-upgrade-tasks.json` 文件
- [ ] 遍历 files 数组，查找第一个 `status: "pending"` 的文件
- [ ] 返回该文件的路径
- [ ] 如无 pending 文件，返回 null 表示迁移完成

### 更新文件状态
- [ ] 接收 file-migrator 的执行结果 (status, phases, changes, error)
- [ ] 更新任务文件中对应文件的:
  - status 字段
  - completed_at 或 failed_at 时间戳
  - phases 数组（记录完成的阶段）
  - changes 统计（added_todos, issues）
  - error 信息（失败时）
- [ ] 重新计算 summary 统计 (total, completed, pending, failed, progress)
- [ ] 更新 updated_at 时间戳
- [ ] 保存任务文件

## 文件选择策略

- 按文件路径字母顺序处理，确保一致性
- 每次只处理一个文件，完成后立即更新任务文件
- 失败的文件不会重试，需要用户手动处理后标记为 completed

## 任务文件字段说明

- `project`: 项目名称
- `created_at`: 任务队列创建时间
- `updated_at`: 任务队列最后更新时间
- `config`: 包含和排除的文件模式
- `files`: 文件列表
  - `path`: 文件相对路径
  - `status`: 状态（pending/completed/failed）
  - `phases`: 各阶段完成情况（completed 文件）
  - `completed_at` / `failed_at`: 完成或失败时间
  - `changes`: 变更统计（completed 文件）
  - `error`: 错误信息（failed 文件）
- `summary`: 统计摘要
  - `total`: 总文件数
  - `completed`: 已完成数
  - `pending`: 待处理数
  - `failed`: 失败数
  - `progress`: 进度百分比
