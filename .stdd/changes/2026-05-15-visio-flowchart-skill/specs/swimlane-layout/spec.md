# Capability: swimlane-layout

## ADDED Requirements

### Requirement: 节点到泳道的分配

系统 SHALL 将提取的节点按角色分配到对应泳道。

#### Scenario: 按角色分配节点

- **GIVEN** 用户描述泳道图为"用户提交订单 → 系统验证库存 → 仓库发货"
- **AND** 已提取角色列表：["用户", "系统", "仓库"]
- **WHEN** Skill 分配节点到泳道
- **THEN** "用户提交订单" SHALL 分配到"用户"泳道
- **AND** "系统验证库存" SHALL 分配到"系统"泳道
- **AND** "仓库发货" SHALL 分配到"仓库"泳道

#### Scenario: 泳道顺序

- **GIVEN** 已提取多个泳道角色
- **WHEN** Skill 创建泳道图
- **THEN** 泳道 SHALL 按角色在用户描述中的首次出现顺序排列（从上到下）

### Requirement: 跨泳道连接

系统 SHALL 在泳道间创建跨泳道连接线。

#### Scenario: 跨泳道连接

- **GIVEN** 节点 A 在"用户"泳道，节点 B 在"系统"泳道
- **AND** 节点 A 连接到节点 B
- **WHEN** Skill 创建连接
- **THEN** 系统 SHALL 创建从泳道 A 到泳道 B 的跨泳道连接线
- **AND** 连接线 SHALL 保持箭头方向正确
