# Vibo

**看懂 AI 编程项目的进展。**

[English](README.md) · [下载最新体验版](https://github.com/Bryce12322/vibo/releases/tag/v0.9.1)

Vibo 把 Agent 上报的进展整理成可视化看板：项目要达成什么、还有哪些工作、检查结果如何，以及现在需要你处理什么。继续在 Codex 对话里开发，需要了解全貌时打开看板。

## 线上预览：无需本地服务

[打开 Vibo](https://vibo.bryceyufeng.workers.dev) · [远程 MCP 地址](https://vibo.bryceyufeng.workers.dev/mcp)

可以免登录开始。在网页选择编码工具，添加远程 MCP 连接并完成浏览器授权，然后在实际项目里说“用 Vibo 跟踪这个项目”。Agent 根据服务提供的规则，在正常开发过程中汇报进展。

线上版将进展记录保存在 Cloudflare，不上传源代码，也不读取所有对话。原有本地记录留在电脑，只有主动选择导出文件后才会上传导入。访客访问依赖当前浏览器或仍有效的 Agent 连接；两者都丢失时无法保证找回记录。

**预览验证范围：** 已实测正式服务的浏览器授权、官方 MCP 客户端调用、进展上报和页面实时更新。Codex、Cursor、Claude Code 的宿主原生接入仍需分别实测，可能需要手动配置 MCP 或开启新对话。账号登录正在配置，尚未宣传为可用。本地 0.9.1 版仍可按下方方式使用。

## 本地版使用

**当前支持 macOS + Codex，需要 Node.js 22.13 或更新版本。**

### 一句话安装

把这句话发给 Codex：

> 帮我安装 Vibo：https://github.com/Bryce12322/vibo，请自动完成下载、校验、解压和 Skill 安装。

Codex 可以替你完成整个安装流程，不需要手动下载、解压或打开安装文件。如果 Codex 请求联网或本地安装授权，同意后即可继续。缺少 Node.js 或版本过低时，Codex 会先说明需要补齐的环境。

Vibo 以本地 **Codex Skill** 的形式安装，Skill 名称为 `track-project`。[给 Codex 的安装指引](INSTALL.md)提供了明确的下载地址和操作步骤。使用 Release 中的安装包，不要选择 GitHub 自动生成的“Source code”压缩包。

### 在项目中使用

安装后，在实际项目对话中说：

> 用 Vibo 跟踪这个项目，并打开看板。

如果 Codex 尚未加载刚安装的 Skill，开启新对话或重启 Codex 后再试，也可以用 `$track-project` 明确调用。接下来正常描述开发需求即可，Agent 会按规则上报进展，不需要每次单独说“同步进展”。

增加其他项目时，在那个项目自己的对话中启用 Vibo，左侧项目栏就会出现它。

<details>
<summary>希望手动安装？</summary>

[下载 vibo-local-v0.9.1.zip](https://github.com/Bryce12322/vibo/releases/download/v0.9.1/vibo-local-v0.9.1.zip)，解压后打开 **Install Vibo.command**。当前安装文件尚未经过 Apple 签名或公证。

</details>

## 能看到什么

- 按交付目标组织的工作，包括功能开发、部署、域名和上线准备。
- 待推进事项优先，已实现事项默认折叠。
- 只有明确需要你处理的事项才提醒，执行状态与关注原因分开。
- 检查证据和变更记录；AI 自检不会冒充人工验收。
- 同一台设备上的多个项目，以及中文、英文界面。

## 数据保存在本机

不需要 Vibo 账号、域名或云服务。本地服务仅监听 `127.0.0.1`，数据留在你的电脑。看板实时展示 Agent 已上报的变化，不扫描代码，也不监听所有聊天；自动上报依赖宿主正确加载和调用 Skill。

为兼容旧版，Skill 名称仍为 `track-project`，数据目录仍为 `~/Library/Application Support/Qingzhou/`。请勿公开其中的连接文件、数据库或备份。重新安装更新会保留项目记录。

## 遇到问题

在 Codex 中说“帮我检查 Vibo 是否正常”，或“帮我备份 Vibo 数据”。[反馈问题](https://github.com/Bryce12322/vibo/issues)时，请提供系统、Node.js 版本和可见报错，不要上传私人项目数据或连接文件。

当前是本地体验版，暂不包含 Windows 安装器、云同步、团队账号和 Token 用量统计。Release 安装包包含完整运行文件及 Skill，本仓库提供分发和使用说明。
