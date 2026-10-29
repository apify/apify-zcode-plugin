# Changelog

All notable changes to the **Apify for ZCode** plugin are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.2] - 2026-10-21

### Added
- `description_i18n` (`en`, `zh-CN`) in `apify/.zcode-plugin/plugin.json` and the `marketplace.json` entry.
- Plugin documentation in `apify/README.md` and `apify/README_CN.md`: components and how to trigger them, dependencies, credentials, network access, permissions, side effects, and third-party services.
- `apify/LICENSE`.

## [1.0.1] - 2026-08-25

### Changed
- Updated Apify MCP server URL in `apify/.mcp.json` to include `?client=zcode+plugin` for client identification.

## [1.0.0] - 2026-08-18 — Initial ZCode release

### Added
- `apify` MCP server entry in `apify/.mcp.json` pointing to `https://mcp.apify.com/`.
- `apify/.zcode-plugin/plugin.json` manifest with plugin metadata and component paths.
- Root `marketplace.json` with `source: "./apify"` for marketplace discovery.
- Apache-2.0 license.
