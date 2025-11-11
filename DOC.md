# 房产估值 MCP Server 接入

通过 MCP 协议提供与房产估值 MCP 的安全交互。

[前往云开发平台运行 MCP Server](https://tcb.cloud.tencent.com/dev#/ai?tab=mcp&p&mcp-template=mcp-mongo)

---

## 环境变量

- 需要将 **MCP-INDUSTRY-APPID** 配置为 **房产估值 MCP AppID**。如果不提供，则使用实际请求 HTTP Authorization Header 中的值。
- 可选配置项：需要将 **MODE** 配置为 **运行模式**，支持 `stdio` 和 `http` 两种模式。如果不提供，默认为 `stdio`。
- 可选配置项：需要将 **HOSTNAME** 配置为 **HTTP 绑定主机名**，仅在 `http` 模式下有效。如果不提供，默认为 `0.0.0.0`，即为绑定到本机所有 IP 地址。
- 可选配置项：需要将 **PORT** 配置为 **HTTP 绑定端口**，仅在 `http` 模式下有效。如果不提供，默认为 `3011`。

具体配置要求也可以参考 [README](https://github.com/creis-ai/mcp-property-valuation-server/blob/master/README.md)。

## 🗺️ 功能清单

| 工具名称                        | 功能描述                                                                                                          | 核心参数                                                                                                                                                                 |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| community_rating（小区评级）    | 提供住宅小区评级（A/B/C/D）、活跃度评级（A/B/C/D）、物业评级（A/B/C/D）、教育评级（A/B/C/D）、板块评级（A/B/C/D） | city（所在城市）、district（所在区县）、community_name（小区名称）                                                                                                       |
| community_valuation（小区评估） | 提供住宅小区均价                                                                                                  | city（所在城市）、district（所在区县）、community_name（小区名称）、start_time（开始时间）、end_time（结束时间）                                                         |
| property_valuation（房产估值）  | 提供单个房产估值总价、估值单价                                                                                    | city（所在城市）、district（所在区县）、community_name（小区名称）、orientation（房屋朝向）、floor_area（建筑面积）、located_floor（所在楼层）、total_floors（总楼层数） |

## 仓库地址

[https://github.com/creis-ai/mcp-property-valuation-server](https://github.com/creis-ai/mcp-property-valuation-server)

## 🔌 使用方式

- [在云开发 Agent 中使用](https://docs.cloudbase.net/ai/mcp/use/agent)
- [在 MCP Host 中使用](https://docs.cloudbase.net/ai/mcp/use/mcp-host)
- [通过 SDK 接入](https://docs.cloudbase.net/ai/mcp/use/sdk)

---

[云开发 MCP 控制台](https://tcb.cloud.tencent.com/dev#/ai?tab=mcp)
