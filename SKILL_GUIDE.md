# VSCode Skill 创建与使用完整指南

## 📚 目录
1. [什么是 Skill](#什么是-skill)
2. [Skill 目录结构](#skill-目录结构)
3. [创建新 Skill](#创建新-skill)
4. [在项目中启用 Skill](#在项目中启用-skill)
5. [使用 Skill](#使用-skill)
6. [实战示例](#实战示例)

---

## 什么是 Skill

**Skill** 是 GitHub Copilot 的领域特定知识增强模块，包含：
- 详细的执行指令
- 工作流程定义
- 命令模板
- 最佳实践

当你在 VSCode 聊天中使用 `$skill-name` 时，Copilot 会：
1. 读取对应的 `SKILL.md` 文件
2. 获取详细的领域知识
3. 按照 skill 定义的流程执行任务

---

## Skill 目录结构

### 系统位置
```
~/.codex/skills/          # 主 skills 目录
├── .system/              # 系统内置 skills
└── your-skill/           # 自定义 skill
    ├── SKILL.md          # 必需：技能定义文件
    ├── scripts/          # 可选：执行脚本
    ├── references/       # 可选：参考文档
    └── examples/         # 可选：示例代码
```

### SKILL.md 基本结构

```markdown
---
name: your-skill-name
description: 简短描述（一句话说明用途和场景）
---

# Skill 标题

详细说明这个 skill 的用途和使用场景。

## Workflow

1. 步骤一：做什么
   - 具体操作
   - 命令示例

2. 步骤二：做什么
   - 具体操作

## Execution Rules

- 规则 1
- 规则 2

## Quick Commands

常用命令速查：

\`\`\`bash
命令示例
\`\`\`

## Resources

- 相关文件说明
- 参考资料
```

---

## 创建新 Skill

### 方法 1：手动创建

**步骤 1**: 创建目录结构
```bash
mkdir -p ~/.codex/skills/my-skill/{scripts,references,examples}
cd ~/.codex/skills/my-skill
```

**步骤 2**: 创建 SKILL.md
```bash
cat > SKILL.md << 'EOF'
---
name: my-skill
description: 这是我的第一个自定义 skill，用于演示如何创建 skill
---

# My Custom Skill

这个 skill 演示了基本的 skill 结构。

## Workflow

1. 初始化环境
   ```bash
   echo "初始化完成"
   ```

2. 执行主要任务
   - 任务描述

## Execution Rules

- 遵循项目规范
- 验证输出结果

## Quick Commands

快速启动：
\`\`\`bash
bash scripts/run.sh
\`\`\`
EOF
```

**步骤 3**: 添加支持脚本（可选）
```bash
cat > scripts/run.sh << 'EOF'
#!/bin/bash
echo "Running my-skill..."
# 你的逻辑
EOF
chmod +x scripts/run.sh
```

### 方法 2：使用 skill-creator（推荐）

在 VSCode Copilot 聊天中：
```
请用 $skill-creator 帮我创建一个用于代码审查的 skill
```

Copilot 会自动：
- 创建目录结构
- 生成 SKILL.md 模板
- 创建必要的脚本文件

---

## 在项目中启用 Skill

### 步骤 1：创建 AGENTS.md

在项目根目录创建 `AGENTS.md`（如果还没有）：

```markdown
# Agent Skills Configuration

本项目启用以下 agent skills：

## Available Skills

### my-skill
**路径**: `~/.codex/skills/my-skill/SKILL.md`

**功能**: skill 的功能描述

**使用方式**:
\`\`\`
请用 $my-skill 执行 xxx
\`\`\`

---

### agent-check
**路径**: `~/.codex/skills/agent-check/SKILL.md`

**功能**: 多代理队列执行和验证

**使用方式**:
\`\`\`
请用 $agent-check 检查并执行 plan.json
\`\`\`
```

### 步骤 2：提交到版本控制

```bash
git add AGENTS.md
git commit -m "docs: 添加 agent skills 配置"
```

---

## 使用 Skill

### 在 VSCode Copilot 聊天中调用

**基本语法**:
```
请用 $skill-name [参数或描述]
```

**示例**:

1. **执行检查流程**
   ```
   请用 $agent-check 检查并执行 plan.json
   ```

2. **列出可用 skills**
   ```
   请用 $skill-installer 列出可安装 skills
   ```

3. **创建新 skill**
   ```
   请用 $skill-creator 帮我做一个用于性能测试的 skill
   ```

4. **自定义 skill**
   ```
   请用 $my-skill 分析当前项目的代码质量
   ```

### Skill 工作原理

当你输入 `$skill-name` 时：

```
用户输入: 请用 $agent-check 检查并执行 plan.json
    ↓
Copilot 识别: $agent-check
    ↓
读取文件: ~/.codex/skills/agent-check/SKILL.md
    ↓
加载指令: 获取详细的工作流程和规则
    ↓
执行任务: 按照 SKILL.md 中定义的步骤操作
    ↓
返回结果: 完成任务并报告
```

---

## 实战示例

### 示例 1：使用 agent-check

**场景**: 验证项目的构建流程

**步骤**:

1. 确保项目有 `AGENTS.md` 和 `plan.json`
   ```bash
   ls -l AGENTS.md plan.json
   ```

2. 在 VSCode Copilot 聊天中输入：
   ```
   请用 $agent-check 检查并执行 plan.json
   ```

3. Copilot 会自动：
   - 读取 plan.json
   - 生成执行队列
   - 运行所有检查
   - 生成验证报告

### 示例 2：创建代码审查 Skill

**需求**: 自动化代码审查流程

1. **创建 skill**
   ```
   请用 $skill-creator 帮我创建一个代码审查 skill，需要检查：
   - Python 代码风格（PEP 8）
   - TypeScript 类型安全
   - Git commit 规范
   ```

2. **Copilot 会生成**:
   ```
   ~/.codex/skills/code-review/
   ├── SKILL.md
   ├── scripts/
   │   ├── check_python.sh
   │   ├── check_typescript.sh
   │   └── check_commits.sh
   └── references/
       └── style_guide.md
   ```

3. **在项目中启用**
   在 `AGENTS.md` 中添加：
   ```markdown
   ### code-review
   **路径**: `~/.codex/skills/code-review/SKILL.md`
   **使用**: `请用 $code-review 审查当前分支的代码`
   ```

4. **使用**
   ```
   请用 $code-review 审查当前分支的代码
   ```

### 示例 3：创建部署 Skill

```
请用 $skill-creator 创建一个部署 skill，包括：
- 构建 Docker 镜像
- 运行测试
- 推送到 registry
- 更新 Kubernetes 配置
```

---

## 最佳实践

### ✅ DO（推荐做法）

1. **明确的 skill 名称**
   - ✅ `code-review`, `deploy-prod`, `test-integration`
   - ❌ `skill1`, `my-tool`, `thing`

2. **详细的 Workflow**
   - 每个步骤都有清晰的命令
   - 包含错误处理说明
   - 提供示例输出

3. **版本化的参考文档**
   ```
   references/
   ├── v1.0-workflow.md
   ├── v2.0-workflow.md
   └── migration-guide.md
   ```

4. **在 AGENTS.md 中声明**
   - 让团队知道可用的 skills
   - 提供使用示例
   - 记录前置条件

### ❌ DON'T（避免）

1. **不要在 SKILL.md 中硬编码路径**
   - ❌ `/Users/alice/project/data`
   - ✅ `${PROJECT_ROOT}/data`

2. **不要遗漏错误处理**
   ```bash
   # ❌ 不好
   python script.py
   
   # ✅ 好
   python script.py || { echo "失败"; exit 1; }
   ```

3. **不要创建过于笼统的 skill**
   - ❌ "处理所有东西"的超级 skill
   - ✅ 专注于单一职责的多个 skills

---

## 常见问题

### Q1: Skill 不生效？
**检查清单**:
- [ ] SKILL.md 文件存在于 `~/.codex/skills/your-skill/`
- [ ] SKILL.md 有正确的 YAML frontmatter
- [ ] 项目根目录有 AGENTS.md
- [ ] AGENTS.md 中声明了该 skill

### Q2: 如何调试 Skill？
```bash
# 1. 验证 skill 文件存在
ls -la ~/.codex/skills/your-skill/SKILL.md

# 2. 检查 SKILL.md 格式
head -10 ~/.codex/skills/your-skill/SKILL.md

# 3. 测试单个命令
bash scripts/your-script.sh
```

### Q3: 如何分享 Skill？
```bash
# 方法 1: 打包为 tar
cd ~/.codex/skills
tar -czf my-skill.tar.gz my-skill/

# 方法 2: Git 仓库
cd my-skill
git init
git add .
git commit -m "Initial skill"
git remote add origin https://github.com/user/my-skill
git push -u origin main

# 其他人安装
cd ~/.codex/skills
git clone https://github.com/user/my-skill
```

### Q4: Skill 和普通脚本的区别？
| 特性 | Skill | 普通脚本 |
|------|-------|---------|
| AI 集成 | ✅ Copilot 自动理解 | ❌ 需要手动说明 |
| 上下文感知 | ✅ 读取 SKILL.md | ❌ 无上下文 |
| 工作流编排 | ✅ 多步骤协调 | ❌ 单一执行 |
| 文档内嵌 | ✅ SKILL.md 即文档 | ❌ 需要额外文档 |

---

## 高级技巧

### 1. Skill 组合使用

```
请先用 $code-review 检查代码，
然后用 $test-integration 运行集成测试，
最后用 $deploy-staging 部署到预发环境
```

### 2. 条件执行

在 SKILL.md 中定义：
```markdown
## Execution Rules

- 如果 `git status --porcelain` 非空，拒绝执行
- 如果 `tests/` 目录不存在，跳过测试步骤
- 如果 `staging` 环境不可用，回退到 `dev`
```

### 3. 参数化 Skill

```
请用 $deploy-prod 部署版本 v2.3.1 到 us-west-2 区域
```

在 SKILL.md 中处理参数：
```markdown
## Workflow

1. 解析参数：版本号、区域
2. 验证版本存在
3. 切换到指定区域
4. 执行部署
```

---

## 相关资源

- 📂 Skills 目录: `~/.codex/skills/`
- 📄 当前项目配置: [AGENTS.md](/Users/haitian/kiro/rootrule/AGENTS.md)
- 📋 示例计划: [plan.json](/Users/haitian/kiro/rootrule/plan.json)
- 🔧 agent-check skill: `~/.codex/skills/agent-check/SKILL.md`

---

## 快速参考卡片

```bash
# 创建新 skill
mkdir -p ~/.codex/skills/my-skill
cd ~/.codex/skills/my-skill
touch SKILL.md

# 列出所有 skills
ls -1 ~/.codex/skills/

# 在项目中启用
echo "### my-skill" >> AGENTS.md

# 使用 skill
# 在 VSCode Copilot 聊天中输入：
# 请用 $my-skill 执行任务
```

---

**最后更新**: 2026-02-13
**版本**: 1.0.0
