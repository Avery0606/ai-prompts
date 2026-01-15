# AI 提示词 - 智能体开发指南

本仓库包含 AI 智能体定义和提示词。贡献时请遵循以下指南。

## 项目结构

```
ai-prompts/
├── agents/                  # Agent definitions directory
│   └── *.md                # Individual agent files
├── AGENTS.md               # This file
├── LICENSE                 # MIT License
└── README.md              # Project documentation
```

## 可用命令

由于这是内容仓库，无构建系统，可用操作包括：

### Git 操作
- `git add .` - 暂存所有更改
- `git commit -m "message"` - 提交更改
- `git push` - 推送到远程仓库

### 文件管理
- 在 `agents/` 目录中创建新智能体
- 所有智能体文件使用 `.md` 扩展名
- 遵循现有命名约定：`agent-name.md`

## Agent Definition Format

All agent files must follow this structure:

```yaml
---
name: agent-name
description: Brief description in Chinese
color: gray|blue|green|yellow|red|purple
model: haiku|sonnet|gpt-4|claude-3
tools: Bash,Glob,Read,Write,Edit,Grep,WebFetch,WebSearch
---

# Agent Title (Chinese)

## 任务描述
[Detailed task description in Chinese]

## 工具使用规则
[Specific tool usage guidelines]

## 输出要求
[Output format requirements]

## 注意事项
[Important notes and constraints]
```

## 代码风格指南

### 文件命名
- 智能体文件名使用 kebab-case：`my-agent.md`
- 保持名称描述性和简洁性
- 文件名使用英文，描述使用中文

### YAML 前置元数据要求
- `name`: kebab-case，唯一标识符
- `description`: 中文，简短（1-2句话）
- `color`: 从预定义颜色中选择
- `model`: 指定推荐模型
- `tools`: 逗号分隔的可用工具列表

### 内容指南
- 所有描述和内容使用中文
- 使用清晰的标题结构（##）
- 明确工具使用和输出要求
- 包含约束和限制

### 工具声明
只包含智能体实际需要的工具：
- `Bash` - 用于命令执行
- `Glob` - 用于文件模式匹配
- `Read` - 用于读取文件
- `Write` - 用于创建文件
- `Edit` - 用于修改文件
- `Grep` - 用于内容搜索
- `WebFetch` - 用于网页内容检索
- `WebSearch` - 用于网页搜索

## 测试和验证

### 手动测试
1. 使用示例输入测试智能体
2. 验证工具使用是否适当
3. 检查输出格式合规性
4. 验证中文语言准确性

### 智能体验证清单
- [ ] YAML 前置元数据完整且有效
- [ ] 智能体名称唯一且遵循命名约定
- [ ] 描述清晰且使用中文
- [ ] 工具列表准确且最小化
- [ ] 任务描述具体且可操作
- [ ] 输出要求定义明确
- [ ] 约束和限制清晰说明

## 导入和组织

### 智能体分类
按目的组织智能体：
- **开发**: 代码相关任务
- **自动化**: 脚本执行和系统任务
- **分析**: 数据处理和内容分析
- **通信**: 文本生成和格式化

### 文件组织
- 每个文件一个智能体
- 使用描述性文件名
- 在目录中保持字母顺序
- 除非绝对必要，否则避免子目录

## 错误处理指南

### Agent Robustness
- Specify error handling in task description
- Define fallback behavior for tool failures
- Include validation steps for inputs
- Provide clear error messages in Chinese

### Tool Usage Safety
- Specify when to use `workdir` parameter for Bash
- Define file path handling rules
- Include safety constraints for system operations
- Specify when to avoid destructive operations

## 命名约定

### Agent Names
- Use kebab-case
- Be descriptive but concise
- Use English only
- Avoid special characters

### Content Headings
- Use Chinese for all headings
- Follow hierarchical structure (#, ##, ###)
- Be consistent with existing agents

## 质量标准

### Content Quality
- All descriptions must be in Chinese
- Tasks must be specific and measurable
- Output requirements must be testable
- Include examples where helpful

### Technical Quality
- YAML must be valid
- Tool declarations must be accurate
- File references must be correct
- No broken links or references

## 贡献流程

1. Create new agent file in `agents/` directory
2. Follow the format and style guidelines
3. Test manually with sample scenarios
4. Validate against checklist
5. Commit with descriptive message
6. Create pull request for review

## Review Criteria

Agents will be reviewed for:
- Format compliance
- Chinese language accuracy
- Tool appropriateness
- Task clarity
- Output specificity
- Safety considerations

---

## 持久记忆设置

### 中文对话模式
- 本仓库默认使用中文进行所有交流和文档编写
- 智能体定义必须使用中文描述任务和要求
- 错误信息和输出内容使用中文
- 代码注释和文档使用中文

### 持久记忆规则
1. 所有智能体都应记住使用中文对话
2. 保持中文语言的一致性和准确性
3. 在工具调用和代码操作中使用中文注释
4. 错误处理和反馈使用中文表达