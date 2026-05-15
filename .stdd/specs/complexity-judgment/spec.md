# Capability: complexity-judgment

## ADDED Requirements

### Requirement: 节点数量判断

系统 SHALL 根据提取的节点数量判断交互模式。

#### Scenario: 简单流程直接生成

- **GIVEN** 提取的节点数量 ≤ 5
- **WHEN** Skill 评估复杂度
- **THEN** 系统 SHALL 跳过用户确认步骤
- **AND** 系统 SHALL 直接进入规范映射和 MCP 编排阶段

#### Scenario: 复杂流程先确认

- **GIVEN** 提取的节点数量 > 5
- **WHEN** Skill 评估复杂度
- **THEN** 系统 SHALL 暂停并展示节点清单
- **AND** 节点清单 SHALL 包含：节点名称、节点类型（开始/处理/判断/结束）、连接顺序

#### Scenario: 分支节点计入复杂度

- **GIVEN** 用户描述包含 2 个条件分支（菱形判断节点），主路径 3 个处理节点
- **WHEN** Skill 计算节点总数
- **THEN** 系统 SHALL 将所有分支路径中的节点计入总数
- **AND** 分支节点自身 SHALL 计入总数

### Requirement: 用户确认交互

系统 SHALL 在复杂流程中支持用户修改节点清单。

#### Scenario: 用户确认节点清单

- **GIVEN** Skill 已展示节点清单给用户
- **WHEN** 用户回复"确认"或"没问题"
- **THEN** 系统 SHALL 以确认的节点清单继续执行
- **AND** 进入规范映射阶段

#### Scenario: 用户修改节点清单

- **GIVEN** Skill 已展示节点清单给用户
- **WHEN** 用户回复包含修改意见（如"把审核改成两级审核"、"增加一个通知节点"）
- **THEN** 系统 SHALL 根据修改意见更新节点清单
- **AND** 系统 SHALL 重新展示更新后的清单供确认
