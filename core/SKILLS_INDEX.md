# 🎯 Skills 统一索引文档

> 📅 生成日期: 2026-01-30
> 📅 最后更新: 2026-02-02 (重新整理：统一为 Skills 体系)
> 🤖 由元模型更新器自动维护
> 📁 索引范围: `/Users/wyw/Project` + `~/.gemini/antigravity/skills`

---

## 📊 总览

| 分类 | 数量 | 来源 |
|------|------|------|
| **自定义 Skills** | 12 | Project 目录 |
| **AntiGravity 内置 Skills** | 16 | ~/.gemini/antigravity |
| **总计** | 28 | — |

---

## 🔥 自定义 Skills

> 以下是你在 Project 目录下开发的所有 Skills，统一按功能分类整理。

---

### 📊 元模型与基础设施

#### 0. 📊 元模型自动更新器 ⭐⭐

| 属性 | 值 |
|------|-----|
| **路径** | `/Users/wyw/Project/skill 元模型/meta-model-updater/` |
| **Skill 名称** | `meta-model-updater` |
| **有 SKILL.md** | ✅ 有（1500+ 行） |
| **状态** | ✅ 完整可用 |
| **重要性** | ⭐⭐ 核心基础设施 |

**功能特性：**
- 🧠 **元认知能力** — 分析和理解其他 Skill 的设计模式
- 🔍 **6维度分析框架** — 工作流、算法、输出、错误处理、外部集成、内容分析
- 🎯 **智能去重逻辑** — 相似度计算（核心特征40% + 场景重叠30% + 实现逻辑30%）
- 🔄 **自动化更新** — 自动更新 SKILL_META_MODEL.md 和 SKILLS_INDEX.md

**触发方式：**
```bash
"更新元模型" / "update meta model" / /update-meta-model
```

---

### � 运营商与商务分析

#### 1. 🌍 海外运营商多维解析

| 属性 | 值 |
|------|-----|
| **路径** | `/Users/wyw/Project/海外运营商多维解析skill/` |
| **Skill 名称** | `carrier-analyzer` |
| **有 SKILL.md** | ✅ 有 |
| **状态** | ✅ 完整可用 |

**功能特性：**
- 🌐 **10维度综合分析** — 本地线路、海缆、IEPL、收购历史、合作风险等
- 📊 **批发业务专项报告** — 海缆资源、PoP覆盖、资源稀缺性、采购策略
- 🤖 **IEPL 4层估算模型** — 直接提取→批发推算→行业对标→AI推理
- ⚖️ **5维度加权评分** — 海缆35%+IEPL30%+批发20%+技术10%+财务5%
- 🎨 **双视觉风格** — 深色科技风（综合）+ 商务蓝色（批发）
- 📁 **5文件输出** — 双报告×双格式 + 原始JSON

**触发方式：**
```bash
/carrier-analyzer Deutsche Telekom
# 或自然语言: "分析德国电信" / "评估Orange的批发业务"
```

---

#### 2. 🏛️ 组织文化分析师 🆕

| 属性 | 值 |
|------|-----|
| **路径** | `/Users/wyw/Project/组织文化分析（会议纪要拆解）/` |
| **Skill 名称** | `org-culture-analyst` |
| **有 SKILL.md** | ✅ 有（.skill 格式） |
| **状态** | ✅ 完整可用 |

**功能特性：**
- 🔬 **四维文化光谱分析** — 认知、关系、沟通、行为四大维度
- 📊 **多维度定位** — 每个维度 2-3 个光谱，精准定位组织特征
- 💬 **证据驱动** — 所有结论搭配原文引用
- 🎭 **中立客观** — 不做价值判断，只还原"生态"
- ✨ **纯 Prompt** — 无需脚本，完全依靠精心设计的提示词

**触发方式：**
```bash
"分析这个会议" / "看看组织文化" / "团队诊断"
```

**创新模式：**
- ✨ 引入了**"模式 10: 基于事实的场景重构"**设计模式
- ✨ 展示了"纯 Prompt Engineering"的最佳实践

---

### 📧 邮件处理

