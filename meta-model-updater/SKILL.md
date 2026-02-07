---
name: meta-model-updater
description: 自动分析新 Skill 并更新元模型，识别可复用的设计模式
license: MIT
triggers:
  - "更新元模型"
  - "update meta model"
  - "分析新模式"
  - "同步元模型"
slash_commands:
  - command: /update-meta-model
    description: 分析最近修改的 Skill 并更新元模型
    usage: /update-meta-model [skill-path]
---

# 📊 元模型自动更新器

> **自动化 AGENTS.md 规则 1 的执行**
> 分析新开发的 Skill，识别可复用的设计模式，并更新 SKILL_META_MODEL.md

---

## 🔇 静默执行协议 (Quiet Mode Protocol)

> [!CRITICAL]
> **必须严格遵守以下原子性执行原则：**
>
> 1. **禁止中途询问** — 不要问"是否继续？"、"需要确认吗？"
> 2. **一次性完整输出** — 收到触发后，完整执行所有步骤
> 3. **静默决策** — 自动判断是否有新模式需要添加
> 4. **错误静默处理** — 错误记录在摘要中，不中断流程
> 5. **缺失即跳过** — 如果找不到新 Skill，输出提示后退出

---

## 1. 核心功能

### 1.1 触发场景

本 Skill 自动执行 AGENTS.md 中的"规则 1: Skill 元模型自动更新"。

**触发时机**（满足任一即可）：
- ✅ 用户明确说"更新元模型"或使用 `/update-meta-model`
- ✅ 本次会话创建或修改了 SKILL.md 文件
- ✅ 会话结束时用户说"完成"/"结束"，且涉及 Skill 开发

### 1.2 执行目标

1. 扫描 `~/Project/` 目录，找到最近 24 小时内修改的 SKILL.md
2. 读取 `~/Project/SKILL_META_MODEL.md`，加载现有 10 个设计模式
3. 使用分析检查清单识别新模式
4. 自动去重，避免重复添加
5. 更新 `SKILL_META_MODEL.md` 和 `SKILLS_INDEX.md`
6. 输出更新摘要

---

## 2. 工作流逻辑

### Step 1: 扫描最近修改的 Skill

**执行动作**：
```bash
# 查找最近 24 小时内修改的 SKILL.md
find ~/Project -name "SKILL.md" -mtime -1 -type f 2>/dev/null

# 如果用户提供了具体路径，直接使用该路径
```

**输出**：
- 如果找到：显示文件路径和修改时间
- 如果未找到：提示"未发现最近修改的 Skill，退出"

---

### Step 2: 读取现有元模型

**执行动作**：
```bash
# 读取元模型文档
cat ~/Project/SKILL_META_MODEL.md
```

**提取信息**：
- ✅ 现有的 10 个设计模式列表
- ✅ 每个模式的名称、来源 Skill、适用场景
- ✅ 元模型的更新日期和版本号

---

### Step 3: 深度分析新 Skill（使用分析检查清单）

**分析框架** - 六大维度检查清单：

#### 3.1 工作流模式维度
```yaml
检查项:
  - [ ] 是否有独特的步骤组织方式？
        示例: 阶段化工作流(PPT Generator)、双报告架构(运营商解析)

  - [ ] 是否有新的串联/并联/条件分支模式？
        示例: Phase 1→2→3→4 的阶段化执行

  - [ ] 是否有创新的交互流程？
        示例: 用户选择 → AI 规划 → 生成 → 合成

判断标准:
  ✅ 与现有"阶段化工作流"(模式5)、"双报告架构"(模式6)不同
  ✅ 具有可复用性（适用于3+场景）
  ❌ 仅是现有模式的微小变体
```

#### 3.2 算法模型维度
```yaml
检查项:
  - [ ] 是否有创新的数据处理算法？
        示例: The Matchmaker 匹配算法、多层估算模型

  - [ ] 是否有新的评分/排序/分类逻辑？
        示例: 加权评分系统(模式8)

  - [ ] 是否有降级/补偿/容错策略？
        示例: 4层 IEPL 估算(模式7)

判断标准:
  ✅ 算法具有通用性（不仅限于当前业务）
  ✅ 有清晰的伪代码或实现逻辑
  ❌ 仅是简单的 if-else 判断
```

