# Visio Flowchart Skill · Visio 流程图技能

> Claude Code Skill — 用自然语言生成规范的 Microsoft Visio 流程图  
> Claude Code Skill — Generate professional Microsoft Visio flowcharts from natural language

[中文](#chinese) | [English](#english)

---

<span id="chinese"></span>

## 中文

### 这是什么

一个 Claude Code 的自定义 Skill，让你用自然语言（如"帮我画个用户登录流程"）自动生成符合规范的 Microsoft Visio 流程图（`.vsdx` 文件）。支持基本流程图（ISO 5807）和泳道图。

底层基于 [visio-mcp](https://pypi.org/project/visio-mcp/) MCP Server，通过 Visio COM 自动化接口操控 Visio。

### 功能特性

| 特性 | 说明 |
|------|------|
| 自然语言输入 | 说"画个 XX 流程图"即可触发，无需手动拖拽 |
| 基本流程图 | 支持 ISO 5807 标准形状（圆角矩形/矩形/菱形/平行四边形/双边框矩形） |
| 泳道图 | 自动识别角色，分配节点到对应泳道 |
| 复杂度自适应 | ≤5 节点直接生成，>5 节点先展示清单确认 |
| 公司规范覆盖 | 通过 `standards.md` 配置文件自定义颜色、字体、形状等 |
| 内置模板 | 提供登录/CRUD/审批/订单/异常处理等常见流程模板 |
| 中文友好 | 全中文交互界面，支持中文节点文本 |

### 环境要求

- Windows 操作系统
- Microsoft Visio Desktop（已安装并激活）
- Python 3.14+
- [uv](https://docs.astral.sh/uv/)（Python 包管理器）
- Claude Code

### 安装

```bash
# 1. 将仓库克隆到你的项目目录
git clone <repo-url> .

# 2. 安装 visio-mcp
pip install visio-mcp

# 3. 重启 Claude Code，Skill 自动生效
```

### 使用

```
# 基本流程图
"帮我画个用户登录流程图"

# 泳道图
"画一个订单处理的泳道图，涉及用户、系统、仓库三个角色"

# 从模板生成
"画个审批流程图，需要两级审批"
```

Skill 会自动加载，解析你的需求，生成 `.vsdx` 文件。

### 公司规范定制

编辑 `.claude/skills/visio-flowchart/standards.md`，填入你公司的颜色、字体规范：

```markdown
| 节点类型 | 填充色 | 字体 | 字号 |
|---------|--------|------|------|
| 开始/结束 | #2196F3 | 微软雅黑 | 12pt |
| 处理 | #FFFFFF | 微软雅黑 | 11pt |
| 判断 | #FFF9C4 | 微软雅黑 | 11pt |
```

未填写的项将自动使用 ISO 5807 默认值。

### 项目结构

```
.
├── .claude/skills/visio-flowchart/
│   ├── SKILL.md              # Skill 核心指令
│   └── standards.md          # 公司规范配置
├── .mcp.json                 # visio-mcp MCP Server 配置
├── .stdd/
│   ├── specs/                # 7 个 Capability 规格文档
│   ├── changes/              # 变更记录
│   └── archive/              # 归档
└── README.md
```

### 开发说明

本项目使用 [STDD](https://github.com/anthropics/claude-code)（Spec+Test Driven Development）方法论开发：

- **Phase 1** 需求理解 → proposal.md
- **Phase 2** 规格设计 → 7 个 spec + test-plan（29 TC）
- **Phase 3** 切片规划 → 7 个垂直切片
- **Phase 4** TDD 实现 → SKILL.md + standards.md + .mcp.json
- **Phase 5** 质量验证 → 三路并行审查 + 11 类失败模式检查
- **Phase 6** 交付归档

完整开发记录见 `.stdd/archive/2026-05-15-visio-flowchart-skill/`。

---

<span id="english"></span>

## English

### What Is This

A Claude Code custom Skill that generates standards-compliant Microsoft Visio flowcharts (`.vsdx` files) from natural language input. Supports basic flowcharts (ISO 5807) and cross-functional flowcharts (swimlane diagrams).

Powered by [visio-mcp](https://pypi.org/project/visio-mcp/) MCP Server via Visio COM automation.

### Features

| Feature | Description |
|---------|-------------|
| Natural Language Input | Just say "draw me a login flowchart" — no manual drag-and-drop |
| Basic Flowcharts | ISO 5807 standard shapes (rounded rect / rect / diamond / parallelogram / double-border rect) |
| Swimlane Diagrams | Auto-detect roles and assign nodes to corresponding lanes |
| Adaptive Complexity | ≤5 nodes: direct generation. >5 nodes: show node list for confirmation first |
| Company Standards | Customize colors, fonts, and shapes via `standards.md` |
| Built-in Templates | Login, CRUD, approval, order processing, exception handling patterns |
| Chinese-Friendly | Full Chinese interface, supports Chinese node labels |

### Prerequisites

- Windows OS
- Microsoft Visio Desktop (installed and activated)
- Python 3.14+
- [uv](https://docs.astral.sh/uv/) (Python package manager)
- Claude Code

### Installation

```bash
# 1. Clone this repo into your project directory
git clone <repo-url> .

# 2. Install visio-mcp
pip install visio-mcp

# 3. Restart Claude Code — the Skill loads automatically
```

### Usage

```
# Basic flowchart
"Draw me a user registration flowchart"

# Swimlane diagram
"Create a swimlane diagram for order processing with User, System, and Warehouse roles"

# From template
"Generate an approval workflow with two levels of review"
```

The Skill auto-loads, parses your intent, and generates a `.vsdx` file.

### Company Standards Customization

Edit `.claude/skills/visio-flowchart/standards.md` with your company's color and font specs:

```markdown
| Node Type | Fill Color | Font | Size |
|-----------|-----------|------|------|
| Start/End | #2196F3 | Arial | 12pt |
| Process | #FFFFFF | Arial | 11pt |
| Decision | #FFF9C4 | Arial | 11pt |
```

Unfilled items fall back to ISO 5807 defaults.

### Project Structure

```
.
├── .claude/skills/visio-flowchart/
│   ├── SKILL.md              # Core Skill instructions
│   └── standards.md          # Company standards config
├── .mcp.json                 # visio-mcp MCP Server config
├── .stdd/
│   ├── specs/                # 7 Capability specification documents
│   ├── changes/              # Change records
│   └── archive/              # Archive
└── README.md
```

### Development

This project was built using the **STDD** (Spec+Test Driven Development) methodology:

| Phase | Output |
|-------|--------|
| 1. Understand | proposal.md — 7 Capabilities, 7 Success Criteria |
| 2. Spec | 7 specs, test-plan.md (16 Requirements, 29 Scenarios) |
| 3. Slice | 7 vertical slices, 38 implementation tasks |
| 4. Build | SKILL.md (271 lines) + standards.md + .mcp.json |
| 5. Verify | 29/29 TC passed, 3-way parallel review (0 Critical, 0 High) |
| 6. Deliver | Archived with full traceability |

Full development records: `.stdd/archive/2026-05-15-visio-flowchart-skill/`.
