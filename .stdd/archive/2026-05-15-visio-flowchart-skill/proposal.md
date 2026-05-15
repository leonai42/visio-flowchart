# Visio 流程图 Skill

## Why

用户需要频繁创建 Visio 流程图（基本流程图、泳道图），但手动拖拽绘制效率低、规范难统一。visio-mcp 提供了操控 Visio 的 API 能力，但缺少两类知识：① 流程图领域专业知识（ISO 5807 形状/布局规范）；② 公司内部文档规范的映射规则（颜色/字体/形状约定）。需要一个 Skill 填补这些缺口。

## What Changes

- 新建 `.claude/skills/visio-flowchart/SKILL.md` — 核心 Skill 文件
- 新建 `.claude/skills/visio-flowchart/standards.md` — 公司规范配置文件
- 新建 `.mcp.json` — 配置 visio-mcp MCP Server
- 初始化项目 `.stdd/` 目录

## Capabilities

### New Capabilities

- `flowchart-intent-parsing`：从用户自然语言中解析流程图类型（基本/泳道）、节点、分支条件、泳道角色
- `complexity-judgment`：自动判断复杂度，≤5节点直接画，>5节点先列清单确认
- `iso-5807-shape-mapping`：按 ISO 5807 标准映射形状（开始/结束→圆角矩形，处理→矩形，判断→菱形，数据→平行四边形，子流程→双边框矩形），作为默认基线
- `company-standard-override`：从 standards.md 读取公司内部规范，覆盖 ISO 5807 默认值。覆盖项包括形状类型、填充色、线条色、字体、字号、对齐方式等。无配置时回退到 ISO 5807 默认值
- `swimlane-layout`：泳道图角色识别、节点到泳道分配、跨泳道连线规则
- `visio-mcp-orchestration`：编排标准调用链（create_diagram → batch_draw_shapes → batch_connect_shapes → set_shape_format → save_document_as）
- `common-pattern-templates`：内置常见流程模板（登录认证、CRUD、审批流、订单处理、异常处理等），模板同样支持公司规范覆盖

## Impact

**代码层面**：
- 新增 1 个 SKILL.md 文件（~300-400 行）
- 新增 1 个 standards.md 文件（~50-100 行，公司规范配置）
- 新增 1 个 .mcp.json 配置文件

**配置层面**：
- `.mcp.json` 添加 visio-mcp server 配置项
- `standards.md` 由用户按公司规范填写

**基础设施**：
- `pip install visio-mcp`（Python 3.14+）
- 本机需已安装 Microsoft Visio Desktop

## Success Criteria

- [ ] 用户提及"流程图/泳道图/flowchart/swimlane"时 Skill 自动加载
- [ ] 正确识别基本流程图 vs 泳道图并选择对应 Visio 模板
- [ ] 默认按 ISO 5807 规范生成形状
- [ ] standards.md 有配置时，形状/颜色/字体按公司规范覆盖
- [ ] 泳道图正确分配节点到不同泳道
- [ ] >5节点先确认再画，≤5节点直接生成
- [ ] 输出 .vsdx 文件可在 Microsoft Visio 中正常打开编辑
