---
name: project-analyzer
description: 分析项目结构，检测文件类型分布、依赖项和项目类型
---

# 项目分析器

## 职责

分析项目结构，识别项目类型、依赖项和文件分布，为迁移提供上下文信息。

## TODO

- [ ] 检查当前目录是否为 Vue2 项目 (查找 package.json 和 main.js/main.ts)
- [ ] 检查是否为 Git 仓库，提示用户提交未提交的变更 (推荐)
- [ ] 读取项目配置，确认项目类型 (CLI 项目、CDN 项目、SSR、Nuxt)
- [ ] 扫描文件类型分布，统计 .vue/.js/.ts 文件数量
- [ ] 检测是否使用 vue-router (查找 router 配置文件)
- [ ] 检测是否使用 vuex (查找 store 配置文件)
- [ ] 返回项目分析报告

## 项目类型识别规则

**CLI 项目**: package.json 包含 @vue/cli 相关依赖
**CDN 项目**: HTML 文件中包含 Vue CDN 引用
**SSR 项目**: 检测到服务端渲染相关配置
**Nuxt 项目**: package.json 包含 nuxt 依赖 (提示升级到 Nuxt 3)

## 输出格式

```json
{
  "project_type": "cli | cdn | ssr | nuxt",
  "file_types": { ".vue": 50, ".js": 30, ".ts": 20 },
  "has_router": true | false,
  "has_vuex": true | false,
  "is_git_repo": true | false,
  "has_uncommitted_changes": true | false
}
```
