# MCP 集成说明（MCP Integration）

本文件说明「麦麦健康省钱顾问」实际使用的麦当劳 MCP Server、Tool、调用流程与业务价值，用于活动资格核验。

## 使用的麦当劳 MCP Server

- Server 名称：麦当劳 MCP（官方仓库 M-China/mcd-mcp-server）
- 接入地址：`https://mcp.mcd.cn`
- 传输方式：Streamable HTTP
- 鉴权方式：Bearer Token（用户自行在 open.mcd.cn 申请的麦当劳 MCP Token，仅存于本地 WorkBuddy 配置）

## 实际使用的 Tool

本 Skill 在"今日餐盘"决策流程中**真实调用**以下 Tool 获取真实数据（非虚构、非占位）：

| Tool | 用途 |
|---|---|
| `list-nutrition-foods` | 餐品营养信息（能量/蛋白质/脂肪/碳水化合物/钠/钙），用于筛选高蛋白低卡餐品、计算营养密度 |
| `campaign-calendar` | 当月营销活动日历（进行中 / 往期 / 未来），用于匹配今日可参与的优惠活动 |
| `available-coupons` | 可领取的麦麦省券列表（券名 / 门槛 / 优惠 / 有效期），用于比价与到手价计算 |

## 调用流程

1. 用户描述偏好（热量目标、预算、忌口、是否外送）
2. Skill 触发，调用上述 3 个麦当劳 MCP Tool 拉取真实营养 / 活动 / 券数据
3. 数据经 `references/analysis-playbook.md` 的算法加工：筛选低卡高蛋白餐品 → 匹配进行中活动 → 叠加可领券算到手价 → 综合评分
4. 输出 1–3 套"今日餐盘"方案（热量 / 蛋白质 / 到手价 / 省多少 + 推荐理由 + 取舍说明）

## 业务价值

把三路麦当劳官方 MCP 数据做分析对比，从"领券工具"升级为"个人决策顾问"，帮用户回答"今天怎样吃得健康又便宜"，契合本次活动"用创意解决实际问题"的宗旨。
