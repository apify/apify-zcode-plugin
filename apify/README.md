# Apify for ZCode

Run ready-made Actors from Apify, the largest marketplace of tools for AI, or build and publish your own. The plugin adds the Apify MCP server, an `apify` routing agent, the `/create-actor` command, and five skills covering the main Apify workflows: using existing Actors, building and deploying Actors, actorizing existing projects, generating Actor output schemas, and integrating Apify into existing applications.

中文文档：[README_CN.md](./README_CN.md)

## Components and how to trigger them

| Component | Registered as | How to trigger it |
|---|---|---|
| Agent `apify` | `apify:apify` | Describe an Apify task in a ZCode session, or select the `apify` agent. It routes the request to the right skill, MCP tool, or CLI/SDK path. This is the main entry point. |
| Command `/create-actor` | `/create-actor` | Type `/create-actor`, optionally followed by a description of the Actor you want. Runs a guided Actor-development workflow. |
| Skill `apify-actor-development` | `apify:apify-actor-development` | Create, debug, and deploy a new Actor. |
| Skill `apify-actorization` | `apify:apify-actorization` | Convert an existing JS/TS, Python, or CLI project into an Actor. |
| Skill `apify-generate-output-schema` | `apify:apify-generate-output-schema` | Generate dataset, output, and key-value store schemas for an existing Actor. |
| Skill `apify-sdk-integration` | `apify:apify-sdk-integration` | Add Actor execution to an existing app with the `apify-client` package. |
| Skill `apify-ultimate-scraper` | `apify:apify-ultimate-scraper` | Select, configure, and run pre-built Actors for multi-step data extraction across 15+ platforms. |
| MCP server `apify` | `plugin:apify:apify` | Used by the agent to search the Apify Store, fetch Actor details, run Actors, read datasets, and look up Apify docs. |

The `apify` agent invokes skills when your request matches them. You can also ask for a skill by name; the bare skill name (for example `apify-actorization`) works as an alias for `apify:<skill>`.

Example requests:

```
Find 5 well-rated coffee shops in Seattle and export them to CSV
Build an Actor that scrapes a sitemap and stores the page titles
Add Apify to this Next.js app so I can run a scraper from /api/scrape
Generate output schemas for the Actor in this folder
```

## Dependencies

- An Apify account. [Sign up free](https://console.apify.com/sign-up), no credit card required.
- For the CLI-based workflows (`apify-actor-development`, `apify-actorization`, `apify-ultimate-scraper`, `/create-actor`): Node.js with npm, and the Apify CLI (`npm install -g apify-cli`).
- For `apify-sdk-integration`: the `apify-client` package in your own application (JavaScript/TypeScript or Python).

## Credentials

- **MCP server:** OAuth. The first time the agent calls an MCP tool, ZCode opens `console.apify.com` in your browser to sign in. Every MCP tool requires sign-in, including Store search and docs lookup. The plugin itself stores no token.
- **Apify CLI:** `apify login` stores credentials in `~/.apify/auth.json`. In headless environments, export `APIFY_TOKEN` instead and the CLI reads it automatically.
- **SDK integration:** your application reads `APIFY_TOKEN` from its environment.

Create API tokens at [console.apify.com/settings/integrations](https://console.apify.com/settings/integrations).

## Network access

| Host | Used for |
|---|---|
| `mcp.apify.com` | The bundled MCP server. |
| `console.apify.com`, `console-backend.apify.com` | OAuth sign-in. |
| `api.apify.com` | Apify API calls from the CLI and `apify-client`. |
| `docs.apify.com` | Apify documentation. |
| npm registry | Only when you install `apify-cli` or `apify-client`. |

## Permissions and command execution

- Nothing runs at install time. The plugin has no hooks and no bundled scripts.
- MCP tool calls go through ZCode's tool approval.
- The CLI-based workflows run `apify …` commands, and `npm` when installing packages, through ZCode's shell tool.

## Side effects

- Running Actors uses your Apify account and consumes your Apify platform usage and credits.
- `apify push` deploys Actor code to your Apify account.
- The Actor-development skills and `/create-actor` write project files into your workspace, such as `.actor/`, source files, and a `Dockerfile`. The SDK-integration skill edits your application's source and dependencies.

## Third-party services

The plugin connects to the Apify platform, operated by Apify Technologies s.r.o. Use of the platform is governed by the [Apify Privacy Policy](https://docs.apify.com/legal/privacy-policy) and the [Apify General Terms and Conditions](https://docs.apify.com/legal/general-terms-and-conditions). The plugin contains no third-party code or assets.

## License

Apache-2.0. See [LICENSE](./LICENSE).