#### 3.3 输出格式维度
```yaml
检查项:
  - [ ] 是否有新的文件格式组合？
        示例: MD + HTML + JSON + PDF

  - [ ] 是否有创新的视觉设计风格？
        示例: 双视觉风格（深色科技风 + 商务蓝色风）

  - [ ] 是否有特殊的报告结构？
        示例: 径向思维导图、交互式播放器

判断标准:
  ✅ 超越"双格式输出标配"(模式3)的创新
  ✅ 视觉设计有明确的场景价值
  ❌ 仅是换了配色或字体
```

#### 3.4 错误处理维度
```yaml
检查项:
  - [ ] 是否有创新的降级策略？
        示例: 正则 → AI Fallback → 人工兜底(模式2)

  - [ ] 是否有独特的错误恢复机制？
        示例: 并行数据采集 + 独立超时处理

  - [ ] 是否有数据质量追踪？
        示例: 每个维度标注来源和置信度

判断标准:
  ✅ 错误处理有明确的降级层级
  ✅ 不中断整体流程（符合静默执行协议）
  ❌ 仅是简单的 try-catch
```

#### 3.5 外部集成维度
```yaml
检查项:
  - [ ] 是否有创新的 API 集成方式？
        示例: API 链式调用、并行调用

  - [ ] 是否有浏览器自动化创新？
        示例: Playwright 持久化登录、状态保持

  - [ ] 是否有数据同步机制？
        示例: 飞书表格同步、邮件追踪

判断标准:
  ✅ 解决了常见的集成痛点
  ✅ 可迁移到其他 API/服务
  ❌ 仅是调用单个 API
```

#### 3.6 内容分析维度 ⭐
```yaml
检查项:
  - [ ] 是否有创新的内容理解方法？
        示例: 基于事实的场景重构(模式10)

  - [ ] 是否超越了简单的文本提取？
        示例: 还原对话场景、关系动态、情感氛围

  - [ ] 是否有防止 AI 幻觉的机制？
        示例: 可追溯性测试、事实依据标注

判断标准:
  ✅ 从"提取"升华为"理解"和"重构"
  ✅ 有明确的边界防止过度推理
  ❌ 仅是逐字逐句提取
```

---

### Step 4: 自动去重（与现有 10 个模式对比）

**对比清单**：

