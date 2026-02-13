# rootrule

基于规则的 LLM 项目管理框架。

---

## ❗ 硬性规则（任何模型必须遵守）

| 规则 | 说明 |
|------|------|
| 🟢 **只能修改** | `WORK/` 目录 |
| 🔴 **不得修改** | `META/` 与 `RULES/` 目录 |
| ⚠️ **修改前必须** | 通过 `RULES/LLM_CHECKLIST.md` 自检 |

> **违反以上任意一条 = 非法操作，必须立即停止**

---

## 📁 目录结构

```
PROJECT_ROOT/
├── META/
│   └── PROJECT_META.md        # 冻结区 - 项目元数据
├── RULES/
│   ├── LLM_CHECKLIST.md       # 核心 - LLM 执行检查清单
│   └── CHANGE_LOG.md          # 变更记录（只追加）
├── WORK/
│   └── ...                    # 所有可变内容
└── README.md                  # 本文件
```

## 📖 目录说明

| 目录/文件 | 用途 | 可变性 |
|-----------|------|--------|
| `META/` | 项目元数据冻结区 | 🔒 冻结 |
| `RULES/` | 规则与检查清单 | ⚠️ 谨慎修改 |
| `WORK/` | 日常工作区 | ✅ 自由修改 |

## 🚀 快速开始

1. 在 `WORK/` 目录下进行日常开发工作
2. 遵循 `RULES/LLM_CHECKLIST.md` 中的检查清单
3. 重要变更记录到 `RULES/CHANGE_LOG.md`

## 🤖 Agent Skills

本项目启用了 Agent Skills 系统，可在 VSCode Copilot 中使用 `$skill-name` 调用专业能力：

- 📋 查看 [AGENTS.md](AGENTS.md) 了解可用的 skills
- 📚 阅读 [SKILL_GUIDE.md](SKILL_GUIDE.md) 学习如何创建和使用 skills
- 🔧 使用 `$agent-check` 执行计划验证流程
- 📦 使用 `$skill-installer` 列出可安装的 skills
- ✨ 使用 `$skill-creator` 创建新的 skill

**示例**:
```
请用 $agent-check 检查并执行 plan.json
```

## 📜 规则

- **META 目录**：冻结区，非特殊情况不可修改
- **RULES 目录**：规则文件，修改需谨慎
- **WORK 目录**：自由工作区，所有可变内容放置于此
- **变更记录**：重要变更需追加到 CHANGE_LOG.md

---

**创建日期**: 2026-01-20
