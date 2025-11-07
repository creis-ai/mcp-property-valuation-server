# 🏙️ CIH Property Valuation MCP

[![NPM Version](https://img.shields.io/npm/v/mcp-property-valuation-server.svg?logo=npm)](https://www.npmjs.com/package/mcp-property-valuation-server)
[![Node.js Version](https://img.shields.io/badge/node-%3E%3D18-green.svg?logo=node.js)](https://nodejs.org)
[![zh-CN](https://img.shields.io/badge/lang-zh--CN-red.svg)](https://github.com/creis-ai/mcp-property-valuation-server/blob/master/README.md)
[![en](https://img.shields.io/badge/lang-en-red.svg)](https://github.com/creis-ai/mcp-property-valuation-server/blob/master/README.en.md)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![MCP Server](https://img.shields.io/badge/MCP-Server-blue)](https://modelcontextprotocol.io)

<!-- Apply for Access Token -->
<!-- [![Apply For Access Token](https://img.shields.io/badge/%E7%94%B3%E8%AF%B7%E5%BC%80%E9%80%9A-gray?label=%F0%9F%91%8B)](https://wuye-ai.cricbigdata.com/mcp) -->
<!-- Practical Guide -->
<!-- [![Practical Guide](https://img.shields.io/badge/%E5%AE%9E%E8%B7%B5%E6%8C%87%E5%8D%97-gray?label=%F0%9F%A7%AD)](https://wuye-ai.cricbigdata.com/mcp) -->

> An MCP Server that provides AI assistants with professional capabilities for "community rating / community evaluation / property valuation". Offers authoritative data support for real estate transactions, investment due diligence, collateral risk control and other scenarios.

---

## ✨ Features

- **Multi-dimensional Community Rating**: Provides A/B/C/D grade ratings based on activity, property services, educational resources, location, and other indicators.
- **Precise Community Evaluation**: Offers community average prices and price trend analysis within a time range.
- **Property Value Assessment**: Supports precise valuation of individual properties, providing total price and unit price.
- **Enterprise-level Security Authentication**: Ensures data security through APPID authorization mechanism.
- **Standardized Output Format**: Unified Markdown format output for easy integration and display.

---

## 🚀 Quick Start

### 1. Get Authorization (APPID)

Before using this service, you need to obtain a valid `APPID`.

📧 **Contact**: `creisxcx1@fang.com` to get your exclusive `APPID`.

### 2. Configure MCP Client

You can enable this service through the following configuration in any client that supports Model Context Protocol (MCP) (such as Claude Desktop, MCP IDE, etc.).

#### Method 1: Stdio Method

When this project is officially released to NPM, you can run it directly through `npx` with a more concise configuration:

```json
{
  "mcpServers": {
    "property-valuation": {
      "transportType": "stdio",
      "command": "npx",
      "args": ["-y", "mcp-property-valuation-server"],
      "env": {
        "MCP-INDUSTRY-APPID": "Your APPID"
      }
    }
  }
}
```

#### Method 2: Connect to Online Service (SSE)

If you have a public online service address, you can also use SSE mode:

```json
{
  "mcpServers": {
    "cih-property-valuation": {
      "transportType": "sse",
      "url": "https://creis.cih-index.com/mcp-service",
      "headers": {
        "MCP-INDUSTRY-APPID": "Your APPID"
      }
    }
  }
}
```

<!-- **Recommended** official MCP Server URLs:

- Test Environment: `https://testcreis.cih-index.com/mcp-service`
- Production Environment: `https://creis.cih-index.com/mcp-service` -->

### 3. Verify Connection

After configuration, restart your MCP client. If configured correctly, you should see the following three tools in the client's available tools list:

- `get_community_rating`
- `get_community_valuation`
- `get_property_valuation`

---

## 🔑 Authorization and Authentication

This service requires a valid `MCP-INDUSTRY-APPID` to function properly. For authorization, please contact:

📧 `creisxcx1@fang.com`

---

## 🛠️ Tool Definitions and Usage

This MCP Server provides the following tools:

### 1. `get_community_rating` - Community Rating

Based on multi-dimensional indicators such as activity, property services, educational resources, and location, it provides grade ratings (A/B/C/D) for residential communities, helping users quickly understand the overall quality of the community.

**Input Parameters:**

| Field            | Required | Type   | Description                                            |
| ---------------- | -------- | ------ | ------------------------------------------------------ |
| `city`           | ✅       | string | City, e.g., "Beijing"                                  |
| `district`       | ✅       | string | District, e.g., "Fengtai District"                     |
| `community_name` | ✅       | string | Community name, e.g., "Zhonghai Fenghe No.3 Courtyard" |

**Output Example:**

```markdown
Community rating is A
Activity rating is B
Property service rating is A
Education rating is A
Location rating is B
```

### 2. `get_community_valuation` - Community Valuation

Supports querying community average prices and price trends within a time range, scientifically evaluating community market performance and value changes.

**Input Parameters:**

| Field            | Required | Type   | Description                                                         |
| ---------------- | -------- | ------ | ------------------------------------------------------------------- |
| `city`           | ✅       | string | City, e.g., "Beijing"                                               |
| `district`       | ✅       | string | District, e.g., "Fengtai District"                                  |
| `community_name` | ✅       | string | Community name, e.g., "Zhonghai Fenghe No.3 Courtyard"              |
| `start_time`     | ❌       | string | Start time, format: `yyyy-mm`, returns latest month's data if empty |
| `end_time`       | ❌       | string | End time, format: `yyyy-mm`, returns latest month's data if empty   |

**Output Example:**

```markdown
2024-01 Community average price: 65,000 yuan/m²
2024-02 Community average price: 65,500 yuan/m²
2024-03 Community average price: 66,000 yuan/m²
```

### 3. `get_property_valuation` - Property Valuation

Supports valuation of individual properties, providing estimated total price and unit price. Through intelligent evaluation models, it accurately assesses property value and is also suitable for collateral valuation scenarios.

**Input Parameters:**

| Field            | Required | Type    | Description                                            |
| ---------------- | -------- | ------- | ------------------------------------------------------ |
| `city`           | ✅       | string  | City, e.g., "Beijing"                                  |
| `district`       | ✅       | string  | District, e.g., "Fengtai District"                     |
| `community_name` | ✅       | string  | Community name, e.g., "Zhonghai Fenghe No.3 Courtyard" |
| `orientation`    | ✅       | string  | House orientation, e.g., "North-South"                 |
| `floor_area`     | ✅       | number  | Building area, unit: m²                                |
| `located_floor`  | ✅       | integer | Floor number                                           |
| `total_floors`   | ✅       | integer | Total number of floors                                 |

**Output Example:**

```markdown
**Estimated Total Price:** 8.5 million yuan
**Estimated Unit Price:** 65,385 yuan/m²
```

---

## 🤝 Cooperation and Support

- **Feedback**: Please submit your questions or suggestions through [GitHub Issues](https://github.com/creis-ai/mcp-property-valuation-server/issues).
- **Contact Us**: For APPID acquisition, business cooperation, or technical support, please contact `creisxcx1@fang.com`.

---

_Developed and maintained by CIH Web Team_
