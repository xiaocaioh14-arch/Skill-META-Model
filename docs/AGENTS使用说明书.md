# AGENTS.md 使用说明书

> 面向用户的操作指南
> 版本：1.0.0
> 适配：Claude Code | Claude Cowork | AntiGravity

---

## 一、什么是 AGENTS.md？

AGENTS.md 是一个**跨工具 AI 协作规则文件**，遵循 Linux Foundation / Agentic AI Foundation 推动的标准。

**核心价值**：
- 让不同 AI 工具（Claude Code、Cowork、AntiGravity）遵循统一规则
- 实现 Skill 开发经验的自动积累
- 解决 AI 工具无跨会话记忆的问题

---

## 二、快速开始

### 2.1 初始化目录结构

首次使用前，请创建以下目录：

```bash
mkdir -p ~/Project/.handoff
mkdir -p ~/Project/.memory
touch ~/Project/.memory/decisions.md
```

### 2.2 确认文件位置

确保以下文件已存在：
- `~/Project/AGENTS.md` — 本规则文件
- `~/Project/SKILL_META_MODEL.md` — Skill 开发元模型
- `~/Project/SKILLS_INDEX.md` — Skill 统一索引

---

## 三、核心功能使用

### 3.1 Skill 元模型自动更新

**场景**：你刚用 Claude Code 开发完一个新 Skill。

**触发方式（4选1）**：

| 方式 | 操作 | 适用场景 |
|------|------|----------|
| 自动触发 | 会话中创建/修改了 SKILL.md | 最常用 |
| 命令触发 | 输入 `/update-meta-model` | 主动触发 |
| 口语触发 | 说「更新元模型」 | 自然交流 |
| 结束触发 | 说「完成」或「done」 | 任务收尾 |

**实际操作示例**：

```
你（在 Claude Code 中）：完成了，帮我更新一下元模型

Claude Code：好的，让我分析本次 Skill 开发中的新模式...
[读取 SKILL_META_MODEL.md]
[分析新 Skill 的创新点]
[更新元模型和索引]

✅ 已更新：
- SKILL_META_MODEL.md：新增模式 10「多源数据聚合」
- SKILLS_INDEX.md：新增「新 Skill 名称」条目
```

---

### 3.2 会话交接（Handoff）

**场景**：今天的任务完成了，想保存上下文供下次继续。

**触发方式**：
```
你：/handoff
或：帮我保存一下今天的上下文
或：记录一下今天做的事情
```

**生成内容示例**：

文件位置：`~/Project/.handoff/handoff_001_skill开发_2026-01-30.md`

```markdown
# Handoff: Skill 开发 - 海外运营商分析
> 日期：2026-01-30
> 工具：Claude Code
> 会话时长：2小时

## 完成的任务
- [x] 创建 SKILL.md 基础框架
- [x] 实现 4 层 IEPL 估算模型
- [x] 完成双报告架构（综合版 + 批发版）

## 关键决策
| 决策 | 理由 |
|------|------|
| 使用 5 维度加权评分 | 覆盖海缆、IEPL、批发、技术、财务全面分析 |
| 输出 5 文件 | 满足不同阅读场景需求 |

## 未完成待办
- [ ] 添加历史数据对比功能
- [ ] 优化 HTML 报告的图表展示

## 后续建议
下次从「历史数据对比」功能开始
```

---

### 3.3 快速简报（Brief）

**场景**：换到另一个 AI 工具，想快速了解当前项目状态。

**触发方式**：
```
你（在 Cowork 中）：/brief
或：给我一个当前状态简报
```

**AI 行为**：
1. 读取 `~/Project/.handoff/HANDOFF_LATEST.md`
2. 读取 `~/Project/SKILLS_INDEX.md`
3. 生成简报

---

### 3.4 记录重要决策

**场景**：做了一个可能影响后续开发的决策。

**触发方式**：
```
你：/remember 决定使用 TypeScript 而不是 Python，因为需要与前端共享类型
或：帮我记录一下这个决策
```

**记录位置**：`~/Project/.memory/decisions.md`

---

## 四、跨工具协作流程

### 4.1 推荐的工具分工

