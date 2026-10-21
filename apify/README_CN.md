# Apify for ZCode

运行 Apify（最大的 AI 工具市场）上的现成 Actor，或构建并发布你自己的 Actor。本插件提供 Apify MCP 服务器、`apify` 路由 Agent、`/create-actor` 命令，以及覆盖 Apify 主要工作流的五个技能：使用现成的 Actor、构建并部署 Actor、将现有项目改造为 Actor、生成 Actor 输出 schema，以及将 Apify 集成到现有应用中。

English documentation: [README.md](./README.md)

## 组件及触发方式

| 组件 | 注册名称 | 如何触发 |
|---|---|---|
| Agent `apify` | `apify:apify` | 在 ZCode 会话中描述 Apify 任务，或选择 `apify` Agent。它会把请求路由到合适的技能、MCP 工具或 CLI/SDK 路径。这是主要入口。 |
| 命令 `/create-actor` | `/create-actor` | 输入 `/create-actor`，可附带你想要的 Actor 的描述。运行引导式 Actor 开发工作流。 |
| 技能 `apify-actor-development` | `apify:apify-actor-development` | 创建、调试和部署新的 Actor。 |
| 技能 `apify-actorization` | `apify:apify-actorization` | 将现有的 JS/TS、Python 或 CLI 项目转换为 Actor。 |
| 技能 `apify-generate-output-schema` | `apify:apify-generate-output-schema` | 为现有 Actor 生成数据集、输出和键值存储的 schema。 |
| 技能 `apify-sdk-integration` | `apify:apify-sdk-integration` | 使用 `apify-client` 包为现有应用添加 Actor 执行能力。 |
| 技能 `apify-ultimate-scraper` | `apify:apify-ultimate-scraper` | 选择、配置并运行预置 Actor，完成覆盖 15+ 平台的多步骤数据提取。 |
| MCP 服务器 `apify` | `plugin:apify:apify` | Agent 用它搜索 Apify Store、获取 Actor 详情、运行 Actor、读取数据集和查询 Apify 文档。 |

当你的请求与技能匹配时，`apify` Agent 会调用相应技能。你也可以按名称指定技能；裸技能名（例如 `apify-actorization`）可作为 `apify:<skill>` 的别名。

示例请求：

```
找出西雅图 5 家评分高的咖啡店并导出为 CSV
构建一个抓取站点地图并保存页面标题的 Actor
把 Apify 集成到这个 Next.js 应用，让我能通过 /api/scrape 运行爬虫
为此文件夹中的 Actor 生成输出 schema
```

## 依赖

- 一个 Apify 账号。[免费注册](https://console.apify.com/sign-up)，无需信用卡。
- 基于 CLI 的工作流（`apify-actor-development`、`apify-actorization`、`apify-ultimate-scraper`、`/create-actor`）需要：Node.js 和 npm，以及 Apify CLI（`npm install -g apify-cli`）。
- `apify-sdk-integration` 需要：在你自己的应用（JavaScript/TypeScript 或 Python）中使用 `apify-client` 包。

## 凭据

- **MCP 服务器：** OAuth。Agent 首次调用 MCP 工具时，ZCode 会在浏览器中打开 `console.apify.com` 进行登录。所有 MCP 工具都需要登录，包括 Store 搜索和文档查询。插件本身不存储任何 token。
- **Apify CLI：** `apify login` 将凭据存储在 `~/.apify/auth.json` 中。在无头环境中，改为导出 `APIFY_TOKEN`，CLI 会自动读取。
- **SDK 集成：** 你的应用从其环境中读取 `APIFY_TOKEN`。

在 [console.apify.com/settings/integrations](https://console.apify.com/settings/integrations) 创建 API token。

## 网络访问

| 主机 | 用途 |
|---|---|
| `mcp.apify.com` | 捆绑的 MCP 服务器。 |
| `console.apify.com`、`console-backend.apify.com` | OAuth 登录。 |
| `api.apify.com` | CLI 和 `apify-client` 调用 Apify API。 |
| `docs.apify.com` | Apify 文档。 |
| npm registry | 仅在安装 `apify-cli` 或 `apify-client` 时。 |

## 权限与命令执行

- 安装时不运行任何内容。插件不包含 hooks，也不包含捆绑脚本。
- MCP 工具调用需经过 ZCode 的工具批准。
- 基于 CLI 的工作流会通过 ZCode 的 shell 工具运行 `apify …` 命令，安装包时还会运行 `npm`。

## 副作用

- 运行 Actor 会使用你的 Apify 账号，并消耗你的 Apify 平台用量和额度。
- `apify push` 会将 Actor 代码部署到你的 Apify 账号。
- Actor 开发技能和 `/create-actor` 会向你的工作区写入项目文件，例如 `.actor/`、源代码文件和 `Dockerfile`。SDK 集成技能会修改你的应用源代码和依赖。

## 第三方服务

本插件连接由 Apify Technologies s.r.o. 运营的 Apify 平台。平台的使用受 [Apify 隐私政策](https://docs.apify.com/legal/privacy-policy) 和 [Apify 通用条款与条件](https://docs.apify.com/legal/general-terms-and-conditions) 约束。本插件不包含第三方代码或资源。

## 许可证

Apache-2.0。见 [LICENSE](./LICENSE)。
