# Vibo

**See where your AI coding project stands.**

[简体中文](README.zh-CN.md) · [Download the latest preview](https://github.com/Bryce12322/vibo/releases/tag/v0.9.1)

Vibo turns the progress your coding agent reports into a local project dashboard: delivery goals, remaining work, checks, and things that need your attention. Keep coding in your usual conversation; check the board when you want the full picture.

## Get started

**Current preview: macOS + Codex. Requires Node.js 22.13 or newer.**

1. [Download vibo-local-v0.9.1.zip](https://github.com/Bryce12322/vibo/releases/download/v0.9.1/vibo-local-v0.9.1.zip) and unzip it.
2. Open **Install Vibo.command**, or give the extracted folder to Codex and ask it to install the bundled Vibo skill. The installer is not Apple-signed or notarized.
3. Start a new Codex chat in your actual project and say:

> Track this project with Vibo and open its board.

Continue developing normally. After you enable tracking, the agent is instructed to report meaningful progress without a separate synchronization prompt. If the skill is not discovered, start a new chat or restart Codex and explicitly use `$track-project`.

To add another project, enable Vibo in that project's own conversation. Both appear in the same local dashboard.

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