```
┌─────────────────────────────────────────────────────────────┐
│                      日常工作流程                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  1. 上下文聚合（Cowork）                                     │
│     └─ 读取各工具上下文，生成统一视图                         │
│                    ↓                                        │
│  2. 深度代码开发（Claude Code）                              │
│     └─ 编写代码，Git 操作，Skill 开发                        │
│                    ↓                                        │
│  3. 单一代码库分析（AntiGravity）                            │
│     └─ 代码理解，重构建议，Bug 定位                          │
│                    ↓                                        │
│  4. 深度研究（Desktop Chat）                                 │
│     └─ Deep Research，市场调研，技术选型                     │
│                    ↓                                        │
│  5. 元模型更新（任意工具）                                   │
│     └─ /update-meta-model                                   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 4.2 实际场景示例

**场景：开发一个新 Skill**

```
步骤 1（Cowork）：
你：帮我看看我现有的 Skills，找找有没有可以参考的模式
Cowork：[读取 SKILL_META_MODEL.md 和 SKILLS_INDEX.md]
       推荐参考「每日线路资源日报」的静默执行模式...

步骤 2（Claude Code）：
你：根据元模型开始开发「XXX Skill」
Claude Code：[开发完成]

步骤 3（Claude Code）：
你：完成了
Claude Code：[触发规则 1，自动更新元模型]

步骤 4（任意工具，下次会话）：
你：/brief
AI：[读取最新 handoff，汇报上次进度]
```

---

## 五、常见问题

### Q1：AGENTS.md 放在哪里最好？

**推荐**：`~/Project/AGENTS.md`（项目根目录）

原因：
- Claude Code 会自动读取项目目录下的 AGENTS.md
- Cowork 可以通过 Desktop Commander 访问
- AntiGravity 也能识别

### Q2：如果我不想自动更新元模型怎么办？

可以在触发条件前说：「不用更新元模型」

### Q3：Handoff 文件会越来越多怎么办？

建议定期清理：
- 保留最近 10 个 handoff 文件
- 旧的归档到 `~/Project/.handoff/archive/`

### Q4：多人协作时 AGENTS.md 会冲突吗？

AGENTS.md 是规则文件，通常不需要频繁修改。
建议：
- 规则变更通过 PR 讨论
- 使用 Git 管理版本

### Q5：如何让新的 AI 工具也遵循这些规则？

只要该工具：
1. 支持读取本地文件
2. 能理解 AGENTS.md 标准格式

就可以自动遵循规则。

---

## 六、命令速查表

| 命令 | 作用 | 示例 |
|------|------|------|
| `/update-meta-model` | 更新 Skill 元模型 | 开发完 Skill 后使用 |
| `/handoff` | 保存会话上下文 | 结束工作时使用 |
| `/brief` | 获取状态简报 | 开始新会话时使用 |
| `/remember [内容]` | 记录重要决策 | 做出关键决策时使用 |
| `/skills` | 显示 Skill 列表 | 查看可用 Skill |

---

## 七、文件路径速查

```yaml
规则文件:
  ~/Project/AGENTS.md

元模型:
  ~/Project/SKILL_META_MODEL.md
  ~/Project/SKILLS_INDEX.md

交接记录:
  ~/Project/.handoff/HANDOFF_LATEST.md
  ~/Project/.handoff/handoff_*.md

决策记忆:
  ~/Project/.memory/decisions.md

各工具上下文:
  Claude Code: ~/.claude/
  AntiGravity: ~/.gemini/antigravity/
```

---

## 八、故障排除

### 元模型没有自动更新？

检查：
1. 是否满足触发条件（创建/修改了 SKILL.md）
2. AI 工具是否有权限读取 ~/Project/ 目录
3. SKILL_META_MODEL.md 是否存在

### Handoff 文件找不到？

检查：
1. `~/Project/.handoff/` 目录是否存在
2. HANDOFF_LATEST.md 是否指向正确文件

### 跨工具读取失败？

对于 Cowork：
1. 确认已启用 Desktop Commander MCP 插件
2. 确认目标目录在允许访问范围内

---

*使用愉快！如有问题，欢迎反馈。*
