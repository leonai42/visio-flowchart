# Capability: iso-5807-shape-mapping

## ADDED Requirements

### Requirement: 节点类型到形状的默认映射

系统 SHALL 按 ISO 5807 标准将节点类型映射到 Visio 形状，作为未配置公司规范时的默认值。

#### Scenario: 开始/结束节点映射

- **GIVEN** 节点被标注为"开始"或"结束"类型
- **AND** standards.md 中无对应覆盖配置
- **WHEN** Skill 映射形状
- **THEN** 系统 SHALL 使用"圆角矩形"（Rounded Rectangle）形状

#### Scenario: 处理节点映射

- **GIVEN** 节点被标注为"处理"类型
- **AND** standards.md 中无对应覆盖配置
- **WHEN** Skill 映射形状
- **THEN** 系统 SHALL 使用"矩形"（Rectangle）形状

#### Scenario: 判断节点映射

- **GIVEN** 节点被标注为"判断"类型（包含"是否/如果/审批/判断/验证"等关键词）
- **AND** standards.md 中无对应覆盖配置
- **WHEN** Skill 映射形状
- **THEN** 系统 SHALL 使用"菱形"（Diamond）形状

#### Scenario: 数据/输入输出节点映射

- **GIVEN** 节点被标注为"数据"或"输入/输出"类型
- **AND** standards.md 中无对应覆盖配置
- **WHEN** Skill 映射形状
- **THEN** 系统 SHALL 使用"平行四边形"（Parallelogram）形状

#### Scenario: 子流程节点映射

- **GIVEN** 节点被标注为"子流程"类型
- **AND** standards.md 中无对应覆盖配置
- **WHEN** Skill 映射形状
- **THEN** 系统 SHALL 使用"双边框矩形"（Double-border Rectangle）形状

### Requirement: 连接线样式

系统 SHALL 为连接线设置默认样式。

#### Scenario: 判断分支标注

- **GIVEN** 连接线从判断节点出发
- **WHEN** Skill 创建连接
- **THEN** 系统 SHALL 在连接线上标注"是/否"或用户描述中的分支条件文本

#### Scenario: 默认箭头样式

- **GIVEN** 任意两个节点间有连接
- **WHEN** Skill 创建连接
- **THEN** 系统 SHALL 使用带箭头的直线连接器
