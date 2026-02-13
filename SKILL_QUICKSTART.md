# Skill 快速入门示例

本文档提供 3 个实战示例，帮助你快速掌握 VSCode Skill 的使用。

---

## 示例 1：使用现有的 agent-check Skill

### 场景
验证项目配置是否正确。

### 步骤

**1. 打开 VSCode Copilot 聊天**
- 快捷键: `Cmd + I` (macOS) 或 `Ctrl + I` (Windows/Linux)
- 或点击侧边栏的 Copilot 图标

**2. 输入命令**
```
请用 $agent-check 检查并执行 plan.json
```

**3. Copilot 会自动**:
- 读取 `/Users/haitian/kiro/rootrule/plan.json`
- 执行所有定义的检查任务
- 生成验证报告
- 显示执行结果

### 预期输出
```
✓ 验证 AGENTS.md 存在
✓ 验证 README.md 存在
✓ 验证 Git 仓库配置
```

---

## 示例 2：创建一个简单的 Skill

### 场景
创建一个检查 Python 代码风格的 skill。

### 步骤

**1. 在 VSCode Copilot 中输入**
```
请用 $skill-creator 创建一个 Python 代码风格检查 skill，功能包括：
1. 运行 black 格式化检查
2. 运行 pylint 代码质量检查
3. 检查 import 顺序
4. 生成检查报告
```

**2. Copilot 会创建**:
```
~/.codex/skills/python-style-check/
├── SKILL.md              # Skill 定义
├── scripts/
│   ├── check_format.sh   # Black 检查
│   ├── check_lint.sh     # Pylint 检查
│   └── check_imports.sh  # Import 检查
└── references/
    └── style_guide.md    # 风格指南
```

**3. 在项目中启用**

编辑 `AGENTS.md`，添加：
```markdown
### python-style-check
**路径**: `~/.codex/skills/python-style-check/SKILL.md`

**功能**: 检查 Python 代码风格和质量

**使用方式**:
\`\`\`
请用 $python-style-check 检查 src/ 目录下的代码
\`\`\`
```

**4. 使用新创建的 skill**
```
请用 $python-style-check 检查 src/ 目录下的代码
```

---

## 示例 3：组合使用多个 Skills

### 场景
在部署前执行完整的质量检查流程。

### 步骤

**1. 创建部署前检查 skill**

在 Copilot 中输入：
```
请用 $skill-creator 创建一个 pre-deploy skill，需要：
1. 检查所有测试通过
2. 验证代码覆盖率 > 80%
3. 检查没有未提交的更改
4. 验证 changelog 已更新
5. 检查版本号已更新
```

**2. 组合执行流程**

在 Copilot 中输入：
```
执行部署前检查流程：
1. 用 $python-style-check 检查代码风格
2. 用 $agent-check 验证配置文件
3. 用 $pre-deploy 执行部署前检查
如果所有检查通过，告诉我可以部署
```

**3. Copilot 会按顺序**:
- 运行代码风格检查
- 验证配置文件
- 执行部署前的所有检查
- 生成综合报告

### 预期输出
```
✓ 代码风格检查通过
✓ 配置文件验证通过
✓ 所有测试通过 (125/125)
✓ 代码覆盖率: 87%
✓ Git 状态干净
✓ changelog 已更新
✓ 版本号: v2.3.1

✅ 所有检查通过，可以部署！
```

---

## 常用命令速查

### 查询类
```
列出所有可用的 skills
请用 $skill-installer 列出可安装 skills
显示 agent-check skill 的详细信息
```

### 执行类
```
请用 $agent-check 检查并执行 plan.json
请用 $python-style-check 检查当前目录
请用 $deploy-prod 部署版本 v2.3.1
```

### 创建类
```
请用 $skill-creator 创建一个 [功能描述] skill
帮我创建一个用于自动化测试的 skill
我需要一个检查依赖更新的 skill
```

---

## 调试技巧

### 1. 检查 skill 是否正确安装
```bash
ls -la ~/.codex/skills/your-skill/SKILL.md
```

### 2. 查看 skill 内容
```bash
cat ~/.codex/skills/your-skill/SKILL.md
```

### 3. 测试 skill 脚本
```bash
cd ~/.codex/skills/your-skill
bash scripts/your-script.sh
```

### 4. 验证项目配置
```bash
cd /Users/haitian/kiro/rootrule
grep "your-skill" AGENTS.md
```

---

## 实用模板

### 最小化 SKILL.md 模板
```markdown
---
name: my-skill
description: 简短描述
---

# My Skill

功能说明。

## Workflow

1. 步骤一
   \`\`\`bash
   命令
   \`\`\`

## Execution Rules

- 规则 1
- 规则 2

## Quick Commands

\`\`\`bash
主要命令
\`\`\`
```

### AGENTS.md 条目模板
```markdown
### skill-name
**路径**: `~/.codex/skills/skill-name/SKILL.md`

**功能**: 功能描述

**使用方式**:
\`\`\`
请用 $skill-name 执行任务
\`\`\`
```

---

## 下一步

1. ✅ 尝试运行示例 1，熟悉基本用法
2. ✅ 根据示例 2 创建你的第一个 skill
3. ✅ 查看 [SKILL_GUIDE.md](SKILL_GUIDE.md) 了解更多高级特性
4. ✅ 探索 `~/.codex/skills/agent-check/` 学习复杂 skill 的结构

---

**提示**: 遇到问题？在 Copilot 中直接问：
```
agent-check skill 不工作，如何调试？
如何查看所有可用的 skills？
SKILL.md 的 description 字段有什么要求？
```

Copilot 会根据上下文和文档给你具体的解决方案！
