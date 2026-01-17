---
name: task-initializer
description: 扫描项目文件，创建 .vue3-upgrade-tasks.json 任务队列
---

# 任务初始化器

## 职责

扫描项目文件，创建任务队列文件。

## TODO

- [ ] 扫描项目目录，查找符合条件的文件
  - include_patterns: **/*.vue, **/*.js, **/*.ts
  - exclude_patterns: node_modules, dist, .git, .vue3-upgrade-tasks.json
- [ ] 为每个文件创建任务记录
  - path: 文件相对路径
  - status: "pending"
  - phases: {}
- [ ] 生成任务文件结构
  - project: 从 package.json 获取项目名称
  - created_at: 当前时间戳
  - updated_at: 当前时间戳
  - config: 包含/排除模式
  - files: 文件任务数组
  - summary: 初始统计 (total, completed=0, pending=total, failed=0, progress="0%")
- [ ] 保存到项目根目录 `.vue3-upgrade-tasks.json`

## 任务文件结构

```json
{
  "project": "项目名称",
  "created_at": "ISO时间戳",
  "updated_at": "ISO时间戳",
  "config": {
    "include_patterns": ["**/*.vue", "**/*.js", "**/*.ts"],
    "exclude_patterns": ["node_modules", "dist", ".git"]
  },
  "files": [
    {
      "path": "src/App.vue",
      "status": "pending" | "completed" | "failed",
      "phases": {},
      "completed_at": "ISO时间戳",
      "failed_at": "ISO时间戳",
      "changes": {
        "added_todos": 0,
        "issues": {"high": 0, "medium": 0, "low": 0}
      },
      "error": "错误信息"
    }
  ],
  "summary": {
    "total": 100,
    "completed": 10,
    "pending": 89,
    "failed": 1,
    "progress": "10%"
  }
}
```
