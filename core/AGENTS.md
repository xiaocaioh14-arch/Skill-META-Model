# AGENTS.md - 跨工具 AI 协作规则

> 适用于：Claude Code | Claude Cowork | AntiGravity | 其他遵循 AGENTS.md 标准的 AI 工具
> 版本：1.0.0
> 更新日期：2026-01-30

---

## 一、文档说明

本文档遵循 Linux Foundation / Agentic AI Foundation 推动的 AGENTS.md 标准。
任何读取此文件的 AI 工具都应遵守以下规则。

**核心目录结构**：
```
~/Project/
├── AGENTS.md                    # 本文件（跨工具共享规则）
├── SKILL_META_MODEL.md          # Skill 开发元模型
├── SKILLS_INDEX.md              # Skill 统一索引
├── .handoff/                    # 会话交接目录
│   └── HANDOFF_LATEST.md        # 最新会话记录
└── .memory/                     # 持久化记忆目录
    └── decisions.md             # 重要决策记录
```

---

## 二、规则定义

### 规则 1：Skill 元模型自动更新

**目的**：确保 SKILL_META_MODEL.md 始终反映最新的开发模式和最佳实践。

**触发条件（满足任一即触发）**：
```yaml
触发条件 A: 本次会话创建了新的 SKILL.md 文件
触发条件 B: 本次会话修改了现有的 SKILL.md 文件
触发条件 C: 用户明确说"更新元模型"或"/update-meta-model"
触发条件 D: 会话结束时，用户说"完成"/"结束"/"done"，且本次涉及 Skill 开发
```

**执行动作**：
```yaml
步骤 1: 读取 ~/Project/SKILL_META_MODEL.md
步骤 2: 分析本次 Skill 开发中的新模式、新技术、新架构
步骤 3: 识别可复用的设计模式（与现有模式对比，避免重复）
步骤 4: 更新元模型文档，添加新发现的模式
步骤 5: 同步更新 ~/Project/SKILLS_INDEX.md
步骤 6: 输出更新摘要
```

**更新格式**：
```markdown
### 模式 N：[模式名称]
**来源 Skill**：[skill 名称]
**适用场景**：[描述]
**核心实现**：
[代码或结构示例]
```

---

### 规则 2：会话交接（Handoff）

**目的**：解决 AI 工具无跨会话记忆的问题，确保上下文连续性。

**触发条件**：
```yaml
触发条件 A: 用户说"handoff"/"交接"/"保存上下文"
触发条件 B: 复杂任务完成后，用户说"记录一下"
触发条件 C: 用户明确指定 /handoff 命令
```

**执行动作**：
```yaml
步骤 1: 生成 handoff 文件名：handoff_[序号]_[主题]_[日期].md
步骤 2: 提取本次会话的：
        - 完成的任务
        - 关键决策及理由
        - 未完成的待办
        - 相关文件路径
        - 后续建议
步骤 3: 保存到 ~/Project/.handoff/
步骤 4: 更新 ~/Project/.handoff/HANDOFF_LATEST.md 指向新文件
```

**Handoff 文件模板**：
```markdown
# Handoff: [主题]
> 日期：[日期]
> 工具：[Claude Code / Cowork / AntiGravity]
> 会话 ID：[如有]

## 完成的任务
- [ ] 任务 1
- [ ] 任务 2

## 关键决策
| 决策 | 理由 | 影响范围 |
|------|------|----------|
| ... | ... | ... |

## 未完成待办
- [ ] 待办 1
- [ ] 待办 2

## 相关文件
- `path/to/file1`
- `path/to/file2`

## 后续建议
[下一个会话应该从哪里开始]
```

---

### 规则 3：禁止操作清单

以下操作在任何情况下都**禁止**AI 工具自动执行：

```yaml
文件操作:
  - 删除用户未明确指定的文件
  - 修改 ~/.ssh/、~/.gnupg/ 等敏感目录
  - 覆盖已存在的文件（除非用户明确确认）

Git 操作:
  - git push --force
  - git reset --hard（未确认）
  - 修改 .gitignore 添加敏感文件

系统操作:
  - 修改系统配置文件
  - 安装系统级软件包（未确认）
  - 修改环境变量（永久性）

网络操作:
  - 发送用户数据到外部服务器
  - 下载并执行未知脚本
  - 访问用户未指定的 API
```

---

### 规则 4：跨工具协作

**场景定义**：

| 场景 | 推荐工具 | 原因 |
|------|----------|------|
| 深度代码开发 | Claude Code | 完整终端权限，Git 集成 |
| 单一代码库理解 | AntiGravity | 深度代码分析，上下文持久化 |
| 跨工具上下文聚合 | Cowork | 可读取多工具配置目录 |
| 文档生成（MD/HTML） | Cowork | Skills 支持，格式丰富 |
| Deep Research | Desktop Chat | 内置深度研究能力 |

**上下文路径索引**：

```yaml
Claude Code:
  配置目录: ~/.claude/
  项目记录: ~/.claude/projects/
  全局规则: ~/.claude/CLAUDE.md

AntiGravity:
  上下文目录: ~/.gemini/antigravity/
  会话记录: ~/.gemini/antigravity/sessions/
  Skills: ~/.gemini/antigravity/skills/

Cowork:
  工作目录: ~/Project/（用户选择）
  Skills: ~/Project/.skills/
```

---

### 规则 5：输出标准

**文件格式优先级**：
```yaml
优先级 1: Markdown (.md)
  - AI 最友好，便于后续处理
  - Git 版本控制友好
  - 跨平台兼容

优先级 2: HTML
  - 需要富媒体展示时
  - 需要直接分享给非技术用户时

优先级 3: 专业格式 (PPTX/DOCX/XLSX)
  - 用户明确要求时
  - 需要与传统办公软件协作时
```

**文件命名规范**：
```yaml
Skill 文件: SKILL.md（大写）
配置文件: config.yaml 或 settings.json
输出报告: [主题]_[日期].md
临时文件: tmp_[描述].[ext]
```

**代码注释要求**：
```yaml
- 关键函数必须有文档字符串
- 复杂逻辑需要行内注释
- TODO/FIXME 需标注日期和负责人
```

---

### 规则 6：记忆与学习

**决策记录**：

当做出重要决策时，记录到 `~/Project/.memory/decisions.md`：

```markdown
## [日期] [决策标题]
**背景**：[为什么需要做这个决策]
**选项**：
1. 选项 A：[描述] - 优点/缺点
2. 选项 B：[描述] - 优点/缺点
**最终选择**：[选项 X]
**理由**：[为什么选择这个]
**影响**：[这个决策会影响什么]
```

**学习记录**：

当发现新的最佳实践时，更新相应的元模型或索引文档。

---

## 三、快速命令索引

| 命令 | 作用 | 触发方式 |
|------|------|----------|
| `/update-meta-model` | 更新 Skill 元模型 | 任何工具 |
| `/handoff` | 保存会话上下文 | 任何工具 |
| `/brief` | 生成当前状态简报 | 任何工具 |
| `/remember [内容]` | 记录重要决策 | 任何工具 |
| `/skills` | 显示可用 Skills 列表 | Cowork / AntiGravity |

---

## 四、版本历史

| 版本 | 日期 | 变更 |
|------|------|------|
| 1.0.0 | 2026-01-30 | 初始版本，包含 6 条核心规则 |

---

*本文档由 Eddie 和 Claude Cowork 协作创建*
*遵循 AGENTS.md 标准 v1.0*
