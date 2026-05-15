# Capability: flowchart-intent-parsing

## ADDED Requirements

### Requirement: 流程图类型识别

系统 SHALL 从用户的自然语言输入中识别出流程图类型（基本流程图或泳道图）。

#### Scenario: 用户请求基本流程图

- **GIVEN** 用户输入包含"流程图/flowchart/画个流程/流程梳理"等关键词
- **AND** 输入中不包含泳道相关关键词
- **WHEN** Skill 解析用户输入
- **THEN** 系统 SHALL 识别为"基本流程图"类型
- **AND** 系统 SHALL 后续调用 create_diagram("basic_flowchart")

#### Scenario: 用户请求泳道图

- **GIVEN** 用户输入包含"泳道/swimlane/跨职能/部门/角色"等关键词
- **WHEN** Skill 解析用户输入
- **THEN** 系统 SHALL 识别为"泳道图"类型
- **AND** 系统 SHALL 后续调用 create_diagram("cross_functional_flowchart")

#### Scenario: 用户输入无明确流程图关键词

- **GIVEN** 用户输入未包含任何流程图相关关键词
- **WHEN** Skill 前端检查 description 匹配
- **THEN** 系统 SHALL 不加载此 Skill

### Requirement: 节点提取

系统 SHALL 从用户自然语言描述中提取流程节点列表及连接顺序。

#### Scenario: 从顺序描述提取节点

- **GIVEN** 用户描述为"用户登录 → 验证账号 → 进入首页"
- **WHEN** Skill 解析节点
- **THEN** 系统 SHALL 提取 3 个节点：["用户登录", "验证账号", "进入首页"]
- **AND** 节点间 SHALL 保持顺序连接关系

#### Scenario: 从含分支的描述提取节点

- **GIVEN** 用户描述为"提交申请 → 经理审批，通过则执行，不通过则退回"
- **WHEN** Skill 解析节点
- **THEN** 系统 SHALL 提取 4 个节点：["提交申请", "经理审批", "执行", "退回"]
- **AND** "经理审批" SHALL 标记为判断节点

### Requirement: 泳道角色提取

系统 SHALL 从泳道图需求中提取角色列表。

#### Scenario: 从描述中提取泳道角色

- **GIVEN** 用户描述为"用户提交订单 → 系统验证库存 → 仓库发货 → 用户收货"
- **AND** 流程图类型已识别为泳道图
- **WHEN** Skill 解析角色
- **THEN** 系统 SHALL 提取 3 个角色：["用户", "系统", "仓库"]
- **AND** 每个节点 SHALL 分配至对应角色泳道
