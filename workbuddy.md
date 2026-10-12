# WorkBuddy 开发上下文（workbuddy.md）

本项目「麦麦健康省钱顾问」使用腾讯 WorkBuddy 智能体开发完成，本文件用于核验是否符合本次活动 WorkBuddy 联动奖励条件。

## 开发环境与方式

- 开发工具：腾讯 WorkBuddy（AI 智能体开发环境，https://www.workbuddy.cn）
- 主要能力使用：Skill 定义与编写、MCP 自定义连接器配置、对话式代码生成与调试、单文件 HTML 演示构建
- MCP 接入：在 WorkBuddy「自定义连接器」配置 `mcd-mcp`（Streamable HTTP，https://mcp.mcd.cn），使用用户自行申请的麦当劳 MCP Token（仅存于本地 WorkBuddy 配置，未写入本项目任何文件）

## 开发过程关键上下文

1. 需求构思：基于麦当劳 MCP 的「营养 + 活动 + 优惠券」三路能力，确定"个人决策顾问"方向（回答"今天怎样吃得健康又便宜"）
2. Skill 编写：产出 `SKILL.md`，定义「问偏好 → 取数 → 分析对比 → 出今日餐盘 → 合规」工作流，并配套 `references/` 三份算法与模板
3. 演示构建：用 WorkBuddy 生成单文件离线 HTML 计算器（`demo/今日餐盘计算器.html`），粘贴 3 个 Tool 的 JSON 即分析出 Top 餐盘
4. 配置验证：编写 `mcp-config.example.json`（脱敏，仅环境变量占位符）与 `MCP_INTEGRATION.md`
5. 合规自查：依据活动规则产出 `CONTEST_DECLARATION.md`（官方原文）并核对内容合规

## 真实性说明

项目确为使用 WorkBuddy 原创开发；麦当劳 MCP Token 仅存于用户本地 WorkBuddy 配置，本项目中所有配置文件均使用 `${MCD_MCP_TOKEN}` 占位符，不含任何真实凭证或他人个人信息。
