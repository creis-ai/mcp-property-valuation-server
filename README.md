# 🏙️ 中指房产估值 MCP

[![NPM Version](https://img.shields.io/npm/v/mcp-property-valuation-server.svg?logo=npm)](https://www.npmjs.com/package/mcp-property-valuation-server)
[![Node.js Version](https://img.shields.io/badge/node-%3E%3D18-green.svg?logo=node.js)](https://nodejs.org)
[![zh-CN](https://img.shields.io/badge/lang-zh--CN-red.svg)](https://github.com/creis-ai/mcp-property-valuation-server/blob/master/README.md)
[![en](https://img.shields.io/badge/lang-en-red.svg)](https://github.com/creis-ai/mcp-property-valuation-server/blob/master/README.en.md)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![MCP Server](https://img.shields.io/badge/MCP-Server-blue)](https://modelcontextprotocol.io)

> 为 AI 助手提供「小区评级 / 小区评估 / 房产估值」专业能力的 MCP Server。为房产交易、投资尽调、押品风控等场景提供权威数据支撑。

---

## ✨ 功能特性

- **多维度小区评级**：基于活跃度、物业服务、教育资源、板块位置等指标提供 A/B/C/D 等级评定。
- **精准小区评估**：提供小区均价及时间范围内价格走势分析。
- **房产价值评估**：支持对单套房产进行精准估值，提供总价和单价。
- **企业级安全认证**：通过 APPID 授权机制确保数据安全。
- **标准化输出格式**：统一的 Markdown 格式输出，便于集成和展示。

---

## 🚀 快速开始

### 1. 获取授权 (APPID)

使用本服务前，您需要先获取有效的 `APPID`。

📧 **请联系**: `creisxcx1@fang.com` 获取您的专属 `APPID`。

### 2. 配置 MCP 客户端

您可以在任何支持 Model Context Protocol (MCP) 的客户端（如 Claude Desktop、MCP IDE 等）中，通过以下配置来启用本服务。

#### 方式一：Stdio 方式

当本项目正式发布到 NPM 后，您可以通过 `npx` 直接运行，配置将更加简洁：

```json
{
  "mcpServers": {
    "property-valuation": {
      "transportType": "stdio",
      "command": "npx",
      "args": ["-y", "mcp-property-valuation-server"],
      "env": {
        "MCP-INDUSTRY-APPID": "您的APPID"
      }
    }
  }
}
```

#### 方式二：连接到线上服务 (SSE)

如果您有可供公网访问的线上服务地址，也可以使用 SSE 模式：

```json
{
  "mcpServers": {
    "cih-property-valuation": {
      "transportType": "sse",
      "url": "https://creis.cih-index.com/mcp/sse",
      "headers": {
        "MCP-INDUSTRY-APPID": "您的APPID"
      }
    }
  }
}
```

### 3. 验证连接

配置完成后，重启您的 MCP 客户端。如果配置正确，您应该能在客户端的可用工具列表中看到以下三个工具：

- `get_community_rating`
- `get_community_valuation`
- `get_property_valuation`

---

## 🔑 授权与认证

本服务需要有效的 `MCP-INDUSTRY-APPID` 才能正常使用。如需获取授权，请联系：

📧 `creisxcx1@fang.com`

---

## 🛠️ 工具定义与使用

本 MCP Server 提供以下工具：

### 1. `get_community_rating` - 小区评级

基于活跃度、物业服务、教育资源、板块位置等多维度指标，为住宅小区提供等级评定（A/B/C/D），帮助用户快速了解小区整体品质。

**输入参数:**

| 字段             | 必填 | 类型   | 说明                             |
| ---------------- | ---- | ------ | -------------------------------- |
| `city`           | ✅   | string | 所在城市，例如：“北京”           |
| `district`       | ✅   | string | 所在区县，例如：“丰台区”         |
| `community_name` | ✅   | string | 小区名称，例如：“中海丰和叁号院” |

**输出示例:**

```markdown
小区评级为 A
活跃度评级为 B
物业评级为 A
教育评级为 A
板块评级为 B
```

### 2. `get_community_valuation` - 小区评估

支持查询住宅小区均价、时间范围内价格走势，科学评估小区市场表现与价值变化。

**输入参数:**

| 字段             | 必填 | 类型   | 说明                                              |
| ---------------- | ---- | ------ | ------------------------------------------------- |
| `city`           | ✅   | string | 所在城市，例如：“北京”                            |
| `district`       | ✅   | string | 所在区县，例如：“丰台区”                          |
| `community_name` | ✅   | string | 小区名称，例如：“中海丰和叁号院”                  |
| `start_time`     | ❌   | string | 开始时间，格式：`yyyy-mm`，为空则返回最新月份数据 |
| `end_time`       | ❌   | string | 结束时间，格式：`yyyy-mm`，为空则返回最新月份数据 |

**输出示例:**

```markdown
2024-01 小区均价为：65000 元/m²
2024-02 小区均价为：65500 元/m²
2024-03 小区均价为：66000 元/m²
```

### 3. `get_property_valuation` - 房产估值

支持对单套房产进行估值，提供估值总价、单价。通过智能评估模型，精准评估房产价值，同时适用于押品估值场景。

**输入参数:**

| 字段             | 必填 | 类型    | 说明                             |
| ---------------- | ---- | ------- | -------------------------------- |
| `city`           | ✅   | string  | 所在城市，例如：“北京”           |
| `district`       | ✅   | string  | 所在区县，例如：“丰台区”         |
| `community_name` | ✅   | string  | 小区名称，例如：“中海丰和叁号院” |
| `orientation`    | ✅   | string  | 房屋朝向，例如：“南北”           |
| `floor_area`     | ✅   | number  | 建筑面积，单位：㎡               |
| `located_floor`  | ✅   | integer | 所在楼层                         |
| `total_floors`   | ✅   | integer | 总楼层数                         |

**输出示例:**

```markdown
**小区估值总价：** 850 万元
**小区估值单价：** 65385 元/m²
```

---

## 🤝 合作与支持

- **问题反馈**: 请通过 [GitHub Issues](https://github.com/creis-ai/mcp-property-valuation-server/issues) 提交您的问题或建议。
- **联系我们**: 如需获取 `APPID`、商务合作或技术支持，请联系 `creisxcx1@fang.com`。

---

_由 CIH Web Team 开发维护_
