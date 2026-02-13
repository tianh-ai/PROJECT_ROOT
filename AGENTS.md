# Agent Skills Configuration

本项目启用以下 agent skills：

## Available Skills

### agent-check
**路径**: `~/.agents/skills/agent-check/SKILL.md`

**功能**: 从 plan.json 生成可执行的多代理队列，并对运行时/检查输出强制执行基于证据的严格验证。

**使用场景**:
1. 自动将 TODO 分区为具有依赖和路径约束的代理波次
2. 将生成的队列执行到可追溯的运行时事件流
3. 通过要求重放和证据哈希一致性来拒绝虚假/弱检查

**使用方式**:
```
请用 $agent-check 检查并执行 plan.json
```

---

## 如何使用 Skills

在 VSCode Copilot 聊天中，使用 `$skill-name` 语法调用 skill：

- `$agent-check` - 执行多代理检查流程
- `$skill-installer` - 列出可安装的 skills
- `$skill-creator` - 创建新的 skill

## Skill 开发

需要创建新 skill？使用：
```
请用 $skill-creator 帮我做一个 [功能描述] skill
```

## 技术说明

- Skills 存储在 `~/.agents/skills/` 目录
- 每个 skill 必须有 `SKILL.md` 文件
- Copilot 通过读取 SKILL.md 获取详细指令