| 现有模式 | 核心特征 | 对比问题 |
|---------|---------|---------|
| **模式 1: 静默执行协议** | 不中断、一次性输出、错误静默处理 | 新 Skill 的流程控制是否与此完全相同？ |
| **模式 2: AI Fallback 降级** | 正则 → AI → 人工的三层降级 | 新 Skill 的降级策略是否有本质区别？ |
| **模式 3: 双格式输出标配** | MD + HTML/PDF 成对出现 | 新 Skill 是否有超越双格式的创新？ |
| **模式 4: 脚本分离架构** | SKILL.md (智能) + scripts/*.py (机械) | 新 Skill 的架构分层是否不同？ |
| **模式 5: 阶段化工作流** | Phase 1 → 2 → 3 → 4 的串联执行 | 新 Skill 的阶段划分是否有独特性？ |
| **模式 6: 双报告架构** | 同一数据 → 不同受众 → 不同报告 | 新 Skill 是否生成多视角报告？ |
| **模式 7: 多层估算模型** | 直接提取 → 推算 → 对标 → AI 推理 | 新 Skill 的数据补全策略是否类似？ |
| **模式 8: 加权评分系统** | 多维度加权 → 量化评分 → 评级映射 | 新 Skill 的评分逻辑是否一致？ |
| **模式 9: 模板驱动报告** | 详细模板 → AI 填充 → 结构一致 | 新 Skill 是否使用结构化模板？ |
| **模式 10: 场景重构** | 深度理解 → 基于事实重构 → 还原场景 | 新 Skill 的内容分析是否达到此深度？ |

**去重规则**：

```python
def is_duplicate_pattern(new_pattern, existing_patterns):
    """
    判断新模式是否与现有模式重复

    返回:
        - "duplicate": 完全重复，不添加
        - "variant": 现有模式的变体，不添加
        - "novel": 全新模式，可添加
        - "enhancement": 增强现有模式，合并到原模式
    """

    # 规则 1: 核心特征完全相同 → duplicate
    if new_pattern.core_features == existing.core_features:
        return "duplicate"

    # 规则 2: 仅应用场景不同，核心逻辑相同 → variant
    if new_pattern.logic == existing.logic:
        return "variant"

    # 规则 3: 在现有模式基础上增强 → enhancement
    if new_pattern.is_enhancement_of(existing):
        return "enhancement"

    # 规则 4: 完全独立的新模式 → novel
    return "novel"
```

**通用性测试**（新模式必须通过）：

```yaml
测试 1: 适用场景数量
  ✅ 通过: 可用于 3+ 个不同场景
  ❌ 失败: 仅限于当前 Skill 的特定场景

测试 2: 实现清晰度
  ✅ 通过: 有清晰的伪代码或实现逻辑
  ❌ 失败: 概念模糊，无法指导实践

测试 3: 独立性
  ✅ 通过: 与现有 10 个模式有本质区别
  ❌ 失败: 是现有模式的简单变体

测试 4: 可追溯性
  ✅ 通过: 能清晰追溯到源 Skill 的具体实现
  ❌ 失败: 无法找到对应的代码或逻辑
```

---

### Step 5: 更新元模型文档

**如果发现新模式**，按以下格式添加到 `SKILL_META_MODEL.md`：

```markdown
### 模式 N: [模式名称] 🆕

**应用于**: [首次出现的 Skill 名称]

**核心思想**: [一句话描述核心理念]

**设计哲学**:
- **[关键点 1]**
- **[关键点 2]**
- **[关键点 3]**

**实现框架**:
\`\`\`
[架构图或流程图]
\`\`\`

**对比示例**:

❌ **传统做法（机械）**:
\`\`\`
[反面示例]
\`\`\`

✅ **创新做法（智能）**:
\`\`\`
[正面示例]
\`\`\`

**适用场景**（广泛）:
- 📝 场景 1
- 💬 场景 2
- 📞 场景 3

**实现代码**:
\`\`\`python
[可复用的代码片段]
\`\`\`

**与其他模式的关系**:
- 融合了"[模式 X]"的 [特性]
- 超越了"[模式 Y]"，升华为 [更高层次]

**为什么重要**:
1. ✅ [重要性 1]
2. ✅ [重要性 2]
3. ✅ [重要性 3]
```

**更新元数据**：
```markdown
> 📅 最后更新: 2026-02-02 (新增：[模式名称])
```

---

### Step 6: 同步更新 SKILLS_INDEX.md

**更新内容**：

1. **如果是新 Skill**，添加到"自定义 Skills"章节：

```markdown
### N. 🎯 [Skill 中文名称] 🆕

| 属性 | 值 |
|------|-----|
| **路径** | `[skill-path]` |
| **Skill 名称** | `[skill-name]` |
| **状态** | ✅ 完整可用 |

**功能特性：**
- 🌐 [特性 1]
- 📊 [特性 2]
- 🤖 [特性 3]

**触发方式：**
\`\`\`bash
/[command]
# 或自然语言: "[触发短语1]" / "[触发短语2]"
\`\`\`
```

2. **更新总览统计**：
```markdown
| 分类 | 数量 | 来源 |
|------|------|------|
| **自定义 Skills（有 SKILL.md）** | [N+1] | Project 目录 |
```

3. **更新"你的 Skill 资产清单"**（如果有新的可复用组件）：

```markdown
| **[新模式名称]** 🆕 | [源 Skill] | [可复用场景] |
```

---

### Step 7: 输出更新摘要

**执行完成后，输出结构化摘要**：

```markdown
✅ 元模型更新完成

📊 本次更新:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🔍 分析 Skill:
  - 名称: [skill-name]
  - 路径: [skill-path]
  - 修改时间: [timestamp]

📈 模式分析结果:
  ✅ 新增模式: [模式 N: 名称]
  或
  ⚠️ 未发现新模式（与现有模式重复）

💾 更新文件:
  - SKILL_META_MODEL.md (新增 [X] 行，共 [Y] 行)
  - SKILLS_INDEX.md (新增 Skill 条目)

🎯 新模式摘要 (如果有):
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
模式 N: [模式名称]

核心思想:
  [一句话描述]

适用场景:
  1. [场景 1]
  2. [场景 2]
  3. [场景 3]

核心代码:
  [关键实现片段]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 下一步建议:
  - [建议 1]
  - [建议 2]
  - [建议 3]

📅 更新时间: [YYYY-MM-DD HH:MM:SS]
```

---

## 3. 核心算法

### 3.1 模式相似度计算

```python
def calculate_pattern_similarity(new_pattern, existing_pattern):
    """
    计算新模式与现有模式的相似度

    返回: 0.0 - 1.0 (0 = 完全不同, 1 = 完全相同)
    """
    similarity_score = 0.0

    # 核心特征相似度 (权重 40%)
    core_features_match = compare_features(
        new_pattern.core_features,
        existing_pattern.core_features
    )
    similarity_score += core_features_match * 0.4

    # 应用场景相似度 (权重 30%)
    scenario_overlap = len(
        set(new_pattern.scenarios) & set(existing_pattern.scenarios)
    ) / len(set(new_pattern.scenarios) | set(existing_pattern.scenarios))
    similarity_score += scenario_overlap * 0.3

    # 实现逻辑相似度 (权重 30%)
    logic_match = compare_logic(
        new_pattern.implementation,
        existing_pattern.implementation
    )
    similarity_score += logic_match * 0.3

    return similarity_score

def is_duplicate(similarity_score):
    """
    基于相似度判断是否重复
    """
    if similarity_score >= 0.85:
        return "duplicate"  # 高度相似，视为重复
    elif similarity_score >= 0.65:
        return "variant"    # 中度相似，视为变体
    elif similarity_score >= 0.45:
        return "enhancement"  # 低度相似，可能是增强
    else:
        return "novel"      # 完全不同，全新模式
```

### 3.2 通用性评分模型

```python
def assess_generalizability(pattern):
    """
    评估模式的通用性（0-100分）
    """
    score = 0

    # 1. 适用场景数量 (40分)
    scenario_count = len(pattern.scenarios)
    if scenario_count >= 5:
        score += 40
    elif scenario_count >= 3:
        score += 30
    elif scenario_count >= 2:
        score += 15
    else:
        score += 5  # 仅1个场景，通用性差

    # 2. 实现清晰度 (30分)
    if pattern.has_pseudocode or pattern.has_code_snippet:
        score += 30
    elif pattern.has_clear_description:
        score += 15

    # 3. 跨领域适用性 (20分)
    domains = set([s.domain for s in pattern.scenarios])
    if len(domains) >= 3:
        score += 20
    elif len(domains) >= 2:
        score += 10

    # 4. 可追溯性 (10分)
    if pattern.source_skill and pattern.source_code:
        score += 10

    return score

def is_generalizable(score):
    """
    判断是否值得加入元模型
    """
    return score >= 60  # 60分以上才值得添加
```

---

## 4. Few-Shot 示例

### ✅ Good Case 1: 发现全新模式

**Input**:
```bash
/update-meta-model ~/Project/组织文化分析（会议纪要拆解）/
```

**Action**:
1. 读取该 Skill 的 SKILL.md
2. 分析发现: "基于事实的场景重构"方法
3. 与现有 10 个模式对比 → 相似度 < 0.4 → 判定为 novel
4. 通用性评分: 85 分（适用于所有对话类内容）→ 值得添加
5. 添加为"模式 10"
6. 更新 SKILL_META_MODEL.md 和 SKILLS_INDEX.md

**Output**:
```
✅ 元模型更新完成

📊 本次更新:
  - 新增模式: 模式 10: 基于事实的场景重构
  - 适用场景: 会议记录、聊天记录、客服对话等
  - 通用性评分: 85/100 (优秀)
  - 更新文件: SKILL_META_MODEL.md (+120行)
```

---

### ✅ Good Case 2: 识别为现有模式的变体

**Input**:
```bash
/update-meta-model ~/Project/新邮件分析/
```

**Action**:
1. 读取 SKILL.md
2. 分析发现: 也是"静默执行 + 双格式输出"
3. 与模式 1、模式 3 对比 → 相似度 > 0.85 → 判定为 duplicate
4. 不添加新模式，仅在 SKILLS_INDEX.md 中添加 Skill 条目

**Output**:
```
✅ 元模型更新完成

📊 本次更新:
  ⚠️ 未发现新模式
  - 原因: 与"模式 1: 静默执行协议"和"模式 3: 双格式输出"重复
  - 建议: 直接复用现有模式即可
  - 更新文件: SKILLS_INDEX.md (新增 Skill 条目)
```

---

### ✅ Good Case 3: 增强现有模式

**Input**:
```bash
/update-meta-model ~/Project/超级邮件汇总/
```

**Action**:
1. 分析发现: 在"AI Fallback"基础上增加了第四层（数据库查询）
2. 相似度计算 → 0.68 → 判定为 enhancement
3. 更新"模式 2: AI Fallback 降级机制"，添加4层版本

**Output**:
```
✅ 元模型更新完成

📊 本次更新:
  ✅ 增强现有模式: 模式 2 (AI Fallback)
  - 新增: 第四层降级策略 (数据库查询)
  - 应用: 超级邮件汇总 Skill
  - 更新文件: SKILL_META_MODEL.md (更新模式2章节)
```

---

### ❌ Anti-Pattern 1: 过度推理

**Bad Behavior**:
```
分析发现: 这个 Skill 使用了"创新的错误处理机制"
（实际上只是简单的 try-catch）
```

**Why Wrong**:
不符合通用性测试，仅是基础编程实践，不是可复用的设计模式

**Correct Behavior**:
```
分析结果: 未发现新模式
- 错误处理: 标准 try-catch，无独特降级策略
- 建议: 参考"模式 2: AI Fallback"增强错误处理
```

---

### ❌ Anti-Pattern 2: 重复添加

**Bad Behavior**:
```
发现新模式: "Markdown + HTML 双输出"
（与模式 3 完全相同）
```

**Why Wrong**:
未执行去重检查，导致模式重复

**Correct Behavior**:
```
分析结果: 与"模式 3: 双格式输出标配"重复
- 相似度: 0.95 (高度相似)
- 判定: duplicate
- 操作: 不添加新模式
```

---

## 5. 输出规范

### 5.1 文件命名

本 Skill 不生成新文件，而是直接修改：
- `~/Project/SKILL_META_MODEL.md`
- `~/Project/SKILLS_INDEX.md`

### 5.2 Git 操作（可选）

如果在 Git 仓库中，建议执行：
```bash
cd ~/Project
git add SKILL_META_MODEL.md SKILLS_INDEX.md
git commit -m "更新元模型: 新增模式 N - [模式名称]

- 来源 Skill: [skill-name]
- 适用场景: [场景列表]
- 更新内容: [简要说明]

🤖 由 meta-model-updater Skill 自动执行"
```

### 5.3 最终输出

执行完成后，仅输出：
```
✅ 元模型自动更新执行完成

📊 更新摘要已展示在上方
📁 更新文件:
  - SKILL_META_MODEL.md
  - SKILLS_INDEX.md

💡 建议: 使用 git diff 查看详细变更
```

---

## 6. 验证矩阵

| 测试场景 | 输入 | 预期行为 | 通过标准 |
|---------|------|---------|---------|
| **全新模式** | 组织文化分析 Skill | 识别"场景重构"模式 → 添加为模式 10 | ✅ 元模型新增章节 |
| **重复模式** | 简单邮件分析 Skill | 识别与模式 1/3 重复 → 不添加 | ✅ 输出"未发现新模式" |
| **增强模式** | 4层 Fallback Skill | 识别为模式 2 增强 → 合并到原模式 | ✅ 模式 2 章节更新 |
| **无新 Skill** | 24 小时内无修改 | 扫描结果为空 → 提示退出 | ✅ 优雅退出 |
| **指定路径** | `/update-meta-model [path]` | 直接分析指定 Skill | ✅ 跳过扫描步骤 |

---

## 7. 高级功能

### 7.1 批量分析模式

```bash
/update-meta-model --batch
# 分析最近 7 天内修改的所有 Skill
```

### 7.2 对比报告模式

```bash
/update-meta-model --report
# 生成详细的模式对比报告（不修改元模型）
```

### 7.3 回滚功能

```bash
/update-meta-model --rollback
# 撤销最近一次更新（基于 Git 历史）
```

---

## 8. 依赖说明

### 8.1 必需文件

| 文件 | 路径 | 说明 |
|------|------|------|
| SKILL_META_MODEL.md | `~/Project/` | 元模型主文档 |
| SKILLS_INDEX.md | `~/Project/` | Skill 索引 |
| AGENTS.md | `~/Project/` | 跨工具协作规则 |

### 8.2 可选工具

- **Git**: 用于提交更新记录
- **diff**: 用于显示文件变更

---

## 9. 最佳实践

### 9.1 何时使用此 Skill

✅ **推荐场景**:
- 每次开发新 Skill 后
- 修改现有 Skill 的核心逻辑后
- 每周回顾时，批量分析近期修改

❌ **不推荐场景**:
- 仅修改 Skill 的文档说明
- 仅调整输出格式（无逻辑变化）
- 修改辅助脚本（不涉及 SKILL.md）

### 9.2 质量保证

每次更新后，手动检查：
- [ ] 新模式的"适用场景"是否真的通用？
- [ ] 代码示例是否可以直接复用？
- [ ] 与其他模式的区别是否清晰？
- [ ] 元模型的总体结构是否保持一致？

---

## 10. 故障排查

### 问题 1: 找不到最近修改的 Skill

**症状**: 输出"未发现最近修改的 Skill"

**原因**:
- 文件修改时间超过 24 小时
- SKILL.md 文件名大小写不匹配

**解决**:
```bash
# 手动指定路径
/update-meta-model ~/Project/[skill-path]/
```

---

### 问题 2: 模式相似度判断不准确

**症状**: 明显不同的模式被判定为 duplicate

**原因**: 相似度阈值设置过低

**解决**:
调整 `is_duplicate()` 函数的阈值
- 当前: 0.85 → 调整为 0.90

---

### 问题 3: 更新后元模型格式混乱

**症状**: Markdown 格式不一致

**原因**: 自动添加的章节格式有误

**解决**:
1. 检查模板是否正确
2. 使用 Markdown 格式化工具修复
3. 必要时手动调整格式

---

## 11. 开发路线图

### v1.0 (当前版本)
- ✅ 基础模式识别
- ✅ 自动去重
- ✅ 更新元模型和索引

### v1.1 (计划中)
- 🔄 支持批量分析
- 🔄 生成可视化对比报告
- 🔄 自动 Git 提交

### v2.0 (未来)
- 💭 AI 驱动的模式命名
- 💭 模式相似度可视化
- 💭 跨项目模式复用建议

---

*本 Skill 是 AGENTS.md 规则 1 的自动化实现*
*致力于让元模型保持最新，让设计模式真正可复用* 🚀