#### 3. 📧 每日线路资源日报

| 属性 | 值 |
|------|-----|
| **路径** | `/Users/wyw/Project/邮件汇总skill/` |
| **Skill 名称** | `daily-circuit-resource-report` |
| **有 SKILL.md** | ✅ 有 |
| **状态** | ✅ 完整可用 |

**功能特性：**
- 📬 IMAP 邮件获取 — 自动获取过去 24 小时邮件
- 🔍 智能提取 — 线路信息、容量、供应商、价格
- 🔄 询价-报价匹配 — 自动关联询价与报价
- 📊 双格式报告 — Markdown + HTML（支持暗黑模式）
- 🤫 静默执行 — 无需确认，全程自动化

**输出文件：**
- `daily_report_{YYYY-MM-DD}.md`
- `daily_report_{YYYY-MM-DD}.html`

---

#### 4. 📊 邮件汇总表格（飞书同步）

| 属性 | 值 |
|------|-----|
| **路径** | `/Users/wyw/Project/邮件汇总表格/` |
| **Skill 名称** | `email-feishu-sync` |
| **有 SKILL.md** | ✅ 有 |
| **状态** | ✅ 完整可用 |
| **文档** | `使用指南.md` |

**功能特性：**
- 📧 邮件智能解析 — 自动提取线路、带宽、供应商、价格
- 🤖 AI 智能总结 — Claude Haiku 生成一句话摘要
- 📋 飞书表格同步 — 自动更新到飞书多维表格
- 🔄 AI Fallback — 正则失败时自动调用 AI 提取

**触发方式：**
```bash
/email-summarize
# 或: "汇总邮件到飞书"
```

---

#### 5. 📧 每日邮件分析

| 属性 | 值 |
|------|-----|
| **路径** | `/Users/wyw/Project/每日邮件分析/` |
| **Skill 名称** | `daily-email-analysis` |
| **有 SKILL.md** | ✅ 有 |
| **状态** | ✅ 可用 |

**功能特性：**
- 📬 邮件获取 — IMAP 自动获取邮件
- 📊 分析报告 — 生成 HTML + MD 格式报告
- 🏢 商务邮件 — 针对线路资源询价/报价

---

### 🎨 内容创作

#### 6. 📊 PPT Generator Pro

| 属性 | 值 |
|------|-----|
| **路径** | `/Users/wyw/Project/PPT Generator Skill/` |
| **Skill 名称** | `ppt-generator-pro` |
| **有 SKILL.md** | ✅ 有 |
| **版本** | 2.0.0 |
| **状态** | ✅ 完整可用 |

**功能特性：**
- 🤖 智能文档分析 — 自动提取核心要点，规划 PPT 内容结构
- 🎨 多风格支持 — 渐变毛玻璃、矢量插画两种专业风格
- 🖼️ 高质量图片 — Nano Banana Pro 生成 16:9 高清 PPT（2K/4K）
- 🎬 AI 转场视频 — 可灵 AI 生成流畅的页面过渡动画
- 🎮 交互式播放器 — 视频+图片混合播放，支持键盘导航
- 🎥 完整视频导出 — FFmpeg 合成包含所有转场的完整视频

**依赖：**
- `GEMINI_API_KEY` — Google AI API（必需）
- `KLING_ACCESS_KEY` / `KLING_SECRET_KEY` — 可灵 AI（视频功能）

**触发方式：**
```bash
/ppt-generator-pro
# 或自然语言: "帮我生成一个 PPT"
```

---

#### 7. 🎙️ 专属播客（MD → 小宇宙）

| 属性 | 值 |
|------|-----|
| **路径** | `/Users/wyw/Project/专属播客/` |
| **Skill 名称** | `md-to-podcast` |
| **有 SKILL.md** | ✅ 有 |
| **状态** | ✅ 完整可用 |

**功能特性：**
- 📝 解析 MD 文件 — 提取备选标题和正文内容
- 🎵 生成音频 — 使用 ListenHub API 将文本转为语音
- 📤 自动上传 — Playwright 自动上传到小宇宙平台
- 🎤 自定义音色 — 支持克隆音色（王永威声音）

