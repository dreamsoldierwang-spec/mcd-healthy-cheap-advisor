# 🥗 麦麦健康省钱顾问 · Mcd Healthy-Cheap Advisor

> 帮吃货在「健康」和「便宜」之间做今天的决策。
> 不是写文案，是给你一张能照着点单的「今日餐盘」。

**麦麦健康省钱顾问** 是一个基于 [麦当劳中国 MCP（`mcd-mcp`）](https://github.com/M-China/mcd-mcp-server) 的 WorkBuddy 创意 Skill，参加 **2026 麦当劳程序员创意开发大赛**。

它解决的真实痛点：想吃麦当劳，又怕胖、又想省钱。本 Skill 把三路真实 MCP 数据拼到一起——**营养表 + 当月活动 + 可领券**——做分析对比，给出「今天怎么吃得健康又便宜」的个性化餐盘方案。

---

## ✨ 和「麦麦种草机」的区别

| | 麦麦种草机 | 麦麦健康省钱顾问（本作） |
| --- | --- | --- |
| 受众 | 内容创作者 | 普通吃货 / 自己 |
| 产出 | 可发的小红书/公众号/抖音草稿 | 个人今日餐盘决策方案 |
| 核心 | 选题 + 成稿 + 排版 | 营养分析 + 优惠比价 + 组合建议 |
| 工具 | 44 工具中内容相关者 | 聚焦 3 工具（见下） |

两者复用同一个 `mcd-mcp` 接入，可同时安装、互不冲突。

## 🎯 核心功能

1. **真实取数**：调 `list-nutrition-foods`（营养）、`campaign-calendar`（今日活动）、`available-coupons`（可领券），绝不编造。
2. **营养分析**：按热量目标筛低卡；按「蛋白密度=蛋白÷能量」排高蛋白。
3. **优惠比价**：把券套到组合原价上，算到手价与省多少；提示可叠加的进行中活动。
4. **出方案**：1–3 套「今日餐盘」（热量/蛋白/到手价/省多少 + 推荐理由）。
5. **离线计算器**：`demo/今日餐盘计算器.html` 单文件可用，粘贴 JSON 即分析，评委与用户都能直接体验。

---

## 🔌 麦当劳 MCP 接入说明（必看）

> 本 Skill 依赖 `mcd-mcp`，接入步骤与麦麦种草机完全一致。

### 1. 申请 MCP Token
- 打开 [麦当劳 MCP 开放平台](https://open.mcd.cn/mcp)，登录 → 控制台 → 激活 → 申请 Token → 一键复制。

### 2. 在 WorkBuddy 配置 MCP
`~/.workbuddy/mcp.json` 中新增（若已装麦麦种草机则已存在，无需重复）：

```json
{
  "mcpServers": {
    "mcd-mcp": {
      "type": "streamableHttp",
      "url": "https://mcp.mcd.cn",
      "headers": { "Authorization": "Bearer 你的_MCP_TOKEN" }
    }
  }
}
```

> 接入地址 `https://mcp.mcd.cn`，协议 **Streamable HTTP**，请求头 `Authorization: Bearer <TOKEN>`。频率限制 600 次/分钟（超了 429）。

### 3. 启用 Skill
将本仓库的 `SKILL.md` 及 `references/`、`assets/` 放入 WorkBuddy 用户级或项目级 `skills/mcd-healthy-cheap-advisor/` 目录，对话中直接用自然语言触发（如「今天怎么吃健康又便宜」）。

---

## 📂 目录结构

```
mcd-healthy-cheap-advisor/
├── SKILL.md                      # 核心 Skill 定义（参赛主交付物）
├── README.md                     # 本文件：介绍 + MCP 接入说明
├── references/
│   ├── tool-fields.md            # 3 工具返回字段映射（防御性命名）
│   ├── analysis-playbook.md      # 营养筛选 + 组合 + 优惠匹配 + 综合评分算法
│   └── output-templates.md       # 今日餐盘 Markdown 输出模板
├── assets/
│   └── brand-kit.md              # 视觉设计参考（配色/字体/风格，非商标授权）
├── demo/
│   └── 今日餐盘计算器.html         # 单文件离线演示 / 实用伴侣
├── examples/
│   └── 示例输出.md                # 一次完整调用示例（mock 数据，仅演示）
└── 参赛声明.md                    # 原创性与合规声明
```

---

## 🚀 快速体验（无需 Token）

打开 `demo/今日餐盘计算器.html`：
1. 设热量目标（如 600 kcal）、预算、忌口；
2. 粘贴三个 MCP 工具返回的 JSON（或点「载入示例」）；
3. 一键算「今日餐盘」，支持复制 / 导出 Markdown / JSON。

---

## ⚠️ 合规声明（摘要）

- 本工具为**第三方决策辅助**，与麦当劳无官方关联，不暗示官方背书、合作或授权。
- 遵守《麦当劳 MCP 服务规则》与《使用条款》，仅用于**非商业**个人创作/自用。
- 所有营养 / 优惠 / 活动均来自 MCP 真实返回，缺数据处标注「以门店/活动页实际为准」，不编造。
- 麦当劳商标、Logo 仅作「被描述对象」出现，不构成任何授权。详见 `参赛声明.md`。

---

## 🏆 参赛信息

- **赛事**：2026 麦当劳程序员创意开发大赛（麦当劳中国 × WorkBuddy）
- **时间**：2026/10/9 10:30 – 2026/10/25 23:59
- **赛道**：基于麦当劳 MCP 的创意 Skill 开发
- **开发方式**：全程使用 WorkBuddy 辅助开发（享专项积分奖励）
