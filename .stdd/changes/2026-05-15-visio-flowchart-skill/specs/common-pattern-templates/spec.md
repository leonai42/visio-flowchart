# Capability: common-pattern-templates

## ADDED Requirements

### Requirement: 内置常见流程模板

系统 SHALL 提供常见业务场景的流程模板，加快常用流程图生成。

#### Scenario: 登录认证模板

- **GIVEN** 用户请求"登录流程"或"认证流程"
- **WHEN** Skill 匹配到内置模板
- **THEN** 系统 SHALL 使用预设节点：[开始, 输入账号密码, 验证账号, 验证通过?, 进入首页, 显示错误提示, 结束]
- **AND** "验证通过?" SHALL 为判断节点（菱形）

#### Scenario: CRUD 操作模板

- **GIVEN** 用户请求"新增/编辑/删除"类 CRUD 操作流程
- **WHEN** Skill 匹配到内置模板
- **THEN** 系统 SHALL 使用预设节点：[开始, 接收请求, 校验参数, 参数有效?, 执行数据库操作, 返回结果, 返回错误信息, 结束]

### Requirement: 模板支持自定义

系统 SHALL 允许用户在内置模板基础上修改节点。

#### Scenario: 基于模板修改节点

- **GIVEN** Skill 加载了内置"登录流程"模板
- **AND** 用户说"登录流程，但是需要加一个验证码校验"
- **WHEN** Skill 应用模板并合并用户修改
- **THEN** 节点清单 SHALL 在"验证账号"步骤前增加"验证码校验"