**MD 文件格式：**
```markdown
## 备选标题
这里是播客节目的标题

## 正文
这里是正文内容，将被转换为音频...
```

**使用方式：**
```bash
python md_to_podcast.py episode.md "王永威声音"
```

---

#### 8. � 论文解读 Skills

| 属性 | 值 |
|------|-----|
| **路径** | `/Users/wyw/Project/论文解读 Skills/` |
| **Skill 名称** | `paper-interpreter` |
| **有 SKILL.md** | ✅ 有 |
| **状态** | ✅ 可用 |

**功能特性：**
- � PDF 深度解读 — 自动分析论文/书籍内容
-  生成报告 — HTML + PDF 格式
- 🎨 精美排版 — 专业级报告样式

**已生成报告：**
- 10x is easier than 2x 深度解读
- 超越百岁 深度解读
- 心理类型 深度解读
- 马斯克闭门预警 深度解读

---

#### 9. � 小红书内容生成

| 属性 | 值 |
|------|-----|
| **路径** | `/Users/wyw/Project/小红书内容生成/` |
| **Skill 名称** | `xiaohongshu-generator` |
| **有 SKILL.md** | ✅ 有 |
| **状态** | 🔧 开发中 |

**功能特性：**
- � 内容转换 — 将文档转为小红书图文
- 🖼️ 图片生成 — 生成小红书风格配图

---

### 🌐 社交媒体与数据采集

#### 10. 🔥 海外营销爆款选品

