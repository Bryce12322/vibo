# Vibo

**See where your AI coding project stands.**

[简体中文](README.zh-CN.md) · [Open online](https://vibo.bryceyufeng.workers.dev) · [Setup guide](CONNECT.md) · [Local 0.9.1](https://github.com/Bryce12322/vibo/releases/tag/v0.9.1)

Vibo turns progress reported by your coding agent into a project dashboard: delivery goals, remaining work, and things that need your attention. Keep coding in your usual tool; open the board for the full picture.

## Start with one message

Send this in your actual project conversation:

> Follow the setup guide at https://github.com/Bryce12322/vibo to connect Vibo to this coding tool and load its ongoing reporting rules, guide me through required authorization, then track this project, sync its existing plan, open the dashboard in this tool’s built-in browser first (external browser only as a fallback), and report meaningful progress during development.

Online Vibo requires no local Vibo service or Node.js. Your agent can perform the setup allowed by its host and guide you through required permissions. Some hosts need manual MCP setup, a new conversation or a restart; fully automatic installation is not guaranteed for every tool. [Agent setup procedure](CONNECT.md).

## How it works

1. Connect the remote MCP server and authorize it in the browser; no account is required.
2. The agent associates this project and syncs goals and tasks from real context.
3. Open the board in the agent’s built-in browser beside the conversation. Use an external browser if in-app browsing is unsupported or fails.
4. Continue developing. The agent follows loaded rules to report progress without a separate synchronization request.

MCP URL: `https://vibo.bryceyufeng.workers.dev/mcp`. Transport: Streamable HTTP with browser OAuth. See [CONNECT.md](CONNECT.md) for configuration and ongoing reporting.

## What you can see

- Delivery goals covering development, deployment, domains, payment setup and other launch work.
- Remaining work first, with implemented work folded away.
- Explicit requests for your input, separate from implementation status.
- Check evidence and change history; AI self-checks are not human acceptance.
- Multiple projects and English / 简体中文 interfaces.

## Data and sign-in

Start as a guest. Online progress records are stored in Cloudflare. Optional GitHub sign-in links guest projects to an account so you can access them from other browsers or devices. It requests public GitHub identity only, with no repository permissions.

Guest access depends on this browser or a valid agent connection. Sign in before switching devices; without an account link or a valid connection, recovery is not guaranteed. Existing local records are uploaded only when you explicitly select an export to import.

Vibo displays what your agent actually reports. It does not scan source code or monitor other conversations. Ongoing reporting depends on the host loading and following the rules.

## Preview status

The online version is **0.10.0-preview**. Verified:

- Browser authorization against the deployed HTTPS service and discovery of all 7 tools through the official MCP client.
- Project, goal and task creation, progress reports and live page updates.
- Real GitHub sign-in retaining guest project IDs, task status and history.
- Recovery of the same project in two independent browser sessions on one computer.
- 52 automated checks.

**Still pending:** native Codex, Cursor and Claude Code onboarding, reporting-rule discovery across conversations, ongoing automatic reporting, load testing and backup recovery drills. The guide describes the intended setup, not certification of every host. This is a preview for small-scale trials.

## Local version: macOS + Codex

Requires Node.js 22.13 or newer. Users who want records stored on their device can continue using **local 0.9.1**.

<details>
<summary>Ask Codex to install the local version</summary>

> Follow the local-version steps at https://github.com/Bryce12322/vibo/blob/main/INSTALL.md to download, verify, unzip and install the Vibo 0.9.1 local skill for me.

Download [vibo-local-v0.9.1.zip](https://github.com/Bryce12322/vibo/releases/download/v0.9.1/vibo-local-v0.9.1.zip), not GitHub's automatic Source code ZIP. The repository root is not an installable skill. [Full installation and checksum instructions](INSTALL.md).

After installation, ask “Track this project with Vibo and open its board.” If the skill is not discovered, start a new conversation or restart and explicitly use `$track-project`.

For compatibility, the skill is named `track-project` and records stay in `~/Library/Application Support/Qingzhou/`. The service listens on `127.0.0.1`; updates preserve existing records. The installer is not Apple-signed or notarized.

</details>

## Feedback

[Report an issue](https://github.com/Bryce12322/vibo/issues) with the online/local version, coding tool and version, OS and visible error. Include Node.js version for local installations. Never attach verification codes, connection credentials, private project data or full conversations.

This repository provides setup and distribution documentation; local release downloads include the complete runtime and skill. Team collaboration and token-usage statistics are not included.
