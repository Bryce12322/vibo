# Vibo

**See where your AI coding project stands.**

[简体中文](README.zh-CN.md) · [Download the latest preview](https://github.com/Bryce12322/vibo/releases/tag/v0.9.1)

Vibo turns the progress your coding agent reports into a local project dashboard: delivery goals, remaining work, checks, and things that need your attention. Keep coding in your usual conversation; check the board when you want the full picture.

## Online preview — no local server required

[Open Vibo online](https://vibo.bryceyufeng.workers.dev) · [Remote MCP endpoint](https://vibo.bryceyufeng.workers.dev/mcp)

Start without an account. Choose your coding tool on the website, connect the remote MCP server, approve browser authorization, then ask your project agent to track this project with Vibo. The agent follows the server's reporting instructions during normal development.

Online Vibo stores progress records in Cloudflare. It does not upload source code or read every conversation. Existing local records stay on your device unless you explicitly select an export to import. Guest access depends on this browser or a still-authorized agent connection; do not promise recovery after both are lost.

**Preview status:** browser authorization, the official MCP client, progress reports, and live page updates have been verified against the deployed service. Native Codex, Cursor and Claude Code setup still needs host-specific testing; some tools may require manual MCP configuration or a new conversation. Account login is being configured and is not yet advertised as available. The local 0.9.1 package below remains supported.

## Local version

**Current preview: macOS + Codex. Requires Node.js 22.13 or newer.**

### Install with one message

Copy this into Codex:

> Install Vibo for me from https://github.com/Bryce12322/vibo — download, verify, unzip and install its Codex skill.

Codex can complete the download, checksum verification, extraction and installation for you. You do not need to download or unzip the package yourself. It may request permission to access the network or install local files; approve the request to continue. If Node.js is missing or too old, Codex will explain the requirement before proceeding.

Vibo installs as a local **Codex skill**, named `track-project`. [Installation steps for coding agents](INSTALL.md) include the exact release URLs and commands. Download the release asset, not GitHub's automatic “Source code” ZIP.

### Use it in your project

After installation, say in your actual project chat:

> Track this project with Vibo and open its board.

If Codex has not loaded the newly installed skill, send the instruction in a new chat or restart Codex and explicitly use `$track-project`. Continue developing normally; the agent is instructed to report meaningful progress without a separate synchronization prompt.

To add another project, enable Vibo in that project's own conversation. Both appear in the same local dashboard.

<details>
<summary>Prefer manual installation?</summary>

[Download vibo-local-v0.9.1.zip](https://github.com/Bryce12322/vibo/releases/download/v0.9.1/vibo-local-v0.9.1.zip), unzip it, then open **Install Vibo.command**. The installer is not Apple-signed or notarized.

</details>

## What you can see

- Work grouped by delivery goal, including development, deployment, domains and other launch tasks.
- Remaining work first, with implemented work folded away.
- Explicit requests for your input, separate from ordinary implementation status.
- Check evidence and change history, without treating AI self-checks as human acceptance.
- Multiple local projects and an English / 简体中文 interface.

## Local by design

No Vibo account, domain or cloud service is needed. The local service binds to `127.0.0.1` and stores your records on your device. The dashboard receives updates after your agent reports them; Vibo does not scan source code or monitor every chat. Automatic reporting depends on your host loading and following the skill.

For compatibility, the installed skill is named `track-project` and data stays in `~/Library/Application Support/Qingzhou/`. Do not share that folder's connection files, database or backups. Installing an update preserves existing project records.

## Help

Ask Codex: **Check whether Vibo is working.** For a backup, ask: **Back up my Vibo data.** Include your OS, Node.js version and the visible error when [reporting an issue](https://github.com/Bryce12322/vibo/issues); do not attach private project data or connection files.

This is a local preview. Windows installers, cloud sync, team accounts and token-usage statistics are not included. Release downloads contain the complete runtime and skill; the repository provides distribution instructions.