| 属性 | 值 |
|------|-----|
| **路径** | `/Users/wyw/Project/海外营销爆款选品/` |
| **Skill 名称** | `hot-picks-scraper` |
| **有 SKILL.md** | ✅ 有 |
| **状态** | ✅ 完整可用（GitHub Actions 自动化） |
| **在线预览** | [hot-picks](https://xiaocaioh14-arch.github.io/hot-picks/reports/latest.html) |

**功能特性：**
- 🌍 多市场覆盖 — 美国、英国、德国
- 📈 双榜数据 — Movers & Shakers + Best Sellers
- 🎯 营销建议 — 每个商品附带定制营销策略
- ⏰ 每日自动更新 — UTC 0:00（北京 08:00）

---

#### 11. 📰 微信公众号文章读取

| 属性 | 值 |
|------|-----|
| **路径** | `/Users/wyw/Project/微信公众号文章读取/` |
| **Skill 名称** | `wechat-article-exporter` |
| **有 SKILL.md** | ✅ 有 |
| **状态** | ✅ 完整可用 |
| **在线站点** | [down.mptext.top](https://down.mptext.top) |
| **文档站** | [docs.mptext.top](https://docs.mptext.top) |

**功能特性：**
- 🔍 搜索公众号 — 支持关键字搜索
- 📥 批量导出 — html/json/excel/txt/md/docx
- 💾 缓存列表 — 减少接口请求
- 🎨 100% 还原 — HTML 格式完整保留样式
- 📊 导出数据 — 阅读量、评论、转发量

**支持部署：**
- Docker 私有化部署
- Cloudflare Workers 部署

---

#### 12. 🔥 微博热搜分析

| 属性 | 值 |
|------|-----|
| **路径** | `/Users/wyw/Project/微博热搜分析/` |
| **Skill 名称** | `weibo-hot-analyzer` |
| **有 SKILL.md** | ✅ 有 |
| **状态** | ✅ 可用 |

**功能特性：**
- 📊 热搜监控 — 定时抓取微博热搜榜
- 📝 分析报告 — 生成热搜分析 Markdown 报告
- ⏰ 自动执行 — GitHub Actions 定时任务

---

## � SKILL.md 状态统计

| 状态 | 数量 | Skills |
|------|------|--------|
| ✅ **已有 SKILL.md** | 12 | 全部 Skills 已完成 SKILL.md 文档 |
| ❌ **待创建 SKILL.md** | 0 | — |

---

## 🏢 AntiGravity 内置 Skills（16个）

| # | 英文名称 | 中文名称 | 功能说明 |
|---|---------|---------|---------|
| 1 | algorithmic-art | 算法艺术生成器 | p5.js 生成式艺术，流场、粒子系统 |
| 2 | brand-guidelines | 品牌设计规范 | Anthropic 官方品牌配色和字体 |
| 3 | canvas-design | 画布设计工具 | 创建 PNG/PDF 精美艺术作品 |
| 4 | doc-coauthoring | 文档协作助手 | 结构化文档协作流程 |
| 5 | docx | Word 文档处理 | 修订追踪、批注、格式保留 |
| 6 | frontend-design | 前端界面设计 | 生产级前端界面，避免 AI 通用样式 |
| 7 | internal-comms | 内部沟通模板 | 3P 更新、公司简报、FAQ |
| 8 | mcp-builder | MCP 服务器构建器 | 创建 LLM 与外部服务交互的 MCP |
| 9 | pdf | PDF 处理工具箱 | 提取、创建、合并、拆分、表单 |
| 10 | pptx | PPT 演示文稿处理 | 创建、编辑、分析演示文稿 |
| 11 | skill-creator | 技能创建指南 | 创建扩展 Claude 能力的新技能 |
| 12 | slack-gif-creator | Slack GIF 制作器 | 针对 Slack 优化的动画 GIF |
| 13 | theme-factory | 主题工厂 | 10 种预设主题 + 自定义主题 |
| 14 | web-artifacts-builder | Web 工件构建器 | React + Tailwind + shadcn/ui |
| 15 | webapp-testing | Web 应用测试工具 | Playwright 自动化测试 |
| 16 | xlsx | Excel 电子表格处理 | 公式、格式化、数据分析 |

---

## 📂 上下文路径索引

### 跨工具上下文访问

| 工具 | 路径 | 说明 |
|------|------|------|
| **Claude Code** | `~/.claude/` | 项目配置、会话历史、todos |
| **AntiGravity** | `~/.gemini/antigravity/` | skills、brain(会话)、conversations |
| **Project** | `/Users/wyw/Project/` | 自定义 skills 和工具项目 |

### AntiGravity 上下文结构

```
~/.gemini/antigravity/
├── skills/
│   └── skills/          # 内置 16 个 Skills
├── brain/               # 会话上下文
│   └── {UUID}/
│       ├── task.md
│       ├── implementation_plan.md
│       └── walkthrough.md
├── conversations/       # 对话历史
└── GEMINI.md           # 全局配置
```

### Claude Code 上下文结构

```
~/.claude/
├── projects/           # 项目配置
├── todos/              # 任务列表
├── session-env/        # 会话环境
├── debug/              # 调试日志
└── settings.json       # 全局设置
```

---

## 🔗 快速访问

### 在线服务

| 服务 | URL |
|------|-----|
| 海外爆款选品 | https://xiaocaioh14-arch.github.io/hot-picks/reports/latest.html |
| 微信公众号导出 | https://down.mptext.top |
| 微信公众号文档 | https://docs.mptext.top |
| 飞书邮件表格 | https://my.feishu.cn/base/UIifbHEl9a2VohsqAIzc5ZX1nIb |

### 本地运行

```bash
# PPT Generator
cd "/Users/wyw/Project/PPT Generator Skill"
python generate_ppt.py --plan slides_plan.json --style styles/gradient-glass.md

# 专属播客
cd /Users/wyw/Project/专属播客
python md_to_podcast.py episode.md

# 邮件汇总
cd /Users/wyw/Project/邮件汇总skill
python3 scripts/fetch_emails.py --days 1

# 飞书同步
cd /Users/wyw/Project/邮件汇总表格
python3 scripts/feishu_bitable.py
```

---

## 📝 维护说明

- **更新索引**：让 Cowork 重新扫描 Project 目录
- **添加新 Skill**：在 Project 目录创建新文件夹，添加 SKILL.md
- **跨工具协作**：Cowork 可读取所有上下文，生成统一视图
- **创建 SKILL.md**：对于标记为"待创建"的 Skill，可使用 `/skill-creator` 生成

---

*本文档由 Claude Cowork 自动生成，支持实时更新*
