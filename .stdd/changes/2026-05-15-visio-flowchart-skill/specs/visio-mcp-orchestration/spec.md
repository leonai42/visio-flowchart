# Capability: visio-mcp-orchestration

## ADDED Requirements

### Requirement: 标准 MCP 调用链

系统 SHALL 按固定顺序调用 visio-mcp 工具生成流程图。

#### Scenario: 基本流程图标准调用链

- **GIVEN** 流程图为基本流程图类型，节点清单已确定
- **WHEN** Skill 执行生成
- **THEN** 调用顺序 SHALL 为：create_diagram → batch_draw_shapes → batch_connect_shapes → set_shape_format → save_document_as
- **AND** 各步之间 SHALL 不跳过

#### Scenario: 保存路径

- **GIVEN** 流程图已生成
- **WHEN** Skill 保存文件
- **THEN** 系统 SHALL 将文件保存到当前工作目录
- **AND** 文件名 SHALL 基于流程主题生成（如 `用户登录流程.vsdx`）
- **AND** 如文件已存在 SHALL 提示用户是否覆盖

### Requirement: 前置检查

系统 SHALL 在执行 MCP 调用前检查环境可用性。

#### Scenario: Visio 未运行

- **GIVEN** Microsoft Visio 未启动
- **WHEN** Skill 执行前置检查
- **THEN** 系统 SHALL 提示"请先启动 Microsoft Visio 后再试"
- **AND** 不执行后续 MCP 调用

#### Scenario: MCP 未安装

- **GIVEN** visio-mcp 未安装
- **WHEN** Skill 检查 visio-mcp 可用性
- **THEN** 系统 SHALL 提示"请先安装 visio-mcp：pip install visio-mcp"

### Requirement: 格式设置

系统 SHALL 在生成形状后应用样式设置。

#### Scenario: 应用样式

- **GIVEN** 形状已通过 batch_draw_shapes 创建
- **AND** 样式规范已确定（ISO 5807 或公司规范覆盖）
- **WHEN** Skill 调用 set_shape_format
- **THEN** 每个形状 SHALL 应用对应的填充色、线条色、字体、字号
