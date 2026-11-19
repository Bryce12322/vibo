# Vibo

**See where your AI coding project stands, what remains and what needs you.**

[简体中文](README.zh-CN.md) · [Install](INSTALL.md) · [Local preview 0.9.3](https://github.com/Bryce12322/vibo/releases/tag/v0.9.3)

## 一句话安装并开始使用 / Install and start with one message

> 请阅读 https://github.com/Bryce12322/vibo/blob/main/INSTALL.md ，自动下载、校验并安装适配当前工具的 Vibo 本地版，接着读取汇报规则、同步当前项目的已有计划，优先在内置浏览器打开看板，并在后续开发中主动更新真实进展。

English

> Read https://github.com/Bryce12322/vibo/blob/main/INSTALL.md, download, verify and install the local Vibo skill for this tool, then load its reporting rules, sync this project's existing plan, open the board in the built-in browser first, and proactively report real progress as development continues.

Paste either message into the conversation for the project you are building. It requests both installation and project tracking. macOS and Node.js 22.13+ are required. Your tool may still show permission prompts.

The default is **local Skill + CLI**. Records stay on your device. No MCP connector, OAuth flow or account is needed for local use. Your host may request permission to execute commands.

The agent installs the complete package, saves a concise plan in one submission and opens the board. Continue developing as usual. Goals, implementation, actual checks and requests for your input are updated through loaded rules. Existing project IDs are reused.

## Requirements and verified scope

macOS and Node.js 22.13+. A suitable WorkBuddy-managed Node runtime can be reused.

- Codex installation entry and local CLI workflows verified.
- WorkBuddy 5.11.3 visibly discovered and enabled the installed Skill. CLI workflows verified. Native multi-turn reporting, cross-chat continuity and in-app opening still need complete host verification.
- 59 automated tests passed, covering upgrades, multi-project isolation, batch submission, retry deduplication, rollback, checks, backup and recovery.
- Other operating systems and hosts remain unverified.

Vibo displays agent-reported progress. Continued reporting depends on the host loading and following the rules.

Development, deployment, domain and payment work are grouped by delivery goals. Remaining work appears first, implemented items fold away, and checks remain separate from implementation and human acceptance.

The service listens on 127.0.0.1. The Skill remains track-project and data stays in ~/Library/Application Support/Qingzhou/ for compatibility. Updates back up the previous Skill. The installer is not Apple-signed or notarized.

## Optional online use

The [online preview](https://vibo.bryceyufeng.workers.dev) remains available through the [optional online setup](CONNECT.md#online). Existing cloud associations are preserved. Local and cloud records do not automatically synchronize in both directions.

WorkBuddy online OAuth callback registration compatibility remains unresolved. Use the local entry for initial trials.

[Report an issue](https://github.com/Bryce12322/vibo/issues) with tool, OS and Vibo versions plus the visible error. Omit credentials, private databases and full conversations.

This repository provides distribution documentation. Release packages include the complete Skill and runtime.
