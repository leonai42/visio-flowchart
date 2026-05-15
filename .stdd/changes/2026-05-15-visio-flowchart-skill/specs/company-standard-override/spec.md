# Capability: company-standard-override

## ADDED Requirements

### Requirement: 读取公司规范配置

系统 SHALL 在映射形状前读取 standards.md，查找覆盖配置。无配置时回退到 ISO 5807 默认值。

#### Scenario: standards.md 存在且有覆盖配置

- **GIVEN** `.claude/skills/visio-flowchart/standards.md` 文件存在
- **AND** 文件中配置了"处理节点颜色=#1E90FF，字体=微软雅黑"
- **WHEN** Skill 映射"处理"节点的样式
- **THEN** 系统 SHALL 使用填充色 #1E90FF
- **AND** 系统 SHALL 使用字体"微软雅黑"
- **AND** 形状类型 SHALL 仍使用 ISO 5807 默认值（因为颜色/字体覆盖不影响形状类型）

#### Scenario: standards.md 存在但某项无覆盖

- **GIVEN** standards.md 存在
- **AND** standards.md 中未配置"判断节点"的颜色
- **WHEN** Skill 映射"判断"节点的样式
- **THEN** 系统 SHALL 回退到 ISO 5807 默认的颜色值

#### Scenario: standards.md 不存在

- **GIVEN** `.claude/skills/visio-flowchart/standards.md` 文件不存在
- **WHEN** Skill 尝试读取配置
- **THEN** 系统 SHALL 全部使用 ISO 5807 默认值
- **AND** 不报错

### Requirement: 规范配置校验

系统 SHALL 对 standards.md 中的配置值进行基本格式校验。

#### Scenario: 颜色值格式校验

- **GIVEN** standards.md 中配置了 `颜色=#GGGGGG`（无效的 hex 颜色）
- **WHEN** Skill 校验配置
- **THEN** 系统 SHALL 忽略该无效配置项
- **AND** 系统 SHALL 提示用户该配置项无效，已回退到默认值

#### Scenario: 有效配置正常应用

- **GIVEN** standards.md 中配置了 `颜色=#1E90FF`（有效的 hex 颜色）
- **WHEN** Skill 校验并应用配置
- **THEN** 系统 SHALL 正常应用该颜色值
